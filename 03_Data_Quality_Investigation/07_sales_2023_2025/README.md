# Sales Dataset — Data Quality Investigation Report

## 1. Dataset Overview

**Dataset:** `sales_2023_2025.csv`  
**Investigation phase:** Phase 3 — Data Quality Investigation  
**Total records:** 100,000  
**Total attributes:** 10

The Sales dataset contains transaction records covering the 2023–2025 period.

The investigation was conducted using a working copy in Google Sheets. The original source dataset was not modified.

### Attributes investigated

| Column | Attribute |
|---|---|
| A | transaction_id |
| B | transaction_date |
| C | customer_id |
| D | store_id |
| E | employee_id |
| F | product_id |
| G | quantity |
| H | unit_price |
| I | discount_pct |
| J | total_amount |

## 2. Completeness and Whitespace Checks

The first investigation examined missing values and whitespace-only entries across all ten attributes.

### Results

| Check | Result |
|---|---:|
| Total records | 100,000 |
| Total attributes | 10 |
| Missing values across all attributes | 0 |
| Whitespace-only values across all attributes | 0 |

No missing or whitespace-only values were identified.

### Formulas used

**Total data records:**
```excel
=COUNTA(A2:A)
```

**Total attributes:**
```excel
=COUNTA(A1:J1)
```

**Whitespace-only check (example for column A):**
```excel
=SUM(ARRAYFORMULA(N((LEN(A2:A100001)>0)*(LEN(TRIM(A2:A100001))=0))))
```

The whitespace formula was adapted for each attribute by changing the column reference.

Missing-value counts were also checked individually for all ten attributes.

**Finding:** No completeness issues were identified.

## 3. Transaction ID Investigation

The transaction ID field was examined for duplicate values and deviations from the expected identifier pattern.

### Results

| Check | Result |
|---|---:|
| Duplicate transaction IDs | 0 |
| Invalid transaction ID formats | 0 |

The observed identifier pattern was `T` followed by seven digits, for example:

- T0000001
- T0000002

### Formulas used

**Duplicate transaction IDs:**
```excel
=COUNTA(A2:A100001)-COUNTUNIQUE(A2:A100001)
```

**Invalid transaction ID format:**
```excel
=SUM(ARRAYFORMULA(N(NOT(REGEXMATCH(A2:A100001,"^T[0-9]+$")))))
```

**Finding:** All transaction IDs were unique and followed the tested format.

## 4. Transaction Date Investigation

The transaction date field was examined to verify its storage type, date range and consistency.

The values were displayed in the following format:

`YYYY-MM-DD HH:MM:SS`

Example: `2025-10-06 20:03:56`

An individual value was checked using `ISNUMBER()` and returned TRUE, confirming that the date-time value was stored numerically rather than as plain text.

### Results

| Check | Result |
|---|---:|
| Missing transaction dates | 0 |
| Invalid numeric date values | 0 |
| Dates outside 2023–2025 | 0 |

### Formulas used

**Check whether a date is stored numerically:**
```excel
=ISNUMBER(B2)
```

**Invalid numeric transaction dates:**
```excel
=COUNT(B2:B100001)-COUNTIF(B2:B100001,">0")
```

**Dates outside the expected period:**
```excel
=COUNTIF(B2:B100001,"<"&DATE(2023,1,1))+COUNTIF(B2:B100001,">="&DATE(2026,1,1))
```

**Finding:** All transaction dates were stored as numeric date-time values and fell within the expected 2023–2025 period. The displayed date-time format was consistent in the inspected records.

## 5. Referential Integrity Investigation

The foreign-key attributes in the Sales dataset were compared against their corresponding reference datasets.

The reference datasets were held in separate Google Sheets spreadsheets. `IMPORTRANGE()` and `MATCH()` were used to compare the identifiers.

### 5.1 Customer References

**Sales attribute:** `customer_id`  
**Reference dataset:** `customers.csv` and `customer_export_legacy.csv`

The initial comparison identified 87 sales records containing customer ID `C0012`, which could not be found in either customer dataset.

### Results

| Check | Result |
|---|---:|
| Sales records with unmatched customer references | 87 |
| Distinct unmatched customer IDs | 1 |
| Unmatched customer ID | C0012 |

**Formula used to count unmatched customer references:**
```excel
=SUM(ARRAYFORMULA(N(ISNA(MATCH(C2:C100001,IMPORTRANGE("1xcDco1pvxN8bFzZe6fUqZv_AmHU5G_Ztd6-9_7fZ_9I","customers!A2:A"),0)))))
```

**Formula used to identify distinct unmatched customer IDs:**
```excel
=LET(ids,C2:C100001,valid,IMPORTRANGE("1xcDco1pvxN8bFzZe6fUqZv_AmHU5G_Ztd6-9_7fZ_9I","customers!A2:A"),COUNTUNIQUE(FILTER(ids,ISNA(MATCH(ids,valid,0)))))
```

**Finding:** Customer ID `C0012` is a confirmed unmatched reference. Its corresponding customer record was not found in either available customer dataset.

No customer record was invented or added during the investigation.

### 5.2 Store References

**Sales attribute:** `store_id`  
**Reference dataset:** Stores dataset

All Sales store IDs were compared against the store IDs in the separate Stores spreadsheet.

**Formula used:**
```excel
=SUM(ARRAYFORMULA(N(ISNA(MATCH(D2:D100001,IMPORTRANGE("1VrbNfXcvMlsA2SY2JL21X-wbuO6R8s22XQGQjE_WOEw","stores!A2:A"),0)))))
```

| Check | Result |
|---|---:|
| Invalid store references | 0 |

**Finding:** All sales records reference existing store IDs. No store-reference integrity issues were identified.

### 5.3 Employee References

**Sales attribute:** `employee_id`  
**Reference dataset:** Employees dataset

All Sales employee IDs were compared against the employee IDs in the separate Employees spreadsheet.

**Formula used:**
```excel
=SUM(ARRAYFORMULA(N(ISNA(MATCH(E2:E100001,IMPORTRANGE("1ZC8C1iaBH7X3422fLUJXW0qhTAYW-cwGtG_nA9upnFU","employees!A2:A"),0)))))
```

| Check | Result |
|---|---:|
| Invalid employee references | 0 |

**Finding:** All sales records reference existing employee IDs. No employee-reference integrity issues were identified.

### 5.4 Product References

**Sales attribute:** `product_id`  
**Reference dataset:** Products dataset

All Sales product IDs were compared against the product IDs in the separate Products spreadsheet.

**Formula used:**
```excel
=SUM(ARRAYFORMULA(N(ISNA(MATCH(F2:F100001,IMPORTRANGE("1cGz3OjqpO_b3RNqUQmaRdRfUucFjHf6Z","products!A2:A"),0)))))
```

| Check | Result |
|---|---:|
| Invalid product references | 0 |

**Finding:** All sales records reference existing product IDs. No product-reference integrity issues were identified.

## 6. Quantity and Unit Price Investigation

The quantity and unit price attributes were checked for zero and negative values.

### Results

| Check | Result |
|---|---:|
| Zero or negative quantities | 10 |
| Zero or negative unit prices | 0 |

### Formulas used

**Invalid quantity values:**
```excel
=COUNTIF(G2:G100001,"<=0")
```

**Invalid unit price values:**
```excel
=COUNTIF(H2:H100001,"<=0")
```

### Investigation of Negative Quantities

The ten records with zero or negative quantities were extracted for closer inspection.

All ten affected records had negative quantities and positive recorded `total_amount` values.

No accompanying documentation was available to explain whether negative quantities represented returns, reversals or another transaction type.

**Finding:** Ten records contain negative quantities with positive recorded totals. Their meaning remains unconfirmed and requires further investigation before any correction is considered.

## 7. Discount Percentage Investigation

The distinct values in `discount_pct` were examined to understand the discount values used in the dataset.

**Formula used:**
```excel
=SORT(UNIQUE(I2:I100001))
```

### Distinct values identified

| Discount value | Interpretation |
|---:|---:|
| 0 | 0% |
| 0.05 | 5% |
| 0.10 | 10% |
| 0.15 | 15% |
| 1.25 | 125% |

The value `1.25` differs significantly from the other discount values.

### Results

| Check | Result |
|---|---:|
| Records with discount value greater than 1 | 6 |

**Formula used:**
```excel
=COUNTIF(I2:I100001,">1")
```

**Finding:** Six records contain a discount value of `1.25`, which represents 125% if the field stores decimal discount rates. This is inconsistent with the other observed values and requires verification.

## 8. Total Amount Calculation Investigation

The recorded `total_amount` values were compared against an expected calculation using quantity, unit price and discount percentage.

### Expected calculation

\[
\text{Expected Total} =
\text{Quantity} \times \text{Unit Price} \times (1-\text{Discount})
\]

### Formula used

```excel
=SUM(ARRAYFORMULA(N(ABS(J2:J100001-(G2:G100001*H2:H100001*(1-I2:I100001)))>0.01)))
```

A tolerance of 0.01 was used to allow for minor decimal rounding differences.

### Results

| Check | Result |
|---|---:|
| Records with calculation discrepancies | 16 |

The affected records were extracted using:

```excel
=FILTER(A2:J100001,ABS(J2:J100001-(G2:G100001*H2:H100001*(1-I2:I100001)))>0.01)
```

### Investigation findings

The 16 affected records consisted of:

- **10 records** with negative quantities and positive recorded totals.
- **6 records** with positive quantities and a discount value of `1.25`.

The six records with the unusual discount value account for the six positive-quantity calculation discrepancies. The remaining ten discrepancies correspond to the negative-quantity records.

**Finding:** Sixteen records do not agree with the expected total calculation. The discrepancies are associated with the negative quantities and unusual discount values identified earlier.

## 9. Consolidated Investigation Results

| Investigation area | Finding |
|---|---|
| Dataset structure | 100,000 records and 10 attributes |
| Completeness | No missing values |
| Whitespace | No whitespace-only values |
| Transaction IDs | No duplicates or tested format deviations |
| Transaction dates | No invalid dates or dates outside 2023–2025 |
| Customer references | 87 records reference unmatched customer ID C0012 |
| Store references | All references valid |
| Employee references | All references valid |
| Product references | All references valid |
| Quantity | 10 negative-quantity records |
| Unit price | No zero or negative values |
| Discount percentage | 6 records contain the unusual value 1.25 |
| Total amount | 16 calculation discrepancies |

## 10. Conclusion and Phase 4 Considerations

The Sales dataset contains 100,000 records and 10 attributes. The investigation found that the dataset is complete, with no missing values or whitespace-only entries. Transaction IDs were unique, transaction dates were within the expected period, and all store, employee and product references were valid.

However, several data quality issues require attention before the dataset can be considered fully validated.

The main findings are:

1. **Unmatched customer reference:** Customer ID `C0012` appears in 87 sales records but is absent from both available customer datasets.
2. **Negative quantities:** Ten records contain negative quantities and positive recorded totals. The meaning of these transactions has not been established.
3. **Unusual discount values:** Six records contain a discount value of `1.25`, unlike the other observed discount values.
4. **Calculation discrepancies:** Sixteen records have recorded totals that do not match the expected calculation.

### Decisions for Phase 4

- Investigate the unmatched customer ID before deciding how to handle the affected records.
- Verify the meaning of negative quantities before changing or excluding those transactions.
- Confirm the intended representation of the discount percentage field and investigate the six values of `1.25`.
- Recalculate or correct total amounts only after the underlying quantity and discount issues have been resolved.
- Preserve the original source data and document any changes made during cleaning.

**Final investigation status:** Completed. The identified issues have been recorded for further investigation and resolution during Phase 4. No changes were made to the original Sales dataset.
