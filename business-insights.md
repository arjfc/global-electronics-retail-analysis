# Business Insights

These insights match the final dashboard. Every figure was checked against the underlying tables. Trend analysis covers 2016-2020; the dataset ends on February 20, 2021.

## Business Insights: Product Popularity
WWI Desktop PC2.33 X2330 Black is the highest-selling product, with about 550 units sold. All of the top 10 products by units sold are desktops (Computers → Desktops), spread across the WWI and Adventure Works brands.

## Business Insights: Product Profitability
WWI Desktop PC2.33 X2330 Black also ranks first by gross profit ($338K), so it leads on both units and profit. Desktops make up 8 of the top 10 products by gross profit. The other two are Adventure Works 52" LCD HDTV X590 models ($264K and $250K).

## Business Insights: Product Margin
The highest-margin products, mainly DVD Storage Binders and Centrex phone systems, earn gross margins of about 67%, against 58.58% overall. Margins within this top group are nearly identical. Revenue and cost are calculated from fixed unit prices and unit costs, so each product's margin reflects its unit economics and not its sales volume. Margin should therefore be read alongside units sold and gross profit dollars.

## Business Insights: Customer Group Revenue
Customers aged 45-64 generate the most gross revenue ($16.4M), followed by customers aged 65+ ($15.4M). Adults (30-44) contribute $12.5M and Young Adults (18-29) $10.2M. Only customers under 18 contribute little, at $1.2M. Older Adults also place the most orders (7.9K), ahead of Seniors (7.3K). Age is calculated at the order date, so one customer can fall into different age groups across years.

## Business Insight: Geographic Sales Performance
Among physical stores, the United States is the dominant market at $23.8M, or 53.6% of physical-store revenue. The United Kingdom follows at $5.7M (13.0%), then Germany ($4.2M, 9.6%), Canada ($3.6M, 8.1%), Australia ($2.1M, 4.7%), Italy ($2.1M, 4.6%) and the Netherlands ($1.6M, 3.6%). France is lowest at $1.2M (2.8%). These are totals, and differences in store count between countries were not examined.

## Business Insight: Online vs Physical Store Revenue
Online sales account for $11.4M, or 20.45% of total revenue ($55.76M), and physical stores for $44.35M (79.55%). The country charts cover physical stores only, so they exclude the online portion.

## Business Insight: Revenue by Year
Gross revenue grew from $6.9M in 2016 to $7.4M in 2017, $12.8M in 2018 and a peak of $18.3M in 2019. It then fell 49.1% to $9.3M in 2020. 2021 is excluded because the dataset ends on February 20, 2021.

## Business Insight: Revenue by Month-Year
From 2016 to 2019, monthly revenue shows a recurring dip around March and April, with recovery from May and stronger performance toward year-end. December consistently ranks among the strongest months, and the overall level of monthly revenue rose substantially through 2019. In 2020, revenue stayed strong through February and then declined sharply for the rest of the year. The March-April dips coincide with far fewer days that have recorded sales (see the next insight).

## Business Insight: Calendar Month Seasonality
Measured as average revenue per calendar day across 2016-2020, February is the strongest month ($52K), followed by December ($48K) and January ($40K). April is the weakest ($4K), and March is also low ($17K). Much of this decline reflects missing sales days: April has recorded sales on only 33 of 150 days and March on 87 of 155, against 140 or more in every other month. Per selling day, April is about $18K against roughly $30K in March and $32K in May, so April is still lower but far less extreme. The recurring March-April dip should be investigated as a possible data gap before calling it seasonality.

## Business Insight: Day-of-Week Performance
Saturday generates the highest gross revenue ($12.9M) and the most distinct orders (6.1K), followed by Thursday ($10.5M, 5.0K) and Wednesday ($9.7M, 4.6K). Tuesday and Friday are close ($7.6M and $7.5M, about 3.5K orders each), and Monday is lower ($5.6M). Friday is clearly below Thursday on both revenue and orders.

Sunday is unusually low: $0.9M in revenue (about 1.6% of the total) and about 0.4K orders. Part of this is missing days. Sundays have recorded sales on only 26 dates in 2016 and 25 in 2020, against 47 in 2019. Even in a complete year, Sunday revenue per selling day is far below Saturday's (about $8K against $89K in 2019). The pattern appears in both channels (online $158K, stores $736K), so store closures alone cannot explain it. It should be investigated as a possible data-recording or operational issue.

## Business Insight: Store Age Performance
Using revenue per month open, so older stores don't benefit just from trading longer, there is no clear relationship between store age and revenue. Stores of similar age range from under $5K to more than $20K per month. Country looks like a stronger driver: U.S. stores sit highest and French stores lowest across the ages where both appear.

## Business Insight: Store Size Performance
Store size does not show a clear relationship with revenue per month open. Most stores under about 700 m² are French and earn little, though two small German stores earn about $12K per month, so size and country are mixed together. Stores around 2,000 m² range from roughly $7K to $29K per month, showing that similar footprints can perform very differently.

## Business Insights: Product Underperformance
Games and Toys is the lowest category by gross revenue and gross profit, at $724.8K in revenue and $396.7K in gross profit. Most of that comes from Download Games ($632.9K), so Boxed Games is the weak part, at $92.0K in revenue and $51.9K in gross profit. Fans are also among the weakest subcategories, under $100K. Music, Movies and Audio Books contains only one subcategory, Movie DVD, at about $3.13M. VCD & DVD ($314.0K in revenue and $175.0K in gross profit) is one of the weaker TV and Video subcategories, though it doesn't appear in the Bottom 5 chart.

## Business Insight: Store Order Volume
The average physical store processes about 364 distinct orders (stores with no recorded sales may be excluded from this average). The spread is wide. Canada (590) and the United States (558) lead, followed by the United Kingdom (398), Italy (297), Germany (238), the Netherlands (194), Australia (180) and France (82). These are averages per physical store and are not adjusted for months open or store count. The 15 lowest-volume stores each have no more than 176 orders, and 7 of them are in France. The lowest, Australia - Northern Territory (#2), opened in January 2008 and has only 4 orders ($15.2K revenue), which looks like a data issue or a nearly inactive store. At least four stores (#3, #7, #11 and #25) have no recorded sales and don't appear in the scatter plots.

---

## Data and method notes

- Revenue is modeled: unit list price × quantity, and cost is unit cost × quantity. It doesn't include discounts, operating costs or exchange-rate adjustments.
- The dataset runs from January 1, 2016 to February 20, 2021. Year, month and weekday analyses cover 2016-2020 only. The Page 1 KPI cards and the age-group charts include 2021, which is why $55.76M differs from the $54.72M in the weekday matrix.
- Recorded sales cover about 47 dates per weekday per year, not 52, with the largest gaps in March and April and on Sundays in 2016 and 2020.
- Online orders are StoreKey 0, and country charts show physical stores only.
- Age is measured at the order date, and store age is measured to February 20, 2021.

## Business analysis framework

1. What products sell the most?
2. What products generate the most profit dollars?
2.1. Which products have the best profit efficiency?
3. Which customer age group contributes most to sales?
4. Which country has the most sales? (physical stores; online revenue is shown separately by channel)
5.1. What is the overall sales trend by year?
5B.1. How does gross revenue change month by month?
5B.2. Which calendar months generate the most revenue per day?
6. Which day of the week has the highest sales and orders?
7. Do older or newly opened stores perform better? (revenue per month open)
8. Do larger stores perform better than smaller stores? (revenue per month open)
9. Which product categories and subcategories perform poorly?
10. How many orders does each store receive?