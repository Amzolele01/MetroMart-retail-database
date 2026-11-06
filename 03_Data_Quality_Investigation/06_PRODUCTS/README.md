## 1. Dataset Overview

**Source file:** `products.csv`  
**Records:** 20  
**Columns:** 5

The dataset contains the following columns:

| Column | Description |
|---|---|
| `product_id` | Unique identifier assigned to each product |
| `product_name` | Product name or description |
| `category` | General product classification |
| `subcategory` | More specific product classification |
| `unit_price` | Recorded unit selling price |

The investigation was conducted in Google Sheets using a working copy of the original CSV file. The original source file was preserved unchanged.

The objective was to assess the completeness, validity, consistency, and reliability of product information before proceeding to data cleaning and database design.

## 2. Missing Values Investigation

All five columns were checked for missing values.

**Formulas used:**

```excel
=COUNTBLANK(A2:A21)
=COUNTBLANK(B2:B21)
=COUNTBLANK(C2:C21)
=COUNTBLANK(D2:D21)
=COUNTBLANK(E2:E21)
```

**Results:**

| Column | Missing values |
|---|---:|
| `product_id` | 0 |
| `product_name` | 0 |
| `category` | 0 |
| `subcategory` | 0 |
| `unit_price` | 0 |
| **Total** | **0** |

**Finding:** No missing values were identified. All 20 product records contain values in every column.

## 3. Product ID Investigation

The product identifiers were checked for uniqueness, completeness, and formatting consistency.

**Formulas used:**

```excel
=COUNTUNIQUE(A2:A21)
```

```excel
=COUNTIF(A2:A21,"P*")
```

```excel
=COUNTUNIQUE(ARRAYFORMULA(LEN(A2:A21)))
```

```excel
=SUMPRODUCT(--REGEXMATCH(A2:A21,"[a-z]"))
```

```excel
=SUMPRODUCT(--(A2:A21<>TRIM(A2:A21)))
```

**Results:**

| Check | Result |
|---|---:|
| Total product records | 20 |
| Unique product IDs | 20 |
| IDs beginning with P | 20 |
| Different ID lengths | 1 |
| IDs containing lowercase letters | 0 |
| IDs with leading or trailing spaces | 0 |

**Finding:** All product IDs are unique and follow a consistent format. No missing, duplicate, or obvious formatting issues were identified.

## 4. Product Name Investigation

Product names were examined for uniqueness, inconsistent spacing, and basic capitalization patterns.

**Formulas used:**

```excel
=COUNTUNIQUE(B2:B21)
```

```excel
=SUMPRODUCT(--(B2:B21<>TRIM(B2:B21)))
```

```excel
=SUMPRODUCT(--REGEXMATCH(B2:B21,"[a-z]"))
```

```excel
=SUMPRODUCT(--REGEXMATCH(B2:B21,"  "))
```

**Results:**

| Check | Result |
|---|---:|
| Total product names | 20 |
| Unique product names | 20 |
| Names with leading or trailing spaces | 0 |
| Names containing lowercase letters | 20 |
| Names with consecutive spaces | 0 |

**Finding:** All product names are unique. No leading, trailing, or repeated spaces were identified. The names use mixed capitalization, which is not considered an issue by itself.

No product-name corrections were identified as necessary during this investigation.

## 5. Unit Price Investigation

The `unit_price` column was checked for numeric validity, text values, zero prices, fractional values, and the overall price range.

**Formulas used:**

```excel
=COUNT(E2:E21)
```

```excel
=COUNTA(E2:E21)-COUNT(E2:E21)
```

```excel
=MIN(E2:E21)
```

```excel
=MAX(E2:E21)
```

```excel
=SUMPRODUCT(--(MOD(E2:E21,1)<>0))
```

```excel
=COUNTIF(E2:E21,0)
```

**Results:**

| Check | Result |
|---|---:|
| Numeric values | 20 |
| Non-numeric values | 0 |
| Minimum price | R39 |
| Maximum price | R7,499 |
| Fractional values | 0 |
| Zero prices | 0 |

**Finding:** All 20 unit prices are numeric. No text values, zero prices, or fractional values were identified. The recorded prices range from R39 to R7,499.

These checks establish the format and basic validity of the prices. They do not independently confirm whether each price is commercially accurate or historically correct.

### 5.1 Duplicate Unit Prices

Repeated unit prices were also examined.

**Formula used:**

```excel
=FILTER(A2:E21,COUNTIF(E2:E21,E2:E21)>1)
```

Repeated prices were found among several products.

**Finding:** Repeated prices were not treated as duplicate product records. Different products can legitimately have the same unit price, and no evidence indicated that these records represented duplicate products.

## 6. Category Investigation

The category column was examined to identify distinct category labels, their frequency, and possible inconsistencies.

**Formula used:**

```excel
=QUERY(C2:C21,"SELECT C, COUNT(C) WHERE C IS NOT NULL GROUP BY C LABEL C 'Category', COUNT(C) 'Product Count'",0)
```

**Observed category distribution:**

| Category | Product count |
|---|---:|
| Appliances | 2 |
| Clothing | 2 |
| Electronic | 3 |
| Electronics | 4 |
| electronics | 3 |
| Home | 2 |
| Household | 1 |
| Stationery | 3 |
| **Total** | **20** |

### 6.1 Category Inconsistencies

The investigation identified several category labels that may represent inconsistent classification.

- `Electronic`, `Electronics`, and `electronics` appear to represent related or potentially identical category labels. They differ in singular/plural form and capitalization.
- Products P004 and P005 share the subcategory `Computer Accessories`, but their parent categories are recorded as `Electronic` and `Electronics`.
- Products P006 and P007 share the subcategory `Kitchen Appliances`, but their parent categories are `electronics` and `Appliances`.
- Products P016 and P017 share the subcategory `Cleaning`, but their parent categories are `Electronic` and `Household`.

These differences were recorded as category consistency concerns. However, no approved category definitions or classification hierarchy were supplied to establish the intended values.

The investigation therefore did not automatically merge or replace category labels.

## 7. Subcategory Investigation

The subcategory column was checked for distinct values, distribution, formatting consistency, and relationships with the category column.

**Distinct subcategories:** 15.

| Subcategory | Product count |
|---|---:|
| Audio | 1 |
| Bags | 1 |
| Cables | 2 |
| Cleaning | 2 |
| Computer Accessories | 2 |
| Cookware | 1 |
| Electrical | 1 |
| Kitchen Appliances | 2 |
| Laundry | 1 |
| Lighting | 1 |
| Menswear | 2 |
| Mobile Phones | 1 |
| Paper | 1 |
| Television | 1 |
| Writing | 1 |
| **Total** | **20** |

**Formatting checks:**

```excel
=SUMPRODUCT(--(C2:C21<>TRIM(C2:C21)))
```

```excel
=SUMPRODUCT(--(D2:D21<>TRIM(D2:D21)))
```

**Results:** No leading or trailing spaces were identified in either the category or subcategory values.

### 7.1 Category and Subcategory Relationship Check

The investigation also examined whether products sharing a subcategory were consistently assigned to the same category.

The working summary used the following formulas:

```excel
=COUNTIF($D$2:$D$21,G1)
```

```excel
=IFERROR(COUNTUNIQUE(FILTER($C$2:$C$21,$D$2:$D$21=G1)),0)
```

The results identified three subcategories associated with more than one category:

| Subcategory | Product count | Distinct category count |
|---|---:|---:|
| Computer Accessories | 2 | 2 |
| Kitchen Appliances | 2 | 2 |
| Cleaning | 2 | 2 |

**Finding:** These relationships require review before a consistent category structure can be established. However, a subcategory appearing under multiple categories is not automatically invalid unless the business defines subcategories as belonging to only one parent category.

## 8. Records Requiring Further Review

The following records were identified as particularly relevant to the category consistency investigation.

| Product ID | Product | Recorded category | Subcategory | Observation |
|---|---|---|---|---|
| P004 | Logitech Wireless Mouse | Electronic | Computer Accessories | Category differs from P005 |
| P005 | HP Wireless Keyboard | Electronics | Computer Accessories | Category differs from P004 |
| P006 | Defy Microwave 20L | electronics | Kitchen Appliances | Category differs from P007 |
| P007 | Russell Hobbs Kettle | Appliances | Kitchen Appliances | Category differs from P006 |
| P016 | Laundry Detergent 2L | Electronic | Cleaning | Potential category misclassification |
| P017 | Dishwashing Liquid 750ml | Household | Cleaning | Different parent category from P016 |
| P020 | Non-stick Frying Pan | Electronic | Cookware | Potential category misclassification |

These records were checked against the original `products.csv`. Their values match the source file, confirming that the observed category values were not introduced through changes to the working copy.

No authoritative category reference file or historical product catalogue was identified to confirm the intended classifications.

## 9. Investigation Findings

The investigation produced the following results:

| Area investigated | Finding |
|---|---|
| Missing values | No missing values |
| Product IDs | Unique and consistently formatted |
| Product names | Unique, with no identified spacing issues |
| Unit prices | Numeric and without zero or fractional values |
| Duplicate prices | Repeated prices found, but no evidence of duplicate products |
| Categories | Inconsistent capitalization and naming |
| Subcategories | 15 distinct values; no spacing issues |
| Category relationships | Three subcategories occur under multiple categories |
| Source traceability | Investigated category values match the original CSV |

### 9.1 Data Quality Issues and Decisions

The main concern identified is inconsistent product categorisation.

The following decisions were made:

1. Original category and subcategory values will remain unchanged during this investigation.
2. `Electronic`, `Electronics`, and `electronics` will be recorded as potentially inconsistent labels.
3. P016 and P020 will be flagged for further classification review.
4. The category relationships involving `Computer Accessories`, `Kitchen Appliances`, and `Cleaning` will be reviewed during the cleaning phase.
5. No category hierarchy or replacement values will be invented without business confirmation.
6. Repeated unit prices will not be treated as duplicate products without additional evidence.

## 10. Business Requirements Relevance

The findings relate to the following business requirements:

- **BR-02:** Maintain a consistent product catalogue.
- **BR-05:** Support product-level analysis.
- **BR-07:** Preserve traceability from cleaned records back to source where practical.
- **BR-08:** Prevent invalid relational records in the final database.
- **BR-10:** Document important cleaning and modelling decisions.

Inconsistent category labels could affect product grouping, category-level reporting, and future database classification rules.

## 11. Phase 4 Considerations

The following items should be carried forward into the cleaning and validation phase:

- Review category naming and capitalization.
- Establish whether `Electronic`, `Electronics`, and `electronics` should be standardised.
- Confirm the intended classification of P016 and P020.
- Establish whether each subcategory must belong to one parent category.
- Preserve original source values and document any approved transformations.

No changes were made to the original `products.csv` during Phase 3.

## 12. Conclusion

The Products dataset contains 20 complete product records with unique identifiers and product names. Unit prices are consistently numeric, and no missing values or duplicate product records were established.

The main data-quality concern is inconsistent product categorisation. These inconsistencies may affect catalogue consistency and product-level reporting, but their intended corrections cannot be established without business confirmation.

The dataset is therefore considered suitable for progression to the next investigation stage, with the identified category concerns retained for Phase 4 review.
