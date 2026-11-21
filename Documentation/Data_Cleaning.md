# Data Cleaning and Data Quality

This document records what was **checked** in the dataset and what is **known** about preparation. It does not claim any cleaning step that cannot be shown.

## Data origin

The dataset was **generated with AI specifically for this project** (stated by the project author). It was created in an analysis-ready form, so it is already processed and no further cleaning was needed. The author also confirmed that **only DAX measures** were used to produce the values shown in the visuals, with no Power Query transformations. The PBIX data model could not be opened during this review, so this is based on the author's statement and the checks below, not on inspecting the model.

## Data quality checks on `Data/VELT.csv`

| Check | Result |
|-------|--------|
| Rows × columns | 2,000 × 15 |
| Missing values (all columns) | **0** |
| Fully duplicated rows | **0** |
| Duplicate `Order_ID` values | **0** (IDs run `ORD0` to `ORD1999`, no gaps) |
| Leading or trailing spaces in text columns | **0** |
| Inconsistent spelling or casing in categories | None found. Each categorical column has a small, clean set of values |
| Return logic | Consistent: `Return_Status = Yes` ⇔ `Return_Reason` ≠ `No Return` ⇔ `Return_Cost` > 0 (528 rows) |
| Negative values | Only in `Profit` (528 rows, all returned orders). No negative prices, costs or times |
| Zero values | `Return_Cost` = 0 for the 1,472 non-returned orders. This is expected, not an error |

### Outliers (1.5 × IQR rule)

| Column | Rows flagged | Comment |
|--------|-------------:|---------|
| `Price` | 153 | Mostly high-priced Handbag orders. Handbag prices (100,001 – 499,199) are naturally higher than Clothing and Shoes |
| `Shipping_Cost` | 186 | Follows price because shipping is a fixed % of price |
| `Return_Cost` | 314 | Flagged because 74% of rows are 0, which distorts the IQR. These are real returned orders |
| `Profit` | 221 | Large negative profits on returned orders |

These values are genuine business values, not entry errors, so **no rows were removed or changed**.

## Steps performed on the data

| Step | Status |
|------|--------|
| Dataset preserved unchanged | Yes. `Data/VELT.csv` is a byte-for-byte copy of the file provided |
| Missing-value handling | Not needed (0 missing) |
| Duplicate handling | Not needed (0 duplicates) |
| Removal of outliers | Not performed |
| Processed / cleaned dataset | **Not created.** The provided dataset was already prepared, so there is a single data file |
| Power Query transformations in Power BI | None, per the project author. Values were produced with DAX measures only |

## Report-level logic found in the PBIX (readable part)

These items come from the report layer of the PBIX, which can be read:

- The report has **one table** in its data model, named `VELT`, which matches the columns of the raw CSV.
- The "High-Risk Return Orders" table shows the **Top 10 `Return_Cost`** orders (a Top N visual filter).
- Four dropdown slicers filter the page: Supplier, Category, Region, Customer_Segment.

## Feature creation

No new columns were found in the report layer. Whether calculated columns exist in the data model could not be checked. The dashboard uses the following **measures** (names read from the report): Total Revenue, Total Profit, Return Rate, Return loss, Delay Rate, Returned Orders, Return Driver Insight, Category Risk Insight, Customer Risk Insight and Supplier Risk Insight. See `DAX/Measures.md`.

## Observation about the data

The values follow very regular rules (for example, shipping cost is exactly 5% or 8% of price depending on supplier). This is expected because the dataset is AI-generated (every returned order also has negative profit). Findings should be read as a demonstration of the analysis, not as real business results.
