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

