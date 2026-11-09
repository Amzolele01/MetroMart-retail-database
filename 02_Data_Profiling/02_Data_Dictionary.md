# Initial Data Dictionary

## 1. Purpose

This document defines the fields identified in the MetroMart source datasets and provides descriptions of their intended business meaning.

The initial data dictionary serves as a reference during data profiling, data quality investigation, and database design.

It combines the original business data dictionary supplied with the project information and an extended field reference covering all seven source datasets.

Field descriptions are based on the available source information and the apparent purpose of each field. They do not establish database constraints, data types, or confirmed relationships.

## 2. Original Business Data Dictionary

The original business data dictionary provided definitions for selected fields in the customer and sales datasets.

### 2.1 Customers

| Field | Description |
|---|---|
| `customer_id` | Customer identifier |
| `customer_name` | Customer full name |
| `phone` | Customer contact number |
| `email` | Customer email address |

### 2.2 Sales

| Field | Description |
|---|---|
| `transaction_id` | Transaction identifier |
| `transaction_date` | Date and time of transaction |
| `customer_id` | Customer identifier |
| `product_id` | Product identifier |
| `quantity` | Quantity sold |
| `unit_price` | Price per unit |
| `discount_pct` | Discount applied |
| `total_amount` | Recorded transaction total |

## 3. Extended Source Field Reference

The following sections expand the original dictionary to include every field present in the seven supplied source datasets.

### 3.1 Customers

**Source dataset:** `customers`

| Field | Description |
|---|---|
| `customer_id` | Unique reference used to identify a customer record. |
| `customer_name` | Customer's recorded name. |
| `phone` | Customer's recorded contact number. |
| `email` | Customer's recorded email address. |
| `city` | City associated with the customer record. |
| `province` | Province associated with the customer record. |

### 3.2 Legacy Customer Export

**Source dataset:** `customer_export_legacy`

| Field | Description |
|---|---|
| `cust_no` | Customer reference number in the legacy dataset. |
| `full_name` | Customer's recorded full name. |
| `contact_number` | Customer's recorded contact number. |
| `city` | City associated with the customer record. |

### 3.3 Employees

**Source dataset:** `employees`

| Field | Description |
|---|---|
| `employee_id` | Identifier assigned to an employee. |
| `employee_name` | Employee's recorded name. |
| `store_id` | Store reference associated with the employee. |
| `role` | Employee's recorded job role. |

### 3.4 Stores

**Source dataset:** `stores`

| Field | Description |
|---|---|
| `store_code` | Identifier assigned to a store. |
| `store_name` | Name of the store. |
| `city` | City in which the store is located. |
| `province` | Province in which the store is located. |

### 3.5 Products

**Source dataset:** `products`

| Field | Description |
|---|---|
| `product_id` | Identifier assigned to a product. |
| `product_name` | Name of the product. |
| `category` | Main category assigned to the product. |
| `subcategory` | Subcategory assigned to the product. |
| `unit_price` | Recorded selling price per unit. |

### 3.6 Sales Transactions

**Source dataset:** `sales_2023_2025`

| Field | Description |
|---|---|
| `transaction_id` | Identifier assigned to a sales transaction. |
| `transaction_date` | Date and time recorded for the transaction. |
| `store_id` | Store reference associated with the transaction. |
| `employee_id` | Employee reference associated with the transaction. |
| `product_id` | Product reference associated with the transaction. |
| `quantity` | Number of units recorded as sold. |
| `unit_price` | Recorded price per unit for the transaction. |
| `discount_pct` | Discount percentage recorded for the transaction. |
| `total_amount` | Total amount recorded for the transaction. |

### 3.7 Returns

**Source dataset:** `returns`

| Field | Description |
|---|---|
| `return_id` | Identifier assigned to a return record. |
| `transaction_id` | Reference to the associated sales transaction. |
| `customer_id` | Customer reference recorded for the return. |
| `product_id` | Product reference associated with the return. |
| `quantity_returned` | Number of units recorded as returned. |
| `return_date` | Date recorded for the return. |
| `reason` | Recorded reason for the return. |

## 4. Dictionary Limitations and Source Notes

### 4.1 Difference Between the Original Dictionary and Sales Source

The original business data dictionary defines a `customer_id` field under sales. However, the actual supplied `sales_2023_2025` dataset contains nine fields and does not include `customer_id`.

The extended source field reference therefore reflects the actual supplied dataset rather than adding a field based solely on the original dictionary.

This discrepancy is retained as a documentation note for consideration during subsequent project stages.

### 4.2 Descriptions and Data Types

The descriptions in this document explain the apparent business meaning of each field.

They should not be interpreted as final database definitions. Actual data types, constraints, nullability, keys, and other implementation decisions will be established through profiling, investigation, and database design.

### 4.3 Potential Relationships

Some fields appear to contain references to records in other datasets. These similarities provide an initial basis for relationship discovery.

However, the presence of similarly named identifier fields does not confirm that the records match or that a valid relationship exists.

These relationships will be examined separately.

## 5. Summary

The initial data dictionary provides a consolidated reference for the fields contained in all seven MetroMart source datasets.

It preserves the original business definitions while extending field descriptions to cover the complete supplied source collection.

The dictionary will serve as a reference throughout the remaining profiling and database development stages. Definitions may be refined as further information about the data and business requirements becomes available.
