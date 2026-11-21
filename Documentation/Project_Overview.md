# Project Overview

## Project
**VELT Retail – Return Loss Intelligence Dashboard** (Power BI)

## Business context
VELT sells Clothing, Shoes and Handbags through two suppliers (China and Italy) to Regular and VIP customers in Asia, Europe and the USA. Returns and late deliveries reduce profit and hurt the customer experience. The dashboard gives managers one page that shows how big the return problem is, where it comes from and which orders cost the most.

## Business problem
More than one in four orders is returned. Management needs to know:
- How large are returns and return losses overall?
- Which categories, customer segments and suppliers are most affected?
- Why do customers return products?
- Which individual orders cause the largest losses?

## Objectives
1. Track the main KPIs: revenue, profit, return rate, return loss and delay rate.
2. Compare returns and return loss by product category.
3. Identify the main return reasons.
4. Compare supplier delay performance.
5. List the highest-cost return orders for follow-up.
6. Let users filter by Supplier, Category, Region and Customer Segment.

## Data
- Source file: `Data/VELT.csv`: 2,000 orders, 15 columns, no missing values, no duplicates.
- See `Data/Data_Dictionary.md` and `Documentation/Data_Cleaning.md`.
- The dataset was generated with AI specifically for this project and was already prepared, so it is a single file with no raw/processed split. It describes no real company. The CSV has no currency field; the dashboard shows ₹.

## Dashboard (what the PBIX contains)
This was read from the report layer of the PBIX. The data model could not be opened (see `DAX/Measures.md`).

| Item | Detail |
|------|--------|
| Pages | 1 page (1280 × 720), titled "EXECUTIVE ANALYTICS – RETURN LOSS INTELLIGENCE", dated "SEPTEMBER 2026" |
| Data model | 1 table (`VELT`), no relationships |
| KPI cards | Total Revenue, Total Profit, Return Rate, Return Loss, Delay Rate |
| Charts | Return Rate by Category (column), Return Loss by Category (bar), Return Reason by Category (stacked bar), Supplier Delay Rate (column), Why Customers Return (donut) |
| Table | High-Risk Return Orders: Top 10 orders by Return_Cost, showing Order_ID, Category, Supplier, Return_Reason, Return_Cost, Profit |
| Insight cards | Return Driver, Category Risk, Customer Risk, Supplier Risk |
| Slicers | Supplier, Category, Region, Customer Segment (dropdowns) |
| Design | Black panels with red (#E30613) and white, VELT logo top-left, custom theme "VELT THEME" on a Fluent 2 base theme, faded image behind the panels |

## Validation
Every KPI and chart value shown in the screenshot was recalculated from the CSV and matched (see `Documentation/KPI_Definitions.md`). One text card, "Category Risk Insight", does not match the data (Handbags paired with the Shoes return rate of 28.2%).

## Workflow
1. AI-generated, analysis-ready CSV loaded into Power BI as a single table, `VELT` (no Power Query transformations).
2. DAX measures created for the KPIs and insight cards.
3. One executive dashboard page designed with cards, charts, a Top 10 table and slicers.
4. Documentation and repository prepared for GitHub.

The workflow was confirmed by the project author.
