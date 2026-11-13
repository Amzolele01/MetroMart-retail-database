# MetroMart Retail Database Project – Relationship Discovery

## 1. Purpose

This document records the structural and potential relational connections identified across the MetroMart source datasets during data profiling.

The purpose of relationship discovery is to establish how records across different datasets may be connected, identify potential primary and foreign keys, and provide a foundation for subsequent data quality investigation and relational database design.

The discovery process considers:

- Dataset attributes and identifier fields.
- Potential primary-key candidates.
- Potential foreign-key references.
- Relationships between operational datasets.
- Legacy customer records and possible customer duplication.
- Reference datasets that may support identifier standardisation.
- Potential referential integrity issues.

The relationships documented here are preliminary findings. Their validity must be established through actual identifier comparisons, relationship testing and business-context evaluation.

No database constraints or source-data modifications are implied by this document.

## 2. Source Dataset Inventory

The project contains seven primary source datasets.

### 2.1 Customers

**Source file:** `customers.csv`

| Attribute | Description |
|---|---|
| `customer_id` | Customer identifier |
| `customer_name` | Customer's recorded name |
| `phone` | Customer contact number |
| `email` | Customer email address |
| `city` | Customer's recorded city |
| `province` | Customer's recorded province |

**Identifier observation:**

The dataset contains two customer ID formats:

- `C####` – standard-format identifiers.
- `C#X##` – legacy-style identifiers.

The investigation identified 20 legacy-format customer records. Each has a corresponding standard-format customer record with matching customer details, including phone numbers after formatting differences are accounted for.

These records are considered strong potential duplicates and require relationship and transaction-reference validation before consolidation.

### 2.2 Legacy Customer Export

**Source file:** `customer_export_legacy.csv`

| Attribute | Description |
|---|---|
| `cust_no` | Customer reference number |
| `full_name` | Customer's full name |
| `contact_number` | Customer contact number |
| `city` | Customer's recorded city |

**Identifier observation:**

The dataset uses the `C####` identifier format.

The different identifier field name (`cust_no`) requires investigation before establishing whether it directly corresponds to `customers.customer_id`.

The dataset may contain customer records that overlap with the main customer dataset. Matching should consider available customer attributes rather than relying exclusively on identifier equality.

### 2.3 Employees

**Source file:** `employees.csv`

The dataset contains employee records, including employee identifiers, names, store assignments and roles.

The exact attribute inventory still requires confirmation in this document.

The previously identified relationship candidates include:

- Employee identifier: `employee_id`.
- Store reference: `store_id`.

The employee-to-store relationship requires validation against `stores.store_code`.

### 2.4 Stores

**Source file:** `stores.csv`

| Attribute | Description |
|---|---|
| `store_code` | Store identifier |
| `store_name` | Store name |
| `city` | Store location |
| `province` | Store province |

**Identifier observation:**

The investigation identified five store records with five unique store codes and five unique store names.

The store dataset is a potential reference point for employee and sales store assignments.

### 2.5 Products

**Source file:** `products.xlsx`

| Attribute | Description |
|---|---|
| `product_id` | Product identifier |
| `product_name` | Product name |
| `category` | Product category |
| `subcategory` | Product subcategory |
| `unit_price` | Recorded product unit price |

**Identifier observation:**

`product_id` is a potential primary-key candidate.

The product dataset is referenced by sales and returns records and may also be supported by the product category reference file.

### 2.6 Sales Transactions

**Source file:** `sales_2023_2025.csv`

| Attribute | Description |
|---|---|
| `transaction_id` | Transaction identifier |
| `transaction_date` | Date and time of the transaction |
| `customer_id` | Customer identifier |
| `store_id` | Store identifier |
| `employee_id` | Employee identifier |
| `product_id` | Product identifier |
| `quantity` | Quantity recorded in the transaction |
| `unit_price` | Recorded selling price per unit |
| `discount_pct` | Applied discount percentage |
| `total_amount` | Recorded transaction line amount |

**Important structural observation:**

The actual supplied sales dataset contains a `customer_id` attribute.

This corrects an earlier observation that the sales dataset did not contain a customer reference.

Consequently, a direct potential relationship between sales and customers can be investigated.

The transaction structure must also be examined to establish whether `transaction_id` uniquely identifies each row or whether a transaction can contain multiple product records.

This distinction will affect the eventual relational database design.

### 2.7 Returns

**Source file:** `returns.csv`

| Attribute | Description |
|---|---|
| `return_id` | Return record identifier |
| `transaction_id` | Associated sales transaction identifier |
| `customer_id` | Customer identifier |
| `product_id` | Returned product identifier |
| `quantity_returned` | Quantity returned |
| `return_date` | Date of return |
| `reason` | Recorded return reason |

**Structural observation:**

The returns dataset contains references to customers, products and sales transactions.

These references provide opportunities to examine whether return records are consistent with their corresponding sales records.

## 3. Potential Primary Keys and Identifiers

The following fields are candidates for identifying records within their respective datasets.

| Dataset | Candidate identifier | Current assessment |
|---|---|---|
| Customers | `customer_id` | Unique in the investigated source |
| Customer export legacy | `cust_no` | Requires uniqueness and matching validation |
| Employees | `employee_id` | Previously identified as unique |
| Stores | `store_code` | Five unique identifiers |
| Products | `product_id` | Requires final uniqueness confirmation |
| Sales | `transaction_id` | Requires uniqueness and transaction-structure investigation |
| Returns | `return_id` | Requires final uniqueness confirmation |

A candidate identifier should only be accepted as a primary key after its uniqueness, completeness and suitability have been established.

In particular, the sales transaction identifier must not automatically be treated as a row-level primary key without examining the transaction structure.

## 4. Identified Potential Relationships

The following relationships have been identified from the source structures and preliminary profiling.

### 4.1 Employee-to-Store Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Employees | `store_id` | Stores | `store_code` |

**Purpose:**

Associates employees with their assigned stores.

**Validation requirements:**

- Confirm that employee store references exist in the stores dataset.
- Identify unmatched store references.
- Examine whether each employee is assigned to one store or whether multiple assignments are possible.

### 4.2 Sales-to-Customer Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Sales | `customer_id` | Customers | `customer_id` |

**Purpose:**

Associates sales records with the customers involved in the transactions.

**Validation requirements:**

- Check whether every sales customer ID exists in the customers dataset.
- Identify unmatched customer references.
- Examine the occurrence of legacy-format customer IDs.
- Establish whether customer records can be safely consolidated without affecting sales references.

This relationship is particularly important for the investigation of the 20 potential duplicate customer pairs.

### 4.3 Sales-to-Store Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Sales | `store_id` | Stores | `store_code` |

**Purpose:**

Associates sales records with the stores where transactions occurred.

**Validation requirements:**

- Compare sales store IDs against available store codes.
- Identify unmatched references.
- Examine whether store-code inconsistencies affect matching.

### 4.4 Sales-to-Employee Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Sales | `employee_id` | Employees | `employee_id` |

**Purpose:**

Associates sales records with the employees responsible for recording or processing transactions.

**Validation requirements:**

- Check whether sales employee IDs exist in the employee dataset.
- Identify unmatched references.
- Examine whether employee store assignments are consistent with sales store references.

### 4.5 Sales-to-Product Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Sales | `product_id` | Products | `product_id` |

**Purpose:**

Identifies the products recorded in individual sales records.

**Validation requirements:**

- Compare sales product IDs against product identifiers.
- Identify unmatched product references.
- Examine consistency between recorded sales prices and product reference prices where business rules permit.

### 4.6 Returns-to-Sales Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Returns | `transaction_id` | Sales | `transaction_id` |

**Purpose:**

Connects return records to their associated sales transactions.

**Validation requirements:**

- Confirm that return transaction IDs exist in the sales dataset.
- Identify returns without corresponding sales transactions.
- Determine whether multiple return records can reference one transaction.
- Compare returned products against products recorded in the associated transaction.
- Examine returned quantities against original quantities sold.

Because sales records contain product-level information, transaction and product references should be examined together when validating the returned item.

### 4.7 Returns-to-Customer Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Returns | `customer_id` | Customers | `customer_id` |

**Purpose:**

Associates return records with the customers recorded as making the returns.

**Validation requirements:**

- Confirm that return customer IDs exist in the customers dataset.
- Identify unmatched customer references.
- Compare return customer IDs with the customer IDs recorded in their associated sales transactions.

A return should not automatically be accepted as correctly associated with a transaction simply because its transaction ID exists.

### 4.8 Returns-to-Product Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Returns | `product_id` | Products | `product_id` |

**Purpose:**

Identifies the products associated with return records.

**Validation requirements:**

- Confirm that returned product IDs exist in the products dataset.
- Identify unmatched product references.
- Compare returned product IDs with the products recorded in the associated sales transactions.

### 4.9 Legacy Customer Export-to-Main Customers Relationship

| Source dataset | Source field | Target dataset | Target field |
|---|---|---|---|
| Customer export legacy | `cust_no` | Customers | `customer_id` |

**Purpose:**

Investigates whether records from the legacy customer export correspond to records in the main customer dataset.

**Validation requirements:**

- Compare customer identifiers.
- Identify matching and unmatched identifiers.
- Compare names and contact numbers.
- Examine possible duplicate customer records.
- Establish whether the legacy export represents an independent customer source or an earlier version of the main customer data.

This relationship remains a proposed connection rather than an established foreign-key relationship.

The two fields have different names, and matching identifier formats alone do not establish that they have identical business meaning.

## 5. Additional Relationship and Data Integration Considerations

### 5.1 Legacy Customer ID Investigation

The customers investigation identified 20 records using the legacy-style `C#X##` identifier format.

Each of these records has a corresponding standard-format `C####` record.

The 20 pairs exhibit the following characteristics:

- Matching customer names.
- Matching email addresses.
- Matching phone numbers after formatting differences are removed.
- Matching cities.
- Matching provinces.
- Different customer identifiers.

All 20 duplicated-email groups contain exactly two records, with one standard-format ID and one legacy-format ID.

The `customer_export_legacy.csv` dataset uses only the standard `C####` identifier format.

The user has also confirmed that the other source files use the standard identifier format.

These observations suggest that the 20 legacy-format records may represent duplicate customer entries introduced through a separate data integration or migration process.

However, their exact origin has not been established.

**Implications for database design and cleaning:**

Before consolidating these records, the following checks are required:

1. Determine whether any of the 20 legacy IDs appear in sales records.
2. Determine whether any of the 20 legacy IDs appear in returns records.
3. Confirm that the corresponding standard IDs are referenced correctly.
4. Establish whether all 20 pairs can be mapped without disrupting historical transaction references.
5. Maintain a record of original and retained identifiers if consolidation is approved.

The standard-format ID may be considered the proposed retained identifier for each confirmed duplicate pair, subject to successful relationship validation.

The original customer identifiers must remain traceable.

### 5.2 Customer Export and Returns

The existing relationship investigation proposed a possible connection between:

`customer_export_legacy.cust_no` and `returns.customer_id`.

This connection requires further examination.

Since both fields contain customer identifiers, their values may be comparable. However, the relationship should only be accepted if the identifiers and associated customer records demonstrate a valid correspondence.

The customer export should not automatically be treated as a parent table for returns.

### 5.3 Sales and Returns Consistency

The returns dataset contains `transaction_id`, `customer_id` and `product_id`.

These fields should be examined together against the corresponding sales records.

The investigation should establish:

- Whether the referenced transaction exists.
- Whether the customer matches the transaction customer.
- Whether the returned product was recorded in that transaction.
- Whether the returned quantity is consistent with the quantity sold.
- Whether multiple return records are associated with the same transaction or product.

This will help establish whether the returns dataset maintains consistent references to the original sales activity.

## 6. Reference Datasets

In addition to the seven primary datasets, the project contains two reference files.

### 6.1 Product Categories

**Source file:** `product_categories.xlsx`

This reference file provides product category information.

It should be examined to establish whether the category and subcategory values in `products.xlsx` correspond to an approved or recognised category structure.

Potential validation areas include:

- Category naming consistency.
- Subcategory naming consistency.
- Unrecognised category values.
- Potential category-to-subcategory relationships.

No direct foreign-key relationship should be assumed until the reference structure and matching rules are established.

### 6.2 Store Codes

**Source file:** `store_codes.csv`

This reference file provides store-code information.

It should be examined against `stores.store_code` and store references appearing in employee and sales records.

Potential validation areas include:

- Matching store codes.
- Unrecognised store codes.
- Differences in code representation.
- Potential historical store-code mappings.

The reference file should not automatically be treated as an additional store entity table. Its actual structure and business purpose must first be established.

## 7. Relationship Validation Framework

The proposed relationships must be examined through systematic validation.

The following checks will be used where applicable.

### 7.1 Identifier Matching

Compare source identifiers against their potential target identifiers.

The objective is to establish whether the referenced records exist.

### 7.2 Referential Integrity

Identify:

- Matched references.
- Unmatched references.
- Missing references.
- Duplicate identifiers in potential parent datasets.

### 7.3 Relationship Cardinality

Establish the expected relationship structure.

Examples include:

- One store to many employees.
- One store to many sales records.
- One employee to many sales records.
- One product to many sales records.
- One customer to many sales records.
- One sales transaction to potentially multiple return records.

Actual cardinality must be determined from the data and business requirements.

### 7.4 Cross-Dataset Attribute Consistency

Where multiple datasets contain related identifiers, compare their associated attributes.

Examples include:

- Employee store assignments against sales store references.
- Return customer identifiers against sales customer identifiers.
- Return product identifiers against sales product identifiers.
- Customer identifiers across the main and legacy customer datasets.

### 7.5 Identifier Standardisation

Where identifiers appear in different formats, determine whether differences are purely representational or indicate separate identifier systems.

Identifiers should not be modified merely to make their formats consistent.

Any proposed mapping must preserve the original identifier and maintain traceability.

## 8. Outstanding Investigation Items

The following items require additional evidence before the relationship discovery stage can be considered complete.

| Investigation item | Status |
|---|---|
| Confirm exact employee attribute inventory | Pending |
| Validate employee-to-store references | Requires validation |
| Validate sales-to-customer references | Requires validation |
| Validate sales-to-store references | Requires validation |
| Validate sales-to-employee references | Requires validation |
| Validate sales-to-product references | Requires validation |
| Validate returns-to-sales references | Requires validation |
| Validate returns-to-customer references | Requires validation |
| Validate returns-to-product references | Requires validation |
| Investigate legacy customer ID references | Requires validation |
| Compare legacy customer export with main customers | Requires validation |
| Examine product category reference structure | Requires validation |
| Examine store-code reference structure | Requires validation |
| Establish transaction identifier uniqueness and structure | Requires validation |

## 9. Summary

Initial relationship discovery has identified potential connections across the seven primary MetroMart datasets.

The most significant relationships involve:

- Employees and stores.
- Sales and customers.
- Sales and stores.
- Sales and employees.
- Sales and products.
- Returns and sales transactions.
- Returns and customers.
- Returns and products.
- Legacy customer records and the main customer dataset.

The discovery also identified an important customer data issue involving 20 legacy-format customer IDs and 20 corresponding standard-format records.

These records appear to represent potential duplicate customers, but consolidation must remain subject to transaction-reference validation.

The actual sales dataset contains a `customer_id` field, correcting an earlier structural observation and enabling direct investigation of the sales-to-customer relationship.

The reference datasets provide additional opportunities for validating product categories and store identifiers.

All proposed relationships remain subject to validation. Their final acceptance, cardinalities and database constraints will be established through subsequent investigation and relational database design.

**The original source datasets will remain unchanged. Any eventual data cleaning, identifier mapping or consolidation will be performed on separate working copies with appropriate documentation and traceability.**
