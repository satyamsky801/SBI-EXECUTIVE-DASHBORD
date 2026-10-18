# SBI Executive Dashboard | Power BI



!\[SBI Executive Dashboard](dashboard.png)



An interactive banking dashboard that brings revenue, profit, customers, loans, deposits, asset quality and state-wise performance together in one executive view.

> \*\*Note:\*\* The dataset is \*\*simulated\*\* for learning and portfolio purposes. It is not real State Bank of India data.

\---

## Objective

Turn banking data into a clear, executive-level view that supports performance monitoring, highlights business opportunities and enables data-driven decisions.

## Questions the dashboard answers

* How are revenue and net profit trending over time?
* What is the balance between loans (advances) and deposits?
* Which states contribute most to total banking business?
* How is the loan portfolio distributed across categories?
* Which customer segments are the largest?
* How are Gross NPA, ROA and ROE performing?
* Where should strategic attention go to improve profitability, asset quality and customer retention?

\---

## Project files

|File|Description|
|-|-|
|`SBI\_Dataset.xlsx`|Main dataset with 4 sheets (see below)|
|`SBI\_Fact\_Monthly\_State.csv`|Fact table as a CSV|
|`SBI\_PowerBI\_Wallpaper.png` / `.svg`|1920×1080 canvas background (sidebar and header)|
|`SBI\_PowerBI\_Wallpaper\_Banner.png`|Same wallpaper with the SBI building banner in the header|
|`SBI\_Header\_Banner.png`|Banner image on its own|
|`SBI\_Executive\_Dashboard.html`|Interactive web version of the dashboard|
|`SBI\_Dashboard.pbix`|Power BI report (add your file here)|

## Dataset

|Sheet|Rows|Columns|
|-|-|-|
|`Fact\_Monthly\_State`|540 (36 months × 15 states)|Date, Year, Month, State, Revenue\_Cr, NetProfit\_Cr, Customers\_K, NewCustomers\_K, Loans\_Cr, Deposits\_Cr, GrossNPA\_Pct, ROA\_Pct, ROE\_Pct|
|`Loan\_Portfolio`|6|Category, Share\_Pct|
|`Product\_Revenue`|6|Product, Revenue\_Cr|
|`Customer\_Segments`|6|Segment, Customers\_Share\_Pct|

Period covered: **January 2023 to December 2025**. Amounts are in ₹ crore (Cr) and customers in thousands (K).

\---

## Tools and skills

Power BI · Power Query · DAX · Data Cleaning and Transformation · Data Modeling · KPI Development · Data Visualization · Business Intelligence · Financial and Banking Analytics

\---

## Data model

A star model with one fact table and two helper tables:

```
DateTable\[Date]  1 ───► \*  Fact\_Monthly\_State\[Date]
State\[State]     1 ───► \*  Fact\_Monthly\_State\[State]
```

* `DateTable` is created with `CALENDAR()` and marked as a date table.
* `State` is created with `DISTINCT(Fact\_Monthly\_State\[State])`.
* `Loan\_Portfolio`, `Product\_Revenue` and `Customer\_Segments` are standalone lookup tables, so their visuals do not respond to the Year and State slicers.

## DAX measures

```DAX
Total Revenue   = SUM(Fact\_Monthly\_State\[Revenue\_Cr])
Net Profit      = SUM(Fact\_Monthly\_State\[NetProfit\_Cr])
Total Loans     = SUM(Fact\_Monthly\_State\[Loans\_Cr])
Total Deposits  = SUM(Fact\_Monthly\_State\[Deposits\_Cr])
Total Customers = SUM(Fact\_Monthly\_State\[Customers\_K]) / 1000
Gross NPA       = AVERAGE(Fact\_Monthly\_State\[GrossNPA\_Pct])
ROA             = AVERAGE(Fact\_Monthly\_State\[ROA\_Pct])
ROE             = AVERAGE(Fact\_Monthly\_State\[ROE\_Pct])
Total Business  = \[Total Loans] + \[Total Deposits]
Loan to Deposit % = DIVIDE(\[Total Loans], \[Total Deposits])
```

\---

## Dashboard layout (single page, 16:9)

* **Sidebar:** SBI logo, *Executive Dashboard* label, Year and State slicers
* **Header:** title and SBI banner
* **KPI cards:** Total Revenue, Customers, Loans, Deposits, Gross NPA, Net Profit, ROA, ROE
* **Visuals:**

  * Revenue and Net Profit trend (column and line chart)
  * Business mix: Deposits vs Loans (donut)
  * Top 5 States by Total Business (stacked bar, Top N filter)
  * Loan portfolio composition (donut)
  * Top 5 Products by revenue (bar, Top N filter)
  * Customer segment analysis (donut)
  * Geographic performance (table or filled map)
* **Key insights:** text summary of the main findings

### Colour palette

|Use|Hex|
|-|-|
|Primary blue|`#1D4F9C`|
|Accent cyan|`#00A7E1`|
|Highlight orange|`#F5A623`|
|Text navy|`#10294D`|
|Border|`#C9D9EE`|

\---

## How to use

1. Open Power BI Desktop and choose **Get Data → Excel**. Load all 4 sheets from `SBI\_Dataset.xlsx`.
2. In Power Query, confirm `Date` is a Date type and the numeric columns are Decimal. Click **Close \& Apply**.
3. Create `DateTable` and `State` in Table view and link them in Model view.
4. Add the DAX measures above.
5. Set **Format → Canvas background → Image** to `SBI\_PowerBI\_Wallpaper\_Banner.png` (Image fit: Fit, Transparency: 0%).
6. Build the cards, slicers and charts as described in the layout section.

\---

## Key insights (sample)

* Revenue and net profit trend upward across the 36 months.
* The loan-to-deposit ratio leaves room to grow advances.
* Gross NPA improves gradually over the period.
* Uttar Pradesh, Maharashtra and Tamil Nadu are among the largest states by business.

## Future improvements

* Link the loan, product and segment tables to State and Date so every visual responds to filters
* Use weighted averages for ROA, ROE and Gross NPA
* Add pages for Loan and Credit Risk, Branch and Regional performance, and Customer Churn
* Add year-over-year growth measures to the KPI cards

\---

## Feedback

Feedback and suggestions are welcome. Feel free to connect or message to discuss Power BI, dashboard development and data analytics projects.

`#PowerBI` `#BankingAnalytics` `#SBIDashboard` `#DataAnalytics` `#BusinessIntelligence` `#DataVisualization` `#DAX` `#PowerQuery` `#KPI`

