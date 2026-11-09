# Returns Dataset — Data Quality Investigation

## 1. Dataset Overview

The `returns.csv` dataset contains 1,800 records and seven attributes relating to returned products.

| Attribute | Description |
|---|---|
| return_id | Unique identifier assigned to each return |
| transaction_id | Identifier of the original sales transaction |
| customer_id | Identifier of the customer associated with the return |
| product_id | Identifier of the returned product |
| quantity_returned | Quantity of products returned |
| return_date | Date on which the return was recorded |
| reason | Recorded reason for the return |

The investigation was conducted using a working copy in Google Sheets. The original source file remained unchanged throughout the investigation.

## 2. Missing Values

All seven attributes were checked for missing values.

| Attribute | Missing Values |
|---|---:|
| return_id | 0 |
| transaction_id | 0 |
| customer_id | 0 |
| product_id | 0 |
| quantity_returned | 0 |
| return_date | 0 |
| reason | 0 |
| **Total** | **0** |

**Finding:** No missing values were identified in the dataset. All 1,800 records contain values across the seven attributes.

## 3. Duplicate Records and Identifier Uniqueness

### 3.1 Return ID

The `return_id` attribute was checked for uniqueness.

- Total records: 1,800
- Unique return IDs: 1,800
- Duplicate return IDs: 0

All return IDs are unique.

### 3.2 Transaction ID

The `transaction_id` attribute was also checked for uniqueness within the Returns dataset.

- Total records: 1,800
- Unique transaction IDs: 1,800
- Duplicate transaction IDs: 0

Each transaction ID appears only once in the Returns dataset.

### 3.3 Exact Duplicate Records

The complete seven-column records were checked for exact duplicates.

**Finding:** No exact duplicate records were identified across all seven attributes.

### 3.4 Customer and Product Identifiers

The dataset contains:

- 937 unique customer IDs.
- 20 unique product IDs.

These counts describe the distinct identifiers present in the Returns dataset; they do not independently establish whether the references are valid. Referential integrity was investigated separately.

## 4. Quantity Returned Investigation

The `quantity_returned` attribute was checked for numeric values, missing values, and unusual quantities.

| Measure | Result |
|---|---:|
| Total records | 1,800 |
| Numeric values | 1,800 |
| Missing values | 0 |
| Minimum quantity | 1 |
| Maximum quantity | 9 |
| Average quantity | 2.0278 |
| Zero or negative quantities | 0 |

All 1,800 records contain positive numeric quantities.

### 4.1 Comparison Against Sales Quantities

Return quantities were compared with the corresponding quantities in `sales_2023_2025.csv`.

Eight return records contain quantities greater than the positive quantities recorded in their corresponding sales transactions.

| Return ID | Transaction ID | Quantity Returned | Quantity Sold |
|---|---|---:|---:|
| R00026 | T0099958 | 9 | 4 |
| R00177 | T0082542 | 9 | 1 |
| R00451 | T0023828 | 9 | 1 |
| R00813 | T0000735 | 9 | 5 |
| R00881 | T0036791 | 9 | 2 |
| R01076 | T0038076 | 9 | 1 |
| R01424 | T0098066 | 9 | 3 |
| R01758 | T0019621 | 9 | 5 |

**Finding:** Eight return quantities exceed the quantities recorded in their corresponding sales transactions.

These records require further business clarification. The investigation does not establish whether the quantities are incorrect, whether multiple items were returned against a transaction, or whether the source system follows a different recording rule.

No quantity values were changed.

## 5. Return Date Investigation

The `return_date` attribute was checked for valid date values and dates outside the sales dataset's 2023–2025 reporting period.

| Measure | Result |
|---|---|
| Invalid return dates | 0 |
| Earliest return date | 2023-01-12 |
| Latest return date | 2026-01-28 |
| Dates before 2023 | 0 |
| Dates after 2025 | 19 |

All return dates were valid date values.

### 5.1 Return Dates Outside the Sales Reporting Period

Nineteen return records have dates in 2026, outside the 2023–2025 period covered by the sales dataset.

These dates were not automatically classified as invalid because a return may be recorded after the original sales reporting period.

### 5.2 Comparison with Original Transaction Dates

Return dates were compared with their corresponding sales transaction dates.

| Check | Result |
|---|---:|
| Returns dated before the original transaction | 0 |
| Returns dated more than 30 days after the original transaction | 0 |

The 30-day comparison was used as an investigative check, not as an official MetroMart return policy.

**Finding:** All return dates occur on or after their corresponding transaction dates, and none exceeds the 30-day investigative threshold.

## 6. Return Reason Investigation

The `reason` attribute was examined to establish the distribution of recorded return reasons.

| Return Reason | Records |
|---|---:|
| Customer Changed Mind | 476 |
| Damaged | 462 |
| Incorrect Item | 437 |
| Other | 425 |
| **Total** | **1,800** |

All records contain a return reason.

**Finding:** Four distinct return reasons were identified. No missing reason values were found.

The investigation did not establish whether these are the only permitted values under an official business reference list.

## 7. Cross-Dataset Referential Integrity

The Returns dataset was compared with the relevant source datasets to establish whether its identifiers correspond to existing records.

### 7.1 Transaction ID References

All 1,800 transaction IDs in `returns.csv` were checked against `sales_2023_2025.csv`.

| Measure | Result |
|---|---:|
| Return transaction references | 1,800 |
| Matching sales transactions | 1,800 |
| Unmatched transaction references | 0 |

**Finding:** All return records reference an existing sales transaction.

### 7.2 Customer ID References

Customer IDs were checked against the main `customers.csv` dataset and the supplementary `customer_export_legacy.csv` dataset.

Two return records reference customer ID `C0012`.

| Return ID | Transaction ID | Customer ID |
|---|---|---|
| R00632 | T0042515 | C0012 |
| R01453 | T0093530 | C0012 |

Both transaction IDs exist in the Sales dataset. However, customer ID `C0012` does not exist in either customer dataset.

The Sales investigation independently identified the same customer ID as missing from both customer datasets, affecting 87 sales records.

**Finding:** Two Returns records contain customer references that cannot be resolved against the available customer datasets. This is consistent with the issue identified during the Sales investigation.

The customer ID was not replaced or inferred.

### 7.3 Product ID References

All product IDs in the Returns dataset were checked against `products.csv`.

| Measure | Result |
|---|---:|
| Return product references | 1,800 |
| Matching product references | 1,800 |
| Unmatched product references | 0 |

**Finding:** All returned product IDs exist in the Products dataset.

### 7.4 Product Consistency with Sales Transactions

The product IDs recorded in Returns were compared with the product IDs in their corresponding Sales transactions.

| Check | Result |
|---|---:|
| Product ID mismatches | 0 |
| Missing transaction matches | 0 |

**Finding:** All return records have a matching sales transaction, and the product IDs agree between the two datasets.

## 8. Relationship Between Returns and Negative Sales Quantities

During the Sales investigation, ten transactions were identified with negative quantities.

These records were cross-checked against the Returns dataset to investigate whether negative Sales quantities could represent returned products.

One of the ten negative-quantity transactions has a corresponding return record.

### 8.1 Confirmed Matching Record

**Sales record:**

| Transaction ID | Customer ID | Product ID | Quantity | Transaction Date |
|---|---|---|---:|---|
| T0035854 | C0682 | P017 | -3 | 2024-06-06 |

**Corresponding Returns record:**

| Return ID | Transaction ID | Customer ID | Product ID | Quantity Returned | Return Date | Reason |
|---|---|---|---|---:|---|---|
| R01359 | T0035854 | C0682 | P017 | 1 | 2024-06-17 | Customer Changed Mind |

The two records agree on transaction ID, customer ID, and product ID.

The return was recorded 11 days after the original transaction. However, the Sales record contains a quantity of -3, while the Returns record records a returned quantity of 1.

### 8.2 Overall Finding

| Measure | Result |
|---|---:|
| Negative-quantity Sales transactions | 10 |
| Transactions with a matching Returns record | 1 |
| Transactions without a matching Returns record | 9 |

**Finding:** Only one of the ten negative-quantity Sales transactions has a corresponding Returns record.

Although the matching record provides evidence of a relationship between the two datasets, it does not establish that negative Sales quantities represent returns. The quantity difference also means the two records cannot be treated as equivalent.

Further clarification of the Sales quantity recording rules is required before assigning a business meaning to negative quantities.

## 9. Summary of Findings

| Investigation Area | Finding |
|---|---|
| Missing values | No missing values across all seven attributes |
| Return IDs | 1,800 unique IDs; no duplicates |
| Transaction IDs | 1,800 unique IDs within Returns |
| Exact duplicate records | None identified |
| Customer IDs | 937 unique values; two records reference unresolved customer ID C0012 |
| Product IDs | 20 unique values; all references valid |
| Returned quantities | All positive and numeric |
| Quantity comparison | Eight return quantities exceed corresponding sales quantities |
| Return dates | All valid; 19 dates fall in 2026 |
| Date comparison | No returns before transactions or more than 30 days afterward |
| Return reasons | Four distinct values; no missing values |
| Transaction references | All 1,800 match Sales |
| Product consistency | No mismatches between Returns and Sales |
| Negative Sales quantities | One of ten has a corresponding Returns record |

## 10. Conclusion

The Returns dataset contains 1,800 complete records with no missing values, duplicate return IDs, duplicate transaction IDs, or exact duplicate records.

All transaction references are valid against the Sales dataset, and all product references are valid against the Products dataset. Product IDs also agree between the Returns records and their corresponding Sales transactions.

The investigation identified two records referencing customer ID `C0012`, which is absent from both available customer datasets. This is consistent with the unresolved customer reference identified during the Sales investigation.

Additional observations include eight return quantities that exceed their corresponding sales quantities and 19 return dates outside the Sales dataset's 2023–2025 reporting period. These findings require business clarification rather than automatic correction.

The cross-check of negative Sales quantities identified one corresponding Returns record, but the available evidence is insufficient to establish that negative Sales quantities represent returns.

No changes were made to the original source dataset. All identified issues and observations will be carried forward for consideration during Phase 4, where cleaning, validation, and transformation decisions will be made using documented rules and supporting evidence.
