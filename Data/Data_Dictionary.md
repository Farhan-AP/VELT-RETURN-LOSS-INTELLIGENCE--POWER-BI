# Data Dictionary

**File:** `Data/VELT.csv`  
**Grain:** one row = one order  
**Size:** 2,000 rows × 15 columns  
**Data types** below are inferred from the CSV. The Power BI data types could not be read from the PBIX (see `DAX/Measures.md`).

| # | Column | Data type | Description | Business meaning | Values / range (from the data) |
|---|--------|-----------|-------------|------------------|-------------------------------|
| 1 | `Order_ID` | Text | Unique order identifier | Key for each order | `ORD0` to `ORD1999`, 2,000 unique values |
| 2 | `Category` | Text | Product category | Used to compare return behaviour by product type | Clothing (656), Handbag (657), Shoes (687) |
| 3 | `Price` | Whole number | Order value | Revenue of the order. The dashboard's **Total Revenue** equals the sum of this column | 20,367 – 499,199 (mean 151,781) |
| 4 | `Customer_Segment` | Text | Customer type | Separates VIP customers from regular customers | Regular (1,419), VIP (581) |
| 5 | `Region` | Text | Sales region | Where the order was sold | Asia (719), USA (654), Europe (627) |
| 6 | `Season` | Text | Season of the order | Lets seasonal patterns be compared. There is no date column | Summer (802), Winter (620), Spring (578) |
| 7 | `Demand_Level` | Text | Demand level when the order was placed | Context for demand pressure | Low (766), Medium (749), High (485) |
| 8 | `Supplier` | Text | Supplier / sourcing country | Used for supplier delay and return comparison | Italy (1,216), China (784) |
| 9 | `Delay` | Text (Yes/No) | Whether the order was delayed | Basis of the **Delay Rate** KPI | No (1,520), Yes (480) |
| 10 | `Shipping_Time` | Whole number | Shipping time (unit not stated; most likely days) | Delivery speed | 3 – 11 (mean 6.7) |
| 11 | `Shipping_Cost` | Whole number | Cost of shipping the order | Logistics cost | 1,035 – 39,822 (mean 10,373) |
| 12 | `Return_Status` | Text (Yes/No) | Whether the order was returned | Basis of the **Return Rate** KPI | No (1,472), Yes (528) |
| 13 | `Return_Reason` | Text | Reason given for the return | Shows what drives returns | No Return (1,472), Size Issue (252), Not as Expected (147), Quality Issue (129) |
| 14 | `Return_Cost` | Whole number | Cost caused by the return | Basis of the **Return Loss** KPI. It is 0 for every non-returned order | 0 – 48,726 (mean 2,932) |
| 15 | `Profit` | Whole number | Profit recorded for the order | Basis of **Total Profit**. It can be negative | -345,396 – 273,589 (mean 23,958) |

## Notes on the columns

- **Currency:** the CSV has no currency field. The dashboard shows values with the ₹ symbol, so this documentation uses ₹ for money values.
- **Return fields are consistent:** `Return_Reason` is `No Return` exactly when `Return_Status` is `No`. `Return_Cost` is greater than 0 exactly when `Return_Status` is `Yes`.
- **Profit:** the source does not explain how `Profit` was calculated. All 528 returned orders have negative profit and all 1,472 non-returned orders have positive profit. The column is used as supplied.
- **Shipping cost pattern:** `Shipping_Cost` is exactly 5% of `Price` for China orders and exactly 8% of `Price` for Italy orders. `Return_Cost` is between 5% and 10% of `Price` for returned orders.
- **No date column:** time trends cannot be analysed. Only `Season` is available.
- **Synthetic data:** the dataset was generated with AI for this project, so it describes no real customers or company.
- **No personal data:** there are no customer names, contact details or addresses.
