# Relationship Discovery

## 1. Purpose

This document records the potential relationships identified between the seven source datasets during initial data profiling.

The purpose is to establish an initial understanding of how records across different datasets may be connected, providing a foundation for subsequent data quality investigation and relational database design.

The relationships documented here are preliminary proposals based on field names, identifiers, and their apparent business meaning. They have not all been verified through referential integrity testing.

## 2. Identified Potential Relationships

The following relationships were identified from the available source structures.

| No. | Source Dataset | Source Field | Potential Target Dataset | Target Field | Relationship Purpose |
|---:|---|---|---|---|---|
| 1 | `employees` | `store_id` | `stores` | `store_code` | Associates employees with their assigned stores. |
| 2 | `sales_2023_2025` | `store_id` | `stores` | `store_code` | Associates sales transactions with the stores where they occurred. |
| 3 | `sales_2023_2025` | `employee_id` | `employees` | `employee_id` | Associates sales transactions with employees. |
| 4 | `sales_2023_2025` | `product_id` | `products` | `product_id` | Identifies the products recorded in sales transactions. |
| 5 | `returns` | `product_id` | `products` | `product_id` | Identifies products associated with return records. |
| 6 | `returns` | `transaction_id` | `sales_2023_2025` | `transaction_id` | Connects return records to their associated sales transactions. |
| 7 | `returns` | `customer_id` | `customers` | `customer_id` | Associates return records with customer records. |

## 3. Additional Relationship Considerations

### 3.1 Legacy Customer Dataset

The `customer_export_legacy` dataset contains a separate customer reference field, `cust_no`, while the main `customers` dataset uses `customer_id`.

The following potential connections were identified for consideration:

| Source Dataset | Source Field | Potential Target Dataset | Target Field | Purpose |
|---|---|---|---|---|
| `customer_export_legacy` | `cust_no` | `customers` | `customer_id` | Investigate whether legacy customer records correspond to records in the main customer dataset. |
| `customer_export_legacy` | `cust_no` | `returns` | `customer_id` | Investigate whether legacy customer references correspond to customer references recorded in returns. |

These are investigation candidates rather than established relationships. The different field names and dataset origins mean that matching identifiers must be examined before any relationship is accepted.

### 3.2 Sales and Customer Relationship

The original business data dictionary includes a `customer_id` field under sales. However, the actual supplied `sales_2023_2025` dataset does not contain this field.

Consequently, a direct relationship between sales transactions and customer records cannot currently be proposed using the supplied sales structure.

This limitation must be considered during database design and when determining the available customer-related reporting capabilities.

## 4. Relationship Validation Considerations

Before implementing these relationships in the relational database, the proposed connections will require further examination.

The following aspects should be considered:

- Whether source identifiers match across the relevant datasets.
- Whether referenced identifiers exist in their respective target datasets.
- Whether differences in formatting or representation affect matching.
- Whether the proposed relationships reflect the intended business meaning.
- Whether the relationship cardinalities are appropriate for the business context.

The presence of similarly named fields does not independently establish a valid relationship.

## 5. Summary

Initial relationship discovery identified potential connections between the employee, store, sales, product, customer, and returns datasets.

The most apparent connections involve employee-to-store assignments, sales-to-store and sales-to-employee references, sales-to-product references, and return references to transactions, customers, and products.

The legacy customer dataset introduces additional relationship considerations that require investigation.

A direct sales-to-customer relationship is not currently supported by the supplied sales source structure because it does not contain a `customer_id` field.

All relationships remain proposed until their validity and referential integrity have been examined. Confirmed relationships and final database constraints will be established during subsequent project stages.
