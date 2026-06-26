# Executive Sales Tableau Dashboard Project

## Business Problem Summary

Retail leadership needs a decision-ready dashboard to monitor sales performance, profitability, customer segments, category performance, shipping performance, discount impact, and return patterns. The dashboard is designed to help leaders identify where to scale growth, where margin is leaking, and where operational risks require follow-up.

## Dataset Description

The dataset is stored at `data/dashboard_sales_data.xlsx`. It contains **4,200 records** from **2024-01-01** to **2025-12-31**. The workbook includes a main data sheet and a data dictionary sheet.

### Field Inspection

| Field Group | Fields |
|---|---|
| Date fields | order_date, ship_date |
| Geographic fields | region, state, city |
| Categorical fields | customer_segment, region, state, city, category, sub_category, product_name, ship_mode, campaign_channel |
| Numerical measures | sales, quantity, discount, profit, delivery_days, customer_rating |
| Binary / flag fields | return_flag |

## Tableau Workbook Description

The required packaged workbook is saved as `tableau/executive_dashboard.twbx`. It packages the Tableau workbook XML with the source Excel data and dashboard screenshot assets. The workbook is structured around one executive dashboard plus the supporting sheet concepts requested in the assignment.

## Calculated Fields Created

| Calculated Field | Logic | Purpose |
|---|---|---|
| Profit Margin | `SUM([profit]) / SUM([sales])` | Shows profitability efficiency after revenue scale is considered. |
| Cost | `SUM([sales]) - SUM([profit])` | Approximates cost base behind sales. |
| Average Order Value | `SUM([sales]) / COUNTD([order_id])` | Measures sales value per order. |
| Return Rate | `SUM([return_flag]) / COUNTD([order_id])` | Measures percentage of orders returned. |
| Shipping Delay Bucket | `IF [delivery_days] <= 2 THEN "0-2 Days" ELSEIF [delivery_days] <= 5 THEN "3-5 Days" ELSE "6+ Days" END` | Creates operational delivery buckets. |
| Discount Band | `IF [discount] = 0 THEN "0%" ELSEIF [discount] <= 0.10 THEN "1-10%" ELSEIF [discount] <= 0.25 THEN "11-25%" ELSE ">25%" END` | Groups discounts for margin analysis. |
| Profit Risk Flag | `IF SUM([profit]) < 0 THEN "Loss" ELSE "Profitable" END` | Highlights loss-making slices. |

## Dashboard Components

- KPI cards: Total Sales, Total Profit, Profit Margin, Return Rate, Average Order Value, Average Delivery Days.
- Sales Trend View: monthly sales line chart.
- Regional Performance View: sales and profit by region.
- Category Profitability View: sub-category profit/loss bar chart.
- Customer Segment View: segment margin and return-risk comparison.
- Shipping Performance View: average delivery days by shipping mode.
- Discount vs Profit View: discount band vs profit margin with order volume context.
- Return Analysis View: return rates by category and region.

## Filters and Interactions Used

Suggested/implemented filter dimensions: Region, Category, Customer Segment, Date, Ship Mode, and Campaign Channel. The dashboard story uses a region-selection action pattern where selecting a region filters the category and KPI views. The screenshot `screenshots/filter_interaction_view.png` shows an interaction example with **South** selected.

## Key Business Insights

- Total sales: **₹217.02M**; total profit: **₹33.31M**; profit margin: **15.3%**.
- Highest sales region: **South** with **₹64.69M** sales.
- Weakest margin region: **West** with **15.1%** margin.
- Highest-profit category: **Technology** with **₹28.04M** profit.
- Largest sub-category profit drag: **Paper** with **₹0.32M** profit.
- Highest-return category: **Furniture** with **7.7%** return rate.
- Slowest ship mode: **Standard Class** with **4.7** average delivery days.
- Lowest-margin discount band: **>25%** with **6.5%** margin.

## Dashboard Story Summary

The dashboard tells a business story from overall performance to diagnostic risks. It starts with KPIs, then shows sales momentum, region/category contribution, segment risk, shipping delays, discount impact, and returns. The recommended leadership focus is to scale profitable categories and regions while reducing discount leakage, return concentration, and fulfillment delays.

## Assumptions and Limitations

- `return_flag` is treated as a binary order-level return indicator.
- `delivery_days` is assumed to represent the difference between order date and ship date or a comparable fulfillment duration.
- Profit margin is calculated as total profit divided by total sales.
- Average order value is calculated as total sales divided by distinct order count.
- The dataset does not include marketing spend, product cost breakdown, inventory stockout data, or customer lifetime value.
- Tableau Desktop is not available in this execution environment, so the packaged workbook is generated as Tableau XML and zipped with local data; visual validation is done through generated dashboard screenshots.

## Screenshots Included

- `screenshots/full_dashboard.png`
- `screenshots/sales_trend_view.png`
- `screenshots/regional_performance_view.png`
- `screenshots/category_profitability_view.png`
- `screenshots/filter_interaction_view.png`

## Repository Structure

```
tableau_dashboard_project/
├── data/
│   └── dashboard_sales_data.xlsx
├── tableau/
│   ├── executive_dashboard.twbx
│   └── executive_dashboard.twb
├── screenshots/
│   ├── full_dashboard.png
│   ├── sales_trend_view.png
│   ├── regional_performance_view.png
│   ├── category_profitability_view.png
│   └── filter_interaction_view.png
├── outputs/
│   ├── business_insights.md
│   ├── dashboard_story.md
│   ├── chart_selection_justification.md
│   └── supporting summary CSV files
└── README.md
```
