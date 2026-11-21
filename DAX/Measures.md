# DAX Measures

## Extraction status — please read

**The original DAX expressions could not be extracted.** The PBIX stores its data model (tables, relationships, measures, Power Query steps) in a compressed binary file (`DataModel`) that could not be opened with the tools available for this review. The project author confirmed that DAX measures were the only method used to calculate the dashboard values.

What *could* be read is the **report layer**, which lists which measures each visual uses. From it, the following was confirmed:

- The model has **one table**, named `VELT`, with the same columns as `Data/VELT.csv`. No relationships are used (single table).
- The report has **one page** (internally named "Page 2", 1280 × 720) with 10 measures in use.

The measure **names** below are real. The **DAX code** in Part 2 is a **suggested example** written to reproduce the dashboard values. It is **not** the original code from the PBIX. Check it against your measures in Power BI Desktop before publishing, and replace it with your own code if it differs.

---

## Part 1 — Measures used in the report (names read from the PBIX)

| Measure | Used in | What it shows |
|---------|---------|---------------|
| Total Revenue | KPI card | Total order value |
| Total Profit | KPI card | Total profit |
| Return Rate | KPI card; Return Rate by Category chart | % of orders returned |
| Return loss | KPI card; Return Loss by Category chart | Total cost of returns |
| Delay Rate | KPI card; Supplier Delay Rate chart | % of orders delayed |
| Returned Orders | Return Reason by Category chart; donut chart | Number of returned orders |
| Return Driver Insight | Executive Insight card | Text: top return reason |
| Category Risk Insight | Executive Insight card | Text: category risk |
| Customer Risk Insight | Executive Insight card | Text: Regular vs VIP return rate |
| Supplier Risk Insight | Executive Insight card | Text: China vs Italy delay rate |

Columns used directly (not as measures): `Order_ID`, `Category`, `Supplier`, `Return_Reason`, `Return_Cost` and `Profit` (in the High-Risk table, summed), plus the slicer columns `Supplier`, `Category`, `Region`, `Customer_Segment`.

---

## Part 2 — Suggested example DAX (NOT the original code)

Each example gives the same result as the dashboard when checked against the raw CSV.

### Total Revenue
```DAX
Total Revenue = SUM ( VELT[Price] )
```
Adds up the price of all orders. Raw-data check: ₹303,562,406 (dashboard ₹303.56M).

### Total Profit
```DAX
Total Profit = SUM ( VELT[Profit] )
```
Adds up the profit of all orders. Raw-data check: ₹47,915,608 (dashboard ₹47.92M).

### Returned Orders
```DAX
Returned Orders =
CALCULATE ( COUNTROWS ( VELT ), VELT[Return_Status] = "Yes" )
```
Counts orders that were returned. Raw-data check: 528.

### Return Rate
```DAX
Return Rate =
DIVIDE ( [Returned Orders], COUNTROWS ( VELT ) )
```
Returned orders divided by all orders. Raw-data check: 26.4%.

### Return Loss
```DAX
Return Loss = SUM ( VELT[Return_Cost] )
```
Adds up the cost caused by returns. Raw-data check: ₹5,863,110 (dashboard ₹5.86M). The report's measure is named `Return loss` (lower-case "l").

### Delay Rate
```DAX
Delay Rate =
DIVIDE (
    CALCULATE ( COUNTROWS ( VELT ), VELT[Delay] = "Yes" ),
    COUNTROWS ( VELT )
)
```
Delayed orders divided by all orders. Raw-data check: 24.0%.

### Text insight measures
The logic of the four "Insight" measures (Return Driver, Category Risk, Customer Risk, Supplier Risk) could not be read, so no code is suggested for them. Their displayed text is documented in `Documentation/KPI_Definitions.md`, including a mismatch found in the Category Risk Insight card.

---

## How to extract the real DAX yourself

1. Open `PowerBI/VELT_Retail_Return_Loss_Intelligence.pbix` in Power BI Desktop.
2. Go to **Model view** or the **Data pane**, click each measure and copy the formula from the formula bar.
3. Replace Part 2 of this file with the copied formulas.
4. Optional: use **Tabular Editor** or **DAX Studio** (free tools) to export all measures at once.
