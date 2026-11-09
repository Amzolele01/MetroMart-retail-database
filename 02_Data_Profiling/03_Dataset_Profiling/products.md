# Products Dataset Profile

## 1. Dataset Overview

The `products` dataset contains MetroMart's product catalogue, including product identifiers, names, categories, subcategories, and unit prices.

The dataset was profiled to understand its structure, completeness, uniqueness, product classification, and pricing information.

| Attribute | Details |
|---|---|
| Dataset | `products` |
| Total records | 20 |
| Total fields | 5 |
| Profiling tool | Google Sheets |

## 2. Field-Level Profile

The following table summarises the initial profiling results.

| Field | Data Type | Total Records | Missing Values | Unique Values |
|---|---|---:|---:|---:|
| `product_id` | String | 20 | 0 | 20 |
| `product_name` | String | 20 | 0 | 20 |
| `category` | String | 20 | 0 | 8 |
| `subcategory` | String | 20 | 0 | 15 |
| `unit_price` | String | 20 | 0 | 17 |

## 3. Initial Profiling Observations

### 3.1 Product Identifier (`product_id`)

- All 20 records contain a product identifier.
- No missing values were identified.
- All 20 identifiers are unique.

**Observation:** Each product record has a distinct identifier. Based on the initial profiling results, `product_id` is a potential primary key.

### 3.2 Product Name (`product_name`)

- All 20 records contain a product name.
- No missing values were identified.
- All 20 product names are unique.

**Observation:** Every product has a distinct recorded name. No repeated product names were identified during initial profiling.

### 3.3 Category (`category`)

- All 20 records contain a category value.
- No missing values were identified.
- Eight distinct category values were identified in the original field values.
- A preliminary grouping exercise indicated six categories after accounting for differences in letter casing.

**Observation:** The category field contains inconsistent representations of some category names. For example, `Electronics`, `electronics`, and `Electronic` appear as separate values in the original data.

These variations may represent inconsistent naming rather than genuinely different product categories.

### 3.4 Subcategory (`subcategory`)

- All 20 records contain a subcategory value.
- No missing values were identified.
- Fifteen unique subcategory values were identified.

**Observation:** The dataset contains a range of product subcategories. Some category and subcategory combinations appear questionable based on their recorded descriptions.

Examples include:

- Product `P016`: `Electronic` category with `Cleaning` subcategory.
- Product `P020`: `Electronic` category with `Cookware` subcategory.

These combinations were recorded for further consideration rather than classified as confirmed errors during initial profiling.

### 3.5 Unit Price (`unit_price`)

- All 20 records contain a unit price.
- No missing values were identified.
- Seventeen unique price values were identified.

**Observation:** The dataset contains 17 distinct unit prices across 20 products. Some prices are shared by multiple products.

Repeated prices are not necessarily unusual, as different products may have the same selling price.

The source field was recorded as a string during initial profiling. Its suitability for numerical database storage will be considered during subsequent data preparation and database design.

## 4. Profiling Summary

The initial profiling established the following characteristics:

- The dataset contains 20 records across five fields.
- All product identifiers are populated and unique.
- All product names are populated and unique.
- The category field contains eight original distinct values, with some variations in naming and letter casing.
- Fifteen unique subcategories were identified.
- Some category and subcategory combinations appear questionable.
- The unit price field contains 17 unique values.
- No missing values were identified in any of the five fields.

## 5. Profiling Conclusion

The `products` dataset provides the initial product catalogue for MetroMart, with complete records across all five fields.

Product identifiers and product names are unique within the dataset, making `product_id` a potential primary key.

The main observations concern product classification and field representation. Differences in category naming and questionable category-subcategory combinations may require attention during the data quality investigation.

The unit price field was recorded as a string during profiling. Its appropriate representation will be considered during database preparation.

No changes were made to the original source data during profiling.
