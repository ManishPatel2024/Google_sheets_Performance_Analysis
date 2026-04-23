# Google_sheets_Performance_Analysis
Store Discount Performance Analysis — Google Sheets
A two-year retail discount analysis built entirely in Google Sheets, examining how discount strategy across four store branches relates to revenue performance across fiscal years 2024–25 and 2025–26.


### Project Overview
This project was built in response to a real-world brief: given two years of raw store sales data, complete an Overview tab in Google Sheets that answers specific business questions about discounting, store performance, and category contribution — using formulas, tabular summaries, and visualisations.

The dataset contains approximately 82,000 rows of transaction-level data across two fiscal year tabs, and required careful handling before any analysis could begin.


### The Data
The workbook contains three sheets:

Overview — completed analysis tab with KPI summaries, comparison tables, and charts
24-25 — 41,293 rows of sales data for fiscal year 2024–25 (columns: Order ID, Order Date, Fiscal Year, Store Branch, Unit Price, Discount %, Discount Amount, Total, Product Name, Product Category)
25-26 — 41,293 rows of sales data for fiscal year 2025–26 (same fields, slightly different column layout — no Fiscal Year column, Store Branch shifts to column C)

Four store branches: California Branch, Illinlois Branch, LA Branch, Seattle Branch

Discount bands present in the data: 0%, 5%, 10%, 14%, 15%, 17%, 19%, 20%, 25%, 30%, 35%, 40%, 45%, 50%, 60%, 65%, 100%

Refund rows: Both sheets contain refund transactions recorded as negative values in the Total column — 2,164 in FY24-25 and 1,491 in FY25-26. These were identified and excluded from all calculations.


### Thought Process
Step 1 — Audit before analysing
The two data sheets have subtly different column layouts. In FY24-25, Total sits in column H and Store Branch in column D. In FY25-26, Total is in column G and Store Branch in column C. Failing to account for this would produce incorrect formula results. Every formula in the Overview tab was written with this difference in mind.
Step 2 — Handle refunds correctly
Refund rows (negative Total values) are genuine business records but would distort any revenue total, order count, or discount average if included. The decision was made to exclude them from all calculations using WHERE Total > 0 in QUERY formulas and ">"&0 conditions in SUMIF/AVERAGEIF functions. This gives a clean picture of actual sales performance.
Step 3 — Choose the right tools for each question
Different questions called for different formula approaches:

SUMIF / COUNTIF / AVERAGEIF — for straightforward single-condition totals (e.g. total revenue per year)
SUMPRODUCT — for multi-condition filtering where SUMIFS would be awkward (e.g. revenue by store, excluding refunds)
AVERAGEIFS — for average discount % per store, filtered to positive orders only
COUNTIFS — for order counts by discount band
QUERY with Col notation — for grouped category analysis; Col1/Col2 notation was used instead of column letters to avoid Google Sheets parse errors with certain data configurations
Step 4 — Surface the insight, not just the numbers
The goal wasn't to produce tables of figures — it was to identify what the data is actually saying. Each summary table was designed to make the key finding visible at a glance, supported by conditional formatting (green/red) on year-over-year changes and charts that make the comparisons immediate.


### Key Insights
1. Higher discounting in FY25-26 did not drive revenue growth
FY25-26 had a higher average discount rate (8.5%) than FY24-25 (6.9%), yet revenue fell from $4.17M to $2.23M and order volume nearly halved — from 37,283 to 19,733 transactions. More discounting correlated with worse performance, not better. This is the headline finding of the analysis.<br/>
2. Illinois Branch was the only store to grow year-over-year (refer to KPI card in google sheet dashboard)
Illinois grew despite discounting at a similar rate to other branches. LA Branch suffered the most dramatic decline — dropping 72% year-over-year and falling from the highest-performing store to the lowest. This warrants investigation: the revenue collapse is too large to be explained by discounting alone.<br/>
3. Zero-discount orders generate the majority of revenue
In both fiscal years, the 0% discount band consistently produced the most revenue and the most orders — by a significant margin.<br/>
Customers buying at full price account for nearly half of total revenue. The 50%+ discount tier generates almost nothing. This suggests discounting is not a meaningful driver of incremental sales volume — the business's strongest customers are not discount-dependent.<br/>
4. Watches dominate the product mix
Watches accounted for approximately $2.45M in FY24-25 — close to 60% of total revenue — with Jewelry a distant second at $986K and Bandlets third at $399K. Any discount strategy review needs to consider this category separately, as changes to watch pricing will have an outsized impact on overall store performance.<br/>
5. Discount depth and revenue have an inverse relationship at higher bands
Across the discount spectrum, revenue drops as discount depth increases beyond 20%. The 30% band generates more than the 15% band in order volume terms, but the net revenue contribution decreases as the discount eats into the transaction value. At 50% and above, the revenue contribution becomes negligible — suggesting these high-discount events are likely clearance or promotional outliers rather than a meaningful sales strategy.<br/>


### Tools Used
Google Sheets — SUMIF, COUNTIF, AVERAGEIF, SUMPRODUCT, AVERAGEIFS, COUNTIFS, QUERY
Conditional formatting for visual flagging of year-over-year changes
Grouped bar charts, column charts, and pie chart for visualisation


### Files
Store Sales Data.xlsx
Raw dataset — two fiscal year tabs plus blank Overview


Author
Manish Patel — Data Analyst
CompTIA Data+ Certified · SQL · Tableau · Power BI · Excel · Google Sheets

