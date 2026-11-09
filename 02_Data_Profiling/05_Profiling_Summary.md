# Data Profiling Summary

## 1. Overview

This document consolidates the findings from the initial profiling of the seven source datasets supplied for the MetroMart Retail Database Project.

The profiling exercise focused on understanding the structure, completeness, uniqueness, field characteristics, and general distribution of values within each dataset.

Google Sheets was used to examine the source data and record the initial profiling results. The original source files were retained separately from the working copies used during the exercise.

## 2. Source Dataset Overview

The project contains seven source datasets covering different areas of MetroMart's retail operations.

| Dataset | Records | Fields |
|---|---:|---:|
| `customers` | 1,220 | 6 |
| `customer_export_legacy` | 350 | 4 |
| `employees` | 60 | 4 |
| `stores` | 5 | 4 |
| `products` | 20 | 5 |
| `sales_2023_2025` | 100,000 | 9 |
| `returns` | 1,800 | 7 |
| **Total** | **103,455** | **39** |

The sales dataset accounts for most of the records supplied, while the stores and products datasets provide smaller reference collections.

## 3. Overall Profiling Findings

### 3.1 Dataset Completeness

No missing values were identified in the following datasets during initial profiling:

- `customer_export_legacy`
- `employees`
- `stores`
- `products`
- `sales_2023_2025`
- `returns`

The `customers` dataset contained 25 missing values in the `phone` field.

All other fields in the customers dataset were complete according to the recorded profiling results.

### 3.2 Identifier Uniqueness

Several identifier fields contained unique values across their respective datasets.

| Dataset | Identifier Field | Records | Unique Values |
|---|---|---:|---:|
| `customers` | `customer_id` | 1,220 | 1,220 |
| `customer_export_legacy` | `cust_no` | 350 | 350 |
| `employees` | `employee_id` | 60 | 60 |
| `stores` | `store_code` | 5 | 5 |
| `products` | `product_id` | 20 | 20 |
| `sales_2023_2025` | `transaction_id` | 100,000 | 100,000 |
| `returns` | `return_id` | 1,800 | 1,800 |

These results identify potential primary key fields for the respective datasets.

The uniqueness of these fields within their own datasets does not independently establish their suitability as final database keys. That decision will be made during database design.

### 3.3 Repeated Values

Repeated values were observed in several descriptive and reference fields.

Examples include:

- Customer names in both customer datasets.
- Employee names in the employee dataset.
- Email addresses in the main customer dataset.
- Transaction timestamps in the sales dataset.
- Customer references across multiple return records.

Repeated values are not automatically data quality issues. Their significance depends on the business meaning of each field and the context in which the values occur.

### 3.4 Formatting and Representation

Several differences in field representation were observed:

- Phone numbers in the `customers` dataset contain different storage formats and lengths.
- The `customers` dataset uses `JHB` among its city values.
- The `stores` dataset contains both `Johannesburg` and `JHB`.
- Product category values contain differences in letter casing and naming.
- A trailing space was observed in product identifier `P011` in the sales and returns datasets.
- Some date and numerical fields were recorded as strings in the source data.

These observations provide areas for consideration during data preparation and database design.

## 4. Dataset-Specific Highlights

The following table summarises notable observations from the individual dataset profiles.

| Dataset | Notable Observations |
|---|---|
| `customers` | 25 missing phone values, repeated names, repeated email addresses, and the use of `JHB` as a city value. |
| `customer_export_legacy` | Repeated customer names, with all contact numbers populated and unique. |
| `employees` | Repeated employee names and different employee distributions across the five stores and four recorded roles. |
| `stores` | Two city representations: `Johannesburg` and `JHB`. |
| `products` | Differences in category naming, questionable category-subcategory combinations, and 17 unique unit prices. |
| `sales_2023_2025` | Repeated transaction timestamps, all five store references and 60 employee references represented, and a formatting variation involving `P011`. |
| `returns` | Repeated customer references, six returned quantity values, dates extending into 2026, and a formatting variation involving `P011`. |

## 5. Initial Relationship Discovery

The source structures revealed several potential relationships between datasets.

These include:

- Employees and stores.
- Sales transactions and stores.
- Sales transactions and employees.
- Sales transactions and products.
- Returns and sales transactions.
- Returns and customers.
- Returns and products.

The legacy customer dataset also presents potential connections to the main customer and returns datasets.

These relationships remain proposed until their validity and referential integrity have been examined.

One important limitation was identified: the original business data dictionary includes a `customer_id` field under sales, but the supplied `sales_2023_2025` dataset does not contain that field.

Therefore, a direct sales-to-customer relationship is not currently supported by the supplied sales structure.

## 6. Profiling Limitations

The initial profiling exercise provides an overview of the supplied data but does not establish that every field or record is valid.

In particular:

- Unique values do not automatically represent valid identifiers.
- Repeated values do not automatically represent duplicate records.
- Populated fields are not necessarily accurate or valid.
- Similar field names do not confirm relationships between datasets.
- Initial field classifications do not establish final database data types.
- Observed formatting differences do not automatically determine the appropriate cleaning method.

The profiling results should therefore be interpreted as preliminary findings rather than final data quality conclusions.

## 7. Conclusion

The initial profiling exercise established an understanding of the seven source datasets, their structures, and their general characteristics.

A total of 103,455 records across 39 fields were identified. The profiling revealed that most fields were complete, while several observations involving missing contact information, repeated values, formatting differences, field representation, and potential relationships were recorded.

The results provide a foundation for the next stages of the MetroMart Retail Database Project.

The detailed investigation of identified data quality concerns, validation of potential relationships, and decisions regarding data preparation are documented separately in the subsequent project stages.

No changes were made to the original source data during initial profiling.
