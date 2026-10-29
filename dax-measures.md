# DAX Measures and Calculated Columns

All measures live in the `_Measures` table. Calculated columns are listed under the table they belong to.

## Data model

| Table | Role | Connects to Sales by |
|---|---|---|
| `Sales` | Fact table | n/a |
| `Products` | Dimension | `ProductKey` |
| `Customers` | Dimension | `CustomerKey` |
| `Stores` | Dimension (StoreKey 0 = online) | `StoreKey` |
| `Date` | Dimension (calculated table) | `Order Date` |
| `Exchange_Rates` | Not used in any measure | none |

Each dimension filters `Sales` one-to-many, in a single direction.

---

## Base measures

**Revenue is modeled** from unit list price and unit cost (USD columns). Discounts and exchange rates are not applied.

```dax
Total Gross Revenue =
SUMX(Sales, Sales[Quantity] * RELATED(Products[Unit Price USD]))
```

```dax
Total Cost of Goods Sold =
SUMX(Sales, RELATED(Products[Unit Cost USD]) * Sales[Quantity])
```

```dax
Gross Profit = [Total Gross Revenue] - [Total Cost of Goods Sold]
```

```dax
Gross Profit Margin = DIVIDE([Gross Profit], [Total Gross Revenue])
```

```dax
Total Units Sold = SUM(Sales[Quantity])
```

```dax
Distinct Order Count = DISTINCTCOUNT(Sales[Order Number])
```

---

## Time measures

```dax
Avg Revenue per Day =
DIVIDE([Total Gross Revenue], DISTINCTCOUNT('Date'[Date]))
```
Divides revenue by calendar days, so shorter months (February) aren't penalized. Verified: February shows 142 days across 2016-2020 (29 + 28 + 28 + 28 + 29).

```dax
Days in Period = DISTINCTCOUNT('Date'[Date])
```
Used to check the day counts behind `Avg Revenue per Day`.

```dax
Days With Sales = DISTINCTCOUNT(Sales[Order Date])
```
Used to find the missing sales days in March, April and on Sundays.

---

## Store measures

```dax
Months Open =
VAR DataStart = CALCULATE(MIN(Sales[Order Date]), REMOVEFILTERS())
VAR DataEnd   = CALCULATE(MAX(Sales[Order Date]), REMOVEFILTERS())
VAR StartDate = MAX(MAX(Stores[Open Date]), DataStart)
RETURN
IF(HASONEVALUE(Stores[StoreKey]), DATEDIFF(StartDate, DataEnd, MONTH))
```
Counts months from the later of the store's opening date and the first order date, to the last order date. It returns a value only for a single store, so use it with `Store Label` in the visual's details well. Stores opened before 2016 show 61 months.

```dax
Revenue per Month Open = DIVIDE([Total Gross Revenue], [Months Open])
```
Lets older and newer stores be compared fairly.

```dax
Avg Orders per Store =
AVERAGEX(
    FILTER(VALUES(Stores[StoreKey]), Stores[StoreKey] <> 0),
    [Distinct Order Count]
)
```
Average distinct orders per physical store (online excluded). It responds to the Country and State slicers, and isn't adjusted for months open.

---

## Calculated columns

### `Sales`

```dax
Age at Order =
VAR Birth = RELATED(Customers[Birthday])
VAR OrderDate = Sales[Order Date]
VAR BirthdayThisYear = DATE(YEAR(OrderDate), MONTH(Birth), DAY(Birth))
RETURN
DATEDIFF(Birth, OrderDate, YEAR) - IF(BirthdayThisYear > OrderDate, 1, 0)
```
Age on the order date. It subtracts a year when the birthday hasn't happened yet, because `DATEDIFF(..., YEAR)` alone counts calendar-year boundaries.

```dax
Age Group =
SWITCH(
    TRUE(),
    Sales[Age at Order] < 18, "Under 18",
    Sales[Age at Order] >= 18 && Sales[Age at Order] <= 29, "Young Adults",
    Sales[Age at Order] >= 30 && Sales[Age at Order] <= 44, "Adults",
    Sales[Age at Order] >= 45 && Sales[Age at Order] <= 64, "Older Adults",
    "Seniors"
)
```

```dax
Age Group Sort Order =
SWITCH(
    TRUE(),
    Sales[Age at Order] < 18, 1,
    Sales[Age at Order] >= 18 && Sales[Age at Order] <= 29, 2,
    Sales[Age at Order] >= 30 && Sales[Age at Order] <= 44, 3,
    Sales[Age at Order] >= 45 && Sales[Age at Order] <= 64, 4,
    5
)
```
`Age Group` is sorted by this column, so charts run from Under 18 to Seniors.

### `Stores`

```dax
Channel = IF(Stores[StoreKey] = 0, "Online", "Physical store")
```
Online orders are recorded under StoreKey 0. The country and store charts filter to Physical store.

```dax
Store Label =
Stores[Country] & " - " & Stores[State] & " (#" & Stores[StoreKey] & ")"
```
Gives each store a readable name for the order-volume chart and the scatter plots.

```dax
Store Age in Years =
IF(
    ISBLANK(Stores[Open Date]),
    BLANK(),
    DATEDIFF(Stores[Open Date], DATE(2021, 2, 20), MONTH) / 12
)
```
Years from the opening date to the end of the data (February 20, 2021). The end date is hard-coded, so update it if the data is refreshed with later dates. The online row has no opening date and stays blank.

### `Date` (calculated table)

```dax
Date = CALENDAR(MIN(Sales[Order Date]), MAX(Sales[Order Date]))
```

```dax
Year = YEAR('Date'[Date])
```

```dax
Quarter = "Q" & QUARTER('Date'[Date])
```

```dax
Month = FORMAT('Date'[Date], "mmmm")
```

```dax
Month Number = MONTH('Date'[Date])
```

```dax
Month Year = FORMAT('Date'[Date], "mmm yyyy")
```

```dax
Month Year Sort = 'Date'[Year] * 100 + 'Date'[Month Number]
```

```dax
Month Start = DATE(YEAR('Date'[Date]), MONTH('Date'[Date]), 1)
```
First day of each month. It's used on a continuous date axis so the monthly trend shows year labels instead of 60 crowded month labels.

```dax
Day = DAY('Date'[Date])
```

```dax
Day of Week = FORMAT('Date'[Date], "dddd")
```

```dax
Day of Week Number = WEEKDAY('Date'[Date], 2)
```
`Day of Week` is sorted by this column (Monday = 1).

---

## Notes and limitations

- `FORMAT` returns month and day names in the language of the machine that refreshes the report.
- `Months Open` returns blank above single-store level, by design.
- `Store Age in Years` uses a fixed end date and is approximate to the month, since `DATEDIFF` counts month boundaries.
- Someone born on February 29 is treated as having a March 1 birthday in non-leap years. This has a negligible effect on age groups.
- The trend pages apply a page filter that excludes 2021, because the data ends on February 20, 2021.
