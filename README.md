# SBI Executive Dashboard | Power BI

An interactive banking dashboard that brings revenue, profit, customers, loans, deposits, asset quality and state-wise performance together in one executive view.

> **Note:** The dataset is **simulated** for learning and portfolio purposes. It is not real State Bank of India data.

---

## Objective

Turn banking data into a clear, executive-level view that supports performance monitoring, highlights business opportunities and enables data-driven decisions.

## Questions the dashboard answers

- How are revenue and net profit trending over time?
- What is the balance between loans (advances) and deposits?
- Which states contribute most to total banking business?
- How is the loan portfolio distributed across categories?
- Which customer segments are the largest?
- How are Gross NPA, ROA and ROE performing?
- Where should strategic attention go to improve profitability, asset quality and customer retention?

---

## Project files

| File | Description |
|---|---|
| `SBI_Dataset.xlsx` | Main dataset with 4 sheets (see below) |
| `SBI_Fact_Monthly_State.csv` | Fact table as a CSV |
| `SBI_PowerBI_Wallpaper.png` / `.svg` | 1920×1080 canvas background (sidebar and header) |
| `SBI_PowerBI_Wallpaper_Banner.png` | Same wallpaper with the SBI building banner in the header |
| `SBI_Header_Banner.png` | Banner image on its own |
| `SBI_Executive_Dashboard.html` | Interactive web version of the dashboard |
| `SBI_Dashboard.pbix` | Power BI report (add your file here) |

## Dataset

| Sheet | Rows | Columns |
|---|---|---|
| `Fact_Monthly_State` | 540 (36 months × 15 states) | Date, Year, Month, State, Revenue_Cr, NetProfit_Cr, Customers_K, NewCustomers_K, Loans_Cr, Deposits_Cr, GrossNPA_Pct, ROA_Pct, ROE_Pct |
| `Loan_Portfolio` | 6 | Category, Share_Pct |
| `Product_Revenue` | 6 | Product, Revenue_Cr |
| `Customer_Segments` | 6 | Segment, Customers_Share_Pct |

Period covered: **January 2023 to December 2025**. Amounts are in ₹ crore (Cr) and customers in thousands (K).

---

## Tools and skills

Power BI · Power Query · DAX · Data Cleaning and Transformation · Data Modeling · KPI Development · Data Visualization · Business Intelligence · Financial and Banking Analytics

---

## Data model

A star model with one fact table and two helper tables:

```
DateTable[Date]  1 ───► *  Fact_Monthly_State[Date]
State[State]     1 ───► *  Fact_Monthly_State[State]
```

- `DateTable` is created with `CALENDAR()` and marked as a date table.
- `State` is created with `DISTINCT(Fact_Monthly_State[State])`.
- `Loan_Portfolio`, `Product_Revenue` and `Customer_Segments` are standalone lookup tables, so their visuals do not respond to the Year and State slicers.

## DAX measures

```DAX
Total Revenue   = SUM(Fact_Monthly_State[Revenue_Cr])
Net Profit      = SUM(Fact_Monthly_State[NetProfit_Cr])
Total Loans     = SUM(Fact_Monthly_State[Loans_Cr])
Total Deposits  = SUM(Fact_Monthly_State[Deposits_Cr])
Total Customers = SUM(Fact_Monthly_State[Customers_K]) / 1000
Gross NPA       = AVERAGE(Fact_Monthly_State[GrossNPA_Pct])
ROA             = AVERAGE(Fact_Monthly_State[ROA_Pct])
ROE             = AVERAGE(Fact_Monthly_State[ROE_Pct])
Total Business  = [Total Loans] + [Total Deposits]
Loan to Deposit % = DIVIDE([Total Loans], [Total Deposits])
```

---

## Dashboard layout (single page, 16:9)

- **Sidebar:** SBI logo, *Executive Dashboard* label, Year and State slicers
- **Header:** title and SBI banner
- **KPI cards:** Total Revenue, Customers, Loans, Deposits, Gross NPA, Net Profit, ROA, ROE
- **Visuals:**
  - Revenue and Net Profit trend (column and line chart)
  - Business mix: Deposits vs Loans (donut)
  - Top 5 States by Total Business (stacked bar, Top N filter)
  - Loan portfolio composition (donut)
  - Top 5 Products by revenue (bar, Top N filter)
  - Customer segment analysis (donut)
  - Geographic performance (table or filled map)
- **Key insights:** text summary of the main findings

### Colour palette

| Use | Hex |
|---|---|
| Primary blue | `#1D4F9C` |
| Accent cyan | `#00A7E1` |
| Highlight orange | `#F5A623` |
| Text navy | `#10294D` |
| Border | `#C9D9EE` |

---

## How to use

1. Open Power BI Desktop and choose **Get Data → Excel**. Load all 4 sheets from `SBI_Dataset.xlsx`.
2. In Power Query, confirm `Date` is a Date type and the numeric columns are Decimal. Click **Close & Apply**.
3. Create `DateTable` and `State` in Table view and link them in Model view.
4. Add the DAX measures above.
5. Set **Format → Canvas background → Image** to `SBI_PowerBI_Wallpaper_Banner.png` (Image fit: Fit, Transparency: 0%).
6. Build the cards, slicers and charts as described in the layout section.

---

## Key insights (sample)

- Revenue and net profit trend upward across the 36 months.
- The loan-to-deposit ratio leaves room to grow advances.
- Gross NPA improves gradually over the period.
- Uttar Pradesh, Maharashtra and Tamil Nadu are among the largest states by business.

## Future improvements

- Link the loan, product and segment tables to State and Date so every visual responds to filters
- Use weighted averages for ROA, ROE and Gross NPA
- Add pages for Loan and Credit Risk, Branch and Regional performance, and Customer Churn
- Add year-over-year growth measures to the KPI cards

---

## Feedback

Feedback and suggestions are welcome. Feel free to connect or message to discuss Power BI, dashboard development and data analytics projects.

`#PowerBI` `#BankingAnalytics` `#SBIDashboard` `#DataAnalytics` `#BusinessIntelligence` `#DataVisualization` `#DAX` `#PowerQuery` `#KPI`
