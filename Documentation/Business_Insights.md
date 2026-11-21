# Business Insights

All figures were calculated from `Data/VELT.csv` (2,000 AI-generated orders) and cross-checked with the dashboard. Money is in ₹ as shown on the dashboard. Because the data is synthetic, the insights illustrate the analysis and are not real business results. Insights describe patterns in the data; they do not prove cause.

## 1. Headline performance

| Metric | Value |
|--------|------:|
| Total revenue | ₹303.56M |
| Total profit | ₹47.92M (15.8% of revenue) |
| Return rate | 26.4% (528 of 2,000 orders) |
| Return loss (direct return cost) | ₹5.86M (1.9% of revenue) |
| Delay rate | 24.0% (480 orders) |

**Interpretation:** more than one in four orders comes back. The direct return cost is small compared with revenue, but see section 6: returned orders are where profit is lost.

## 2. Return reasons

| Reason | Returned orders | Share of returns |
|--------|----------------:|-----------------:|
| Size Issue | 252 | 47.7% |
| Not as Expected | 147 | 27.8% |
| Quality Issue | 129 | 24.4% |

- Size Issue is the single largest driver in every category (Shoes 90, Clothing 83, Handbag 79) and for both suppliers.
- "Not as Expected" and "Quality Issue" together account for 52.3% of returns. They point to product description and quality control rather than sizing.

## 3. Category analysis

| Category | Orders | Return rate | Return loss | Share of return loss | Share of revenue | Profit margin |
|----------|-------:|------------:|------------:|---------------------:|-----------------:|--------------:|
| Shoes | 687 | **28.2%** (highest) | ₹1.33M | 22.7% | 21.4% | 13.6% |
| Clothing | 656 | 25.6% | ₹0.76M | 13.0% | 13.2% | 16.1% |
| Handbag | 657 | 25.3% | **₹3.77M** (highest) | 64.3% | 65.4% | 16.4% |

- **Shoes have the highest return rate**, and the lowest profit margin.
- **Handbags cause most of the return loss** even though their return rate is the lowest. The reason is price: the average Handbag order is about ₹302K, versus ₹94K for Shoes and ₹61K for Clothing. The average return cost per returned Handbag is ₹22.7K, versus ₹6.9K (Shoes) and ₹4.5K (Clothing).
- All of the top 10 highest-cost returns are Handbags.
- Note: the dashboard's "Category Risk Insight" card shows "Handbags – 28.2%". 28.2% is the Shoes return rate (see `KPI_Definitions.md`).

## 4. Customer segment analysis

| Segment | Orders | Return rate | Return loss | Revenue | Profit margin |
|---------|-------:|------------:|------------:|--------:|--------------:|
| Regular | 1,419 | **30.4%** | ₹4.76M (81% of total) | ₹215.8M | 11.8% |
| VIP | 581 | 16.7% | ₹1.11M (19%) | ₹87.8M | 25.5% |

- Regular customers are 71% of orders but 82% of returns and 81% of return loss.
- Regular customers return more for every reason: Size Issue 14.9% of Regular orders vs 6.9% for VIP.
- VIP orders earn more than double the profit margin of Regular orders, with a similar average order value (₹151K vs ₹152K).

## 5. Supplier analysis

| Supplier | Orders | Delay rate | Return rate | Return loss | Shipping cost (% of price) |
|----------|-------:|-----------:|------------:|------------:|---------------------------:|
| China | 784 | **30.6%** | 26.8% | ₹2.27M | 5% |
| Italy | 1,216 | 19.7% | 26.2% | ₹3.59M | 8% |

- China has a much higher delay rate (30.6% vs 19.7%).
- Return rates are almost the same for both suppliers (26.8% vs 26.2%), so supplier alone does not explain returns.
- Delayed orders are returned only slightly more often than on-time orders (27.3% vs 26.1%). In this data, delay is not a strong driver of returns.
- By category, Clothing from China returns most (30.0%) and Clothing from Italy least (22.9%); Shoes are higher from Italy (29.5% vs 26.4%). These groups are smaller than the full dataset, so treat the differences with care.

## 6. Profit impact of returns

- All 528 returned orders have **negative profit** (total −₹49.9M). The 1,472 non-returned orders earn +₹97.8M.
- The "Return Loss" KPI (₹5.86M) counts only the direct return cost. The profit lost on returned orders is much larger, so the KPI probably understates the full impact of returns. The source does not explain how `Profit` is calculated, so this should be confirmed before quoting it as a business fact.
- Handbag returns account for −₹32.0M of that negative profit, Shoes −₹11.5M, Clothing −₹6.4M.

## 7. Region, season and demand

| Group | Return rate |
|-------|------------:|
| USA | **28.4%** |
| Europe | 26.0% |
| Asia | 24.9% |
| Summer | **29.2%** |
| Winter | 25.5% |
| Spring | 23.5% |
| High demand | 28.5% |
| Low demand | 27.7% |
| Medium demand | 23.8% |

- Summer has the highest return rate (29.2%) and the highest return loss (₹2.68M).
- The USA has the highest return rate among regions.
- There is no date column, so month-by-month or year-over-year trends cannot be analysed. The only time view available is by `Season`, and Autumn does not appear in the data.

## 8. Recommendations

These follow from the patterns above. They are suggestions for discussion, not tested actions.

1. **Fix sizing first.** Size Issue causes 47.7% of returns in every category. Improve size charts, fit guidance and size-related product information, starting with Shoes (28.2% return rate).
2. **Protect Handbag returns.** Handbags drive 64% of return loss and all of the 10 costliest returns. Add pre-shipment quality checks and accurate photos and descriptions for high-value items.
3. **Improve product information.** "Not as Expected" plus "Quality Issue" make up 52.3% of returns, which suggests listing accuracy and quality control need attention.
4. **Target Regular customers.** They return 30.4% of orders against 16.7% for VIP. Test sizing help, clearer return policies or loyalty benefits aimed at this group.
5. **Review China delivery performance.** A 30.6% delay rate is well above Italy's 19.7%. Set delivery targets with the supplier and track them.
6. **Prepare for summer.** Summer has the highest return rate (29.2%). Review sizing and stock plans before the season.
7. **Add a date field and return-cost breakdown** (refund, shipping, handling) to future data so trends and the true cost of returns can be measured.
