# VELT Retail – Return Loss Intelligence Dashboard

A single-page Power BI executive dashboard that analyses product returns, return losses and supplier delays for a retail business selling Clothing, Shoes and Handbags.

![Dashboard overview](Screenshots/Dashboard_Overview.jpg) 

## Project Overview
VELT sells through two suppliers (China and Italy) to Regular and VIP customers in Asia, Europe and the USA. This project turns a 2,000-order dataset into one dashboard that shows how large the return problem is, why customers return products and which orders and categories cost the most.

## Business Problem
Returns and late deliveries reduce profit. In this dataset **26.4% of orders are returned**. Management needs to see where returns come from, what drives them and where the biggest losses are.

## Project Objectives
- Track revenue, profit, return rate, return loss and delay rate.
- Compare returns and return loss by product category.
- Identify the main return reasons.
- Compare supplier delay performance.
- List the highest-cost return orders.
- Allow filtering by Supplier, Category, Region and Customer Segment.

## Dataset
- **File:** [`Data/VELT.csv`](Data/VELT.csv): 2,000 orders × 15 columns
- **Columns:** Order_ID, Category, Price, Customer_Segment, Region, Season, Demand_Level, Supplier, Delay, Shipping_Time, Shipping_Cost, Return_Status, Return_Reason, Return_Cost, Profit
- **Quality:** no missing values, no duplicate rows, no duplicate Order_IDs
- **Synthetic data:** the dataset was generated with AI specifically for this project, in an already prepared form. It does not describe a real company or real customers, and contains no personal data (no customer names or contact details)
- Full column descriptions: [Data Dictionary](Data/Data_Dictionary.md)

## Tools and Technologies
- Power BI Desktop (dashboard, measures)
- DAX (measures; see the note on DAX below)
- CSV source data
- Python / pandas, used only to verify the dashboard figures against the raw data
- GitHub for the portfolio repository

## Data Preparation
The dataset was AI-generated for this project and was already prepared, so there is no separate raw/processed split. Checks confirmed 0 missing values, 0 duplicates and consistent category labels, so no cleaning was needed. The file is kept unchanged. No Power Query transformations were used; all dashboard values are calculated with DAX measures. Details: [Data Cleaning](Documentation/Data_Cleaning.md).

## Dashboard
One page, "Executive Analytics – Return Loss Intelligence", containing:
- 5 KPI cards
- 5 charts (return rate, return loss, return reason by category, supplier delay rate, return reasons donut)
- A Top 10 "High-Risk Return Orders" table
- 4 executive insight cards
- 4 dropdown slicers (Supplier, Category, Region, Customer Segment)

## Key KPIs
Values below were recalculated from the raw data and match the dashboard.

| KPI | Value |
|-----|------:|
| Total Revenue | ₹303.56M |
| Total Profit | ₹47.92M |
| Return Rate | 26.4% |
| Return Loss | ₹5.86M |
| Delay Rate | 24.0% |

Definitions and checks: [KPI Definitions](Documentation/KPI_Definitions.md)

## Key Business Insights
- **Size Issue is the top return reason:** 252 of 528 returns (47.7%), in every category.
- **Shoes have the highest return rate** (28.2%); **Handbags cause the highest return loss** (₹3.77M, 64% of the total) because of their high price.
- **Regular customers return far more than VIP:** 30.4% vs 16.7%, and account for 81% of return loss.
- **China has a much higher delay rate than Italy:** 30.6% vs 19.7%, while return rates are almost equal (26.8% vs 26.2%).
- **Every returned order has negative profit** (−₹49.9M in total), so the return cost KPI alone understates the impact of returns.

More detail: [Business Insights](Documentation/Business_Insights.md)

## Business Recommendations
1. Improve size guidance and size charts, starting with Shoes.
2. Add quality checks and accurate product information for high-value Handbags.
3. Target Regular customers with sizing help and clearer return policies.
4. Agree delivery targets with the China supplier.
5. Prepare for Summer, the season with the highest return rate (29.2%).

## Project Workflow
1. Load the raw CSV into Power BI.
2. Create measures for the KPIs and insight cards.
3. Design the executive dashboard page.
4. Validate dashboard figures against the raw data.
5. Document the project for GitHub.

## Repository Structure
```
VELT-Retail-Return-Loss-Intelligence/
├── README.md
├── .gitignore
├── Data/
│   ├── VELT.csv
│   └── Data_Dictionary.md
├── PowerBI/
│   └── VELT_Retail_Return_Loss_Intelligence.pbix
├── Screenshots/
│   └── Dashboard_Overview.jpg
├── Documentation/
│   ├── Project_Overview.md
│   ├── Data_Cleaning.md
│   ├── Business_Insights.md
│   └── KPI_Definitions.md
└── DAX/
    └── Measures.md
```

## How to Open and Use the Project
1. Download or clone this repository.
2. Open `PowerBI/VELT_Retail_Return_Loss_Intelligence.pbix` in **Power BI Desktop** (a recent version is needed because the report uses the newer report format).
3. Use the dropdown slicers (Supplier, Category, Region, Customer Segment) to filter the page.
4. The source data is in `Data/VELT.csv`. If Power BI asks for the data location, point it to this file.

## Limitations
- The DAX measures could not be extracted from the PBIX, so [`DAX/Measures.md`](DAX/Measures.md) lists the real measure names and *suggested example* code, not the original formulas.
- The dataset has no date column, so only seasonal comparisons are possible, not monthly trends.
- The data is synthetic (AI-generated), so the findings illustrate the analysis method and are not real business results. The currency is not stated in the data; the dashboard uses ₹.
- The "Category Risk Insight" card pairs "Handbags" with 28.2%, which is the Shoes return rate (see [KPI Definitions](Documentation/KPI_Definitions.md)).

## Acknowledgements
Dashboard, analysis and documentation by MUHAMMED FARHAN ASHRAF. Dataset generated with AI for this project.
