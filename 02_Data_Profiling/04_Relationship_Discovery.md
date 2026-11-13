# MetroMart Retail Database Project – Relationship Discovery

## 1. Purpose

The purpose of relationship discovery is to identify potential connections between the supplied datasets before designing the relational database.

This stage examines dataset attributes, identifier formats, and their apparent business meaning to identify fields that may link records across different datasets.

The relationships identified in this document are preliminary. They must be verified through data inspection and referential integrity checks before being treated as confirmed database relationships.

## 2. Datasets and Relevant Attributes

The following datasets were considered during relationship discovery.

### 2.1 Customers

**Source:** `customers.csv`

| Attribute |
|---|
| customer_id |
| customer_name |
| phone |
| email |
| city |
| province |

Contains registered customer information and their associated customer identifiers.

### 2.2 Legacy Customer Export

**Source:** `customer_export_legacy.csv`

| Attribute |
|---|
| cust_no |
| full_name |
| contact_number |
| city |

Contains customer information from an older export. Its identifiers and records may overlap with the current customer dataset.

### 2.3 Employees

**Source:** `employees.csv`

| Attribute |
|---|
| employee_id |
| employee_name |
| store_id |
| role |

Contains employee information, including their assigned store and role.

### 2.4 Stores

**Source:** `stores.csv`

| Attribute |
|---|
| store_code |
| store_name |
| city |
| province |

Contains the store master records and their identifying codes.

### 2.5 Products

**Source:** `products.xlsx`

| Attribute |
|---|
| product_id |
| product_name |
| category |
| subcategory |
| unit_price |

Contains the product catalogue and associated product information.

### 2.6 Sales

**Source:** `sales_2023_2025.csv`

| Attribute |
|---|
| transaction_id |
| transaction_date |
| customer_id |
| store_id |
| employee_id |
| product_id |
| quantity |
| unit_price |
| discount_pct |
| total_amount |

Contains sales transaction records, including the associated customer, store, employee, product, and financial information.

### 2.7 Returns

**Source:** `returns.csv`

| Attribute |
|---|
| return_id |
| transaction_id |
| customer_id |
| product_id |
| quantity_returned |
| return_date |
| reason |

Contains product return records and the identifiers needed to associate returns with customers, products, and original sales transactions.

## 3. Potential Relationships

The following relationships were identified based on the available dataset attributes and their apparent business meaning.

| No. | Source Dataset | Source Field | Potential Target Dataset | Target Field | Relationship Purpose |
|---:|---|---|---|---|---|
| 1 | stores | store_code | employees | store_id | Identifies the store assigned to each employee. |
| 2 | stores | store_code | sales_2023_2025 | store_id | Identifies the store where a sale occurred. |
| 3 | customers | customer_id | sales_2023_2025 | customer_id | Identifies the customer associated with a sale. |
| 4 | employees | employee_id | sales_2023_2025 | employee_id | Identifies the employee associated with a sale. |
| 5 | products | product_id | sales_2023_2025 | product_id | Identifies the product included in a sales record. |
| 6 | customers | customer_id | returns | customer_id | Identifies the customer associated with a return. |
| 7 | products | product_id | returns | product_id | Identifies the product being returned. |
| 8 | sales_2023_2025 | transaction_id | returns | transaction_id | Connects a return to its original sales transaction. |
| 9 | customers | customer_id | customer_export_legacy | cust_no | Investigates whether legacy customer records correspond to records in the current customer dataset. |
| 10 | customers | customer_id | customer_export_legacy | cust_no | Provides a basis for comparing legacy customer identifiers against the current customer records. |

**Note:** Rows 9 and 10 describe the same field-level candidate and should ultimately be represented by a single relationship. The legacy export should also be checked against customer identifiers appearing in sales and returns, but those comparisons are investigative checks rather than additional confirmed foreign-key relationships.

## 4. Additional Relationship Considerations

### 4.1 Legacy Customer Identifiers

The legacy customer export uses `cust_no`, while the current customer dataset uses `customer_id`.

Both fields contain customer identifiers, making a comparison between the datasets relevant.

The investigation should establish whether:

- Legacy identifiers correspond to existing customer records.
- The two datasets contain overlapping customer records.
- Any identifiers or customer records require mapping or reconciliation.

The existence of similar identifier formats does not, by itself, establish that the records represent the same customers.

### 4.2 Sales and Returns Consistency

The returns dataset contains `transaction_id`, `customer_id`, and `product_id`.

These fields provide an opportunity to verify whether each return corresponds to the correct original sales transaction.

The investigation should check that:

- The return transaction exists in the sales dataset.
- The customer recorded in the return matches the customer associated with the original sale.
- The returned product matches the product recorded in the original sale.

### 4.3 Customer Identifier Consistency

The current customer dataset contains both standard and legacy-style customer identifiers.

These variations require careful investigation before customer records are consolidated or identifiers are changed.

Any proposed customer consolidation must preserve the relationships between customers, sales, and returns.

## 5. Relationship Verification

Identifying a potential relationship does not confirm that the relationship is valid.

The following checks are required during subsequent validation:

- Check whether employee store identifiers exist in the stores dataset.
- Check whether sales customer identifiers exist in the customers dataset.
- Check whether sales store identifiers exist in the stores dataset.
- Check whether sales employee identifiers exist in the employees dataset.
- Check whether sales product identifiers exist in the products dataset.
- Check whether return customer identifiers exist in the customers dataset.
- Check whether return product identifiers exist in the products dataset.
- Check whether return transaction identifiers exist in the sales dataset.
- Compare customer and product identifiers in returns against the corresponding original sales records.
- Compare legacy customer identifiers against the current customer records and relevant transaction references.

The results of these checks will determine which relationships can be confirmed for the eventual database design.

## 6. Limitations

The relationships documented here are based on the available source attributes and preliminary dataset inspection.

They do not automatically establish:

- Primary keys or foreign keys.
- Cardinality between related datasets.
- Whether all referenced identifiers are valid.
- Whether records with matching identifiers represent the same real-world entity.

These aspects must be confirmed through further validation and database modelling.

## 7. Conclusion

Relationship discovery has identified potential connections across the customer, legacy customer, employee, store, product, sales, and returns datasets.

These findings provide an initial understanding of how the datasets may be connected and establish a basis for subsequent data cleaning, validation, and relational database design.

All relationships remain subject to verification before implementation in the final database.
