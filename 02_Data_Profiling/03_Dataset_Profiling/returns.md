# Returns Dataset Profile

## 1. Dataset Overview

The `returns` dataset contains records of products returned by customers. It includes return identifiers, references to sales transactions and customers, product information, returned quantities, return dates, and reasons for returns.

The dataset was profiled to understand its structure, completeness, uniqueness, return quantities, date distribution, and recorded return reasons.

| Attribute | Details |
|---|---|
| Dataset | `returns` |
| Total records | 1,800 |
| Total fields | 7 |
| Profiling tool | Google Sheets |

## 2. Field-Level Profile

The following table summarises the initial profiling results.

| Field | Data Type | Total Records | Missing Values | Unique Values |
|---|---|---:|---:|---:|
| `return_id` | String | 1,800 | 0 | 1,800 |
| `transaction_id` | String | 1,800 | 0 | 1,800 |
| `customer_id` | String | 1,800 | 0 | 937 |
| `product_id` | String | 1,800 | 0 | 20 |
| `quantity_returned` | Integer | 1,800 | 0 | 6 |
| `return_date` | String | 1,800 | 0 | 877 |
| `reason` | String | 1,800 | 0 | 4 |

## 3. Initial Profiling Observations

### 3.1 Return Identifier (`return_id`)

- All 1,800 records contain a return identifier.
- No missing values were identified.
- All 1,800 identifiers are unique.

**Observation:** Every return record has a distinct identifier. Based on the initial profiling results, `return_id` is a potential primary key.

### 3.2 Transaction Reference (`transaction_id`)

- All 1,800 records contain a transaction reference.
- No missing values were identified.
- All 1,800 transaction references are unique within the returns dataset.

**Observation:** Each return record references a distinct transaction identifier within this dataset. Whether these identifiers correspond to existing sales transactions has not been established through initial profiling.

### 3.3 Customer Reference (`customer_id`)

- All 1,800 records contain a customer reference.
- No missing values were identified.
- The dataset contains 937 unique customer identifiers.

**Observation:** Customer identifiers are repeated across some return records. This indicates that some customers are associated with multiple returns.

The validity and consistency of these references against the customer datasets are matters for further investigation.

### 3.4 Product Reference (`product_id`)

- All 1,800 records contain a product reference.
- No missing values were identified.
- All 20 product identifiers are represented.
- A trailing space was observed in the representation of product identifier `P011`.

**Observation:** All products in the product catalogue are represented in the returns dataset. The trailing space associated with `P011` is recorded as a potential formatting inconsistency.

### 3.5 Returned Quantity (`quantity_returned`)

- All 1,800 records contain a returned quantity.
- No missing values were identified.
- Six unique quantity values were identified.

| Quantity Returned | Records |
|---:|---:|
| 1 | 802 |
| 2 | 498 |
| 3 | 258 |
| 4 | 164 |
| 5 | 70 |
| 9 | 8 |
| **Total** | **1,800** |

**Observation:** Most return records involve quantities between one and five units. Eight records contain a returned quantity of nine units, which differs from the distribution of the other recorded values.

This pattern is retained for further consideration without assuming that the values are invalid.

### 3.6 Return Date (`return_date`)

- All 1,800 records contain a return date.
- No missing values were identified.
- The field contains 877 unique values.
- The recorded date range extends from 12 January 2023 to 28 January 2026.

**Observation:** Return dates cover a period extending beyond the 2023–2025 period indicated by the sales dataset filename.

The presence of 2026 dates is recorded as an observation for consideration when examining the relationship between sales and returns.

The field was recorded as a string during initial profiling.

### 3.7 Return Reason (`reason`)

- All 1,800 records contain a return reason.
- No missing values were identified.
- Four unique return reasons were identified.

| Return Reason | Records |
|---|---:|
| Customer Changed Mind | 476 |
| Damaged | 462 |
| Incorrect Item | 437 |
| Other | 425 |
| **Total** | **1,800** |

**Observation:** Four return reasons are represented in the dataset. Their record counts are relatively evenly distributed, with `Customer Changed Mind` having the highest count.

## 4. Profiling Summary

The initial profiling established the following characteristics:

- The dataset contains 1,800 records across seven fields.
- All return identifiers are populated and unique.
- All transaction references are populated and unique within the returns dataset.
- Customer references contain 937 unique identifiers.
- All 20 product identifiers are represented.
- A trailing space was observed in the representation of product identifier `P011`.
- Returned quantities contain six distinct values, including eight records with a quantity of nine.
- Return dates contain 877 unique values and range from 12 January 2023 to 28 January 2026.
- Four distinct return reasons are represented.
- No missing values were identified in any of the seven fields.

## 5. Profiling Conclusion

The `returns` dataset contains 1,800 complete records across seven fields.

Return identifiers are unique, while transaction references are also unique within the returns dataset. Customer references occur repeatedly, and all 20 products are represented.

The initial profiling identified several observations, including a product identifier formatting variation, a small group of records with returned quantities of nine, and return dates extending into 2026.

These observations provide an initial understanding of the returns dataset. Further investigation into transaction references, customer references, product identifiers, returned quantities, and date ranges is handled separately during the data quality investigation stage.

No changes were made to the original source data during profiling.
