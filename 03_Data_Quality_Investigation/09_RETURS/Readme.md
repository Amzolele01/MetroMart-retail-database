# Returns Dataset — Data Quality Investigation

## 1. Dataset Overview

**Source file:** `returns.csv`

**Investigation phase:** Phase 3 — Data Quality Investigation

**Records:** 1,800

**Columns:** 7

### Source columns

- `return_id`
- `transaction_id`
- `customer_id`
- `product_id`
- `quantity_returned`
- `return_date`
- `reason`

The investigation was conducted using a separate Google Sheets working sheet. The original source file was not modified.

## 2. Completeness and Missing Values

All seven columns were checked for missing values.

| Column | Missing values |
|---|---:|
| return_id | 0 |
| transaction_id | 0 |
| customer_id | 0 |
| product_id | 0 |
| quantity_returned | 0 |
| return_date | 0 |
| reason | 0 |

**Finding:** No missing values were identified across the 1,800 records.

## 3. Identifier Uniqueness

The identifier fields were examined to understand their uniqueness.

| Identifier | Unique values |
|---|---:|
| return_id | 1,800 |
| transaction_id | 1,800 |
| customer_id | 937 |
| product_id | 20 |

- All 1,800 return IDs were unique.
- No duplicate return IDs were identified.
- All 1,800 transaction IDs were unique within the Returns dataset.
- The dataset contains 937 distinct customers and 20 distinct products.

The transaction ID result indicates that each return record references a different transaction in this dataset.

## 4. Duplicate Record Investigation

The complete records were checked for exact duplicates across all seven columns.

**Formula used:**

```excel
=COUNTA(A2:A1801)-COUNTUNIQUE(ARRAYFORMULA(A2:A1801&"♦"&B2:B1801&"♦"&C2:C1801&"♦"&D2:D1801&"♦"&E2:E1801&"♦"&F2:F1801&"♦"&G2:G1801))
```

**Result:** 0 exact duplicate records.

No identical records were identified.

## 5. Quantity Validation

The `quantity_returned` field was checked for numeric validity and unusual values.

| Check | Result |
|---|---:|
| Numeric values | 1,800 |
| Non-numeric, nonblank values | 0 |
| Zero quantities | 0 |
| Negative quantities | 0 |
| Minimum quantity | 1 |
| Maximum quantity | 9 |
| Average quantity | 2.0278 |

**Finding:** All returned quantities were numeric and positive. No zero or negative returned quantities were identified.

### 5.1 Returned Quantity Compared with Quantity Sold

Returned quantities were compared with the original sales quantities using the corresponding transaction IDs.

The comparison was performed in a separate `Returns_Check` sheet within the Sales spreadsheet.

**Quantity comparison formula:**

```excel
=IF(B2>C2,"Exceeds sold quantity","Within sold quantity")
```

Where:
- Column B contains quantity returned.
- Column C contains quantity sold.

**Results:**

- 8 returns exceeded their corresponding positive sales quantities.
- 1 additional return referenced a transaction with a negative sales quantity.

#### Records where returned quantity exceeded positive quantity sold

| Return ID | Transaction ID | Returned | Sold |
|---|---|---:|---:|
| R00026 | T0099958 | 9 | 4 |
| R00177 | T0082542 | 9 | 1 |
| R00451 | T0023828 | 9 | 1 |
| R00813 | T0000735 | 9 | 5 |
| R00881 | T0036791 | 9 | 2 |
| R01076 | T0038076 | 9 | 1 |
| R01424 | T0098066 | 9 | 3 |
| R01758 | T0019621 | 9 | 5 |

**Finding:** Eight records contain returned quantities greater than the quantities recorded as sold. These are confirmed quantity discrepancies requiring further investigation.

#### Related negative sales quantity

Transaction `T0035854`, associated with return `R00632`, records a sales quantity of `-3`.

The corresponding Sales record contains:

| Field | Value |
|---|---|
| Transaction ID | T0035854 |
| Transaction date | 2024-06-06 11:54:11 |
| Customer ID | C0682 |
| Store ID | S005 |
| Employee ID | E019 |
| Product ID | P017 |
| Quantity | -3 |
| Unit price | 59 |
| Discount | 0 |
| Total amount | 177 |

The negative quantity originates in the Sales dataset. It is therefore recorded as a related Sales data-quality issue, rather than classified as a normal over-return.

## 6. Return Date Validation

The `return_date` field was checked for valid date values and date boundaries.

| Check | Result |
|---|---|
| Valid date values | 1,800 |
| Non-numeric, nonblank values | 0 |
| Earliest return date | 2023-01-12 |
| Latest return date | 2026-01-28 |
| Dates before 2023 | 0 |
| Dates after 2025 | 19 |

**Finding:** All 1,800 return dates were valid date values. Nineteen records have dates after the 2023–2025 sales period.

These dates were retained as observations for further consideration rather than automatically classified as errors.

### 6.1 Return Dates Compared with Transaction Dates

Return dates were compared with their corresponding sales transaction dates.

| Check | Result |
|---|---:|
| Return dates earlier than transaction dates | 0 |
| Returns more than 30 days after transaction dates | 0 |

The comparison identified no return dates earlier than their corresponding transaction dates and no returns occurring more than 30 days after the original transactions.

The 30-day comparison is an investigative threshold, not confirmation of an official business return policy.

## 7. Return Reason Investigation

Four distinct return reasons were identified.

| Return reason | Records | Percentage |
|---|---:|---:|
| Customer Changed Mind | 476 | 26.44% |
| Damaged | 462 | 25.67% |
| Incorrect Item | 437 | 24.28% |
| Other | 425 | 23.61% |
| **Total** | **1,800** | **100%** |

**Finding:** Four return reasons account for all 1,800 records. No missing return reasons were identified.

## 8. Cross-Dataset Reference Validation

The Returns dataset was checked against the Customers, Products and Sales datasets.

### 8.1 Transaction References

Every `transaction_id` in Returns was checked against the Sales dataset.

**Unmatched transaction IDs:** 0

All 1,800 return transactions have corresponding transaction IDs in Sales.

### 8.2 Customer References

Every `customer_id` was checked against the Customers dataset.

**Unmatched customer IDs:** 2 records.

| Return ID | Transaction ID | Customer ID |
|---|---|---|
| R00632 | T0042515 | C0012 |
| R01453 | T0093530 | C0012 |

Both transactions exist in Sales and also reference customer `C0012`.

**Finding:** Customer `C0012` is referenced by both Sales and Returns but is absent from the Customers master dataset. This indicates a missing customer master record rather than a disagreement between Sales and Returns.

### 8.3 Product References

All returned product IDs were checked against the 20 product IDs in the Products dataset.

**Unmatched product references:** 0

All 1,800 return records reference product IDs found in the Products dataset.

### 8.4 Product Consistency Against Sales

The product IDs in Returns were compared with the product IDs in the corresponding Sales transactions.

| Check | Result |
|---|---:|
| Product mismatches | 0 |
| Missing transaction matches | 0 |

**Finding:** All 1,800 return records have matching product IDs in their corresponding Sales transactions.

## 9. Summary of Findings

### Confirmed data-quality findings

1. Eight returns have quantities greater than the corresponding positive sales quantities.
2. Two return records reference customer `C0012`, which is missing from the Customers master dataset.
3. The related Sales transaction `T0035854` contains a negative sales quantity of `-3`. This is a Sales dataset issue associated with one return record.

### Observations

1. Nineteen return dates fall outside the 2023–2025 sales period, extending into January 2026.
2. The Returns dataset contains one return record per transaction ID.
3. Four distinct return reasons account for all records.

### Checks with no identified issues

- No missing values.
- No duplicate return IDs.
- No exact duplicate records.
- No invalid or non-positive returned quantities.
- No invalid return dates.
- No return dates earlier than their corresponding sales dates.
- No returns more than 30 days after their corresponding sales dates.
- No unmatched transaction references.
- No unmatched product references.
- No product mismatches between Returns and Sales.

## 10. Conclusion

The Returns dataset contains 1,800 records with complete fields, unique return identifiers and valid basic quantity and date values.

Cross-dataset validation confirmed that all transaction and product references exist and that returned products match their corresponding sales transactions.

The investigation identified eight returned-quantity discrepancies and two records referencing a customer missing from the Customers master dataset. One additional return is associated with a negative quantity in the Sales dataset.

These findings must be preserved for the subsequent cleaning and validation phase. The original source data remains unchanged at this stage.

