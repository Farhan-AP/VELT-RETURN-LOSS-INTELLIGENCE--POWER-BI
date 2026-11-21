# KPI Definitions

All "Actual value" figures below were **recalculated from `Data/VELT.csv`** and compared with the dashboard screenshot (`Screenshots/Dashboard_Overview.jpg`). The "Calculation" column describes the logic that reproduces the dashboard value. The original DAX could not be read from the PBIX, so these are not the author's DAX text (see `DAX/Measures.md`).

## Headline KPIs (cards)

| KPI | Business meaning | Calculation | Actual value (raw data) | Dashboard | Match |
|-----|------------------|-------------|------------------------:|----------:|:-----:|
| Total Revenue | Total order value across all orders | Sum of `Price` | ₹303,562,406 | ₹303.56M | ✔ |
| Total Profit | Net profit recorded across all orders (returns already reduce it because returned orders have negative profit) | Sum of `Profit` | ₹47,915,608 | ₹47.92M | ✔ |
| Return Rate | Share of orders that were returned | Returned orders ÷ total orders = 528 ÷ 2,000 | 26.4% | 26.4% | ✔ |
| Return Loss | Direct cost caused by returns | Sum of `Return_Cost` | ₹5,863,110 | ₹5.86M | ✔ |
| Delay Rate | Share of orders delivered late | Orders with `Delay = Yes` ÷ total orders = 480 ÷ 2,000 | 24.0% | 24.0% | ✔ |

## Chart KPIs

| Visual | Measure | Values from raw data | Dashboard | Match |
|--------|---------|----------------------|-----------|:-----:|
| Return Rate by Category | Return Rate | Shoes 28.2% (194/687), Clothing 25.6% (168/656), Handbag 25.3% (166/657) | 28.2 / 25.6 / 25.3% | ✔ |
| Return Loss by Category | Return loss | Handbag ₹3.77M, Shoes ₹1.33M, Clothing ₹0.76M | 3.8M / 1.3M / 0.8M | ✔ |
| Return Reason by Category | Returned Orders | Shoes 55 / 49 / 90, Clothing 49 / 36 / 83, Handbag 43 / 44 / 79 (Not as Expected / Quality / Size) | same | ✔ |
| Supplier Delay Rate | Delay Rate | China 30.6% (240/784), Italy 19.7% (240/1,216) | 30.6% / 19.7% | ✔ |
| Why Customers Return | Returned Orders | Size Issue 252 (47.7%), Not as Expected 147 (27.8%), Quality Issue 129 (24.4%), total 528 | same | ✔ |
| High-Risk Return Orders | Return_Cost, Profit | Top 10 orders by `Return_Cost`: total ₹451,864 cost and −₹3,002,338 profit | same totals | ✔ |

## Executive Insight cards (text measures)

| Card | Dashboard text | Check against raw data | Match |
|------|----------------|------------------------|:-----:|
| Return Driver Insight | "47.7% – Size Issues" | Size Issue is 47.7% of returns | ✔ |
| Category Risk Insight | "Handbags – 28.2%" | **28.2% is the Shoes return rate.** Handbag return rate is 25.3%. Handbags have the highest *return loss* (₹3.77M, 64% of the total) | ✘ see below |
| Customer Risk Insight | "Regular – 30% vs VIP – 17%" | Regular 30.4%, VIP 16.7% return rate | ✔ |
| Supplier Risk Insight | "China – 30.6% vs Italy – 19.7%" | These are **delay rates**. Return rates by supplier are 26.8% (China) and 26.2% (Italy) | ✔ for delay, but the label says "Risk" |

### Issue to resolve in the dashboard

The **Category Risk Insight** card pairs "Handbags" with "28.2%". The raw data shows 28.2% belongs to **Shoes** (highest return *rate*), while **Handbags** carry the highest return *loss*. Check the measure logic in Power BI Desktop and either change the text to "Shoes – 28.2%" (highest return rate) or "Handbags – ₹3.8M" (highest return loss). The measure expression could not be read here, so the cause could not be confirmed.

## Dashboard filters

The four slicers (Supplier, Category, Region, Customer Segment) change all KPI values. Every figure above is for the **unfiltered** dashboard (all slicers set to "All").
