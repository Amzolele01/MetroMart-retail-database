# Data Source Inventory

## 1. Purpose

This document provides an inventory of the source datasets supplied for the MetroMart Retail Database Project.

The inventory establishes the datasets available for the project, their general business purpose, record counts, and the information contained in each dataset.

It serves as a reference for the subsequent data profiling, data quality investigation, database design, and development stages.

## 2. Source Data Overview

The project uses seven source datasets covering different areas of MetroMart's retail operations.

These datasets contain information relating to customers, employees, stores, products, sales transactions, and product returns.

The datasets were supplied separately and represent different aspects of the business. They will be examined individually before their potential relationships are incorporated into the database design.

The original source data is retained separately from the working copies used during profiling and investigation.

## 3. Dataset Inventory

The following table summarises the seven source datasets.

| No. | Dataset | Records | Fields | Description |
|---:|---|---:|---:|---|
| 1 | `customers` | 1,220 | 6 | Contains registered customer information, including customer identifiers, names, contact details, and location information. |
| 2 | `customer_export_legacy` | 350 | 4 | Contains customer information from a legacy export, including customer reference numbers, names, contact numbers, and cities. |
| 3 | `employees` | 60 | 4 | Contains employee information, including employee identifiers, names, assigned stores, and job roles. |
| 4 | `stores` | 5 | 4 | Contains store information, including store codes, store names, cities, and provinces. |
| 5 | `products` | 20 | 5 | Contains the product catalogue, including product identifiers, product names, categories, subcategories, and unit prices. |
| 6 | `sales_2023_2025` | 100,000 | 9 | Contains sales transaction records, including transaction dates, store and employee references, product information, quantities, prices, discounts, and recorded totals. |
| 7 | `returns` | 1,800 | 7 | Contains product return records, including return identifiers, transaction and customer references, product information, returned quantities, dates, and return reasons. |
| | **Total** | **103,455** | | **7 source datasets** |

*Record counts represent data records and exclude column headers where applicable.*

## 4. Source Dataset Field Overview

This section records the fields present in each supplied dataset. Field names are retained as they appear in the source data.

### 4.1 Customers

**Dataset:** `customers`

| Field | Description |
|---|---|
| `customer_id` | Customer identifier |
| `customer_name` | Customer's name |
| `phone` | Customer contact number |
| `email` | Customer email address |
| `city` | Customer's city |
| `province` | Customer's province |

### 4.2 Legacy Customer Export

**Dataset:** `customer_export_legacy`

| Field | Description |
|---|---|
| `cust_no` | Customer reference number |
| `full_name` | Customer's full name |
| `contact_number` | Customer contact number |
| `city` | Customer's city |

### 4.3 Employees

**Dataset:** `employees`

| Field | Description |
|---|---|
| `employee_id` | Employee identifier |
| `employee_name` | Employee's name |
| `store_id` | Reference to the employee's assigned store |
| `role` | Employee's job role |

### 4.4 Stores

**Dataset:** `stores`

| Field | Description |
|---|---|
| `store_code` | Store identifier |
| `store_name` | Store name |
| `city` | Store's city |
| `province` | Store's province |

### 4.5 Products

**Dataset:** `products`

| Field | Description |
|---|---|
| `product_id` | Product identifier |
| `product_name` | Product name |
| `category` | Product category |
| `subcategory` | Product subcategory |
| `unit_price` | Product unit price |

### 4.6 Sales Transactions

**Dataset:** `sales_2023_2025`

| Field | Description |
|---|---|
| `transaction_id` | Sales transaction identifier |
| `transaction_date` | Date and time of the transaction |
| `store_id` | Reference to the store where the transaction occurred |
| `employee_id` | Reference to the employee associated with the transaction |
| `product_id` | Reference to the product sold |
| `quantity` | Quantity sold |
| `unit_price` | Recorded unit price |
| `discount_pct` | Discount percentage applied |
| `total_amount` | Recorded transaction total |

### 4.7 Returns

**Dataset:** `returns`

| Field | Description |
|---|---|
| `return_id` | Return record identifier |
| `transaction_id` | Reference to the original sales transaction |
| `customer_id` | Customer reference associated with the return |
| `product_id` | Reference to the returned product |
| `quantity_returned` | Quantity returned |
| `return_date` | Date of the return |
| `reason` | Recorded reason for the return |

## 5. Source Data Notes

The following points provide important context for interpreting the source inventory.

### 5.1 Separate Customer Datasets

Two customer-related datasets were supplied:

- `customers` contains the main registered customer records.
- `customer_export_legacy` contains a separate legacy customer export.

Although both datasets contain customer information, their identifiers and structures differ. Their potential relationship will be examined during the profiling and relationship discovery stages.

### 5.2 Sales Dataset Structure

The supplied `sales_2023_2025` dataset contains nine fields. It does not contain a `customer_id` field.

The original business data dictionary includes a `customer_id` definition under sales. This difference between the dictionary and the actual supplied dataset is noted for further consideration. The source structure will be used as the reference when profiling the actual dataset.

### 5.3 Dataset Relationships

Some datasets contain fields that appear to reference records in other datasets. Examples include:

- Employee records referencing stores.
- Sales records referencing stores, employees, and products.
- Return records referencing sales transactions, customers, and products.

These are potential relationships identified from the field names and business context. Their validity and referential integrity have not been established through this inventory.

## 6. Inventory Summary

The MetroMart Retail Database Project begins with seven separate source datasets containing a total of **103,455 records**.

Together, these datasets provide information about the business's customers, legacy customer records, employees, stores, products, sales transactions, and product returns.

The inventory establishes the source data available for the project without making conclusions about its overall quality, consistency, or suitability for database implementation.

The next stage will examine the structure and characteristics of each dataset through individual data profiling.
