# Products Dataset — Data Quality Investigation

## 1. Dataset Overview

**Source file:** `products.csv`  
**Records:** 20  
**Columns:** 5

The dataset contains:

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
=COUNTIF(A2:A21,"P*")
=COUNTUNIQUE(ARRAYFORMULA(LEN(A2:A21)))
=SUMPRODUCT(--REGEXMATCH(A2:A21,"[a-z]"))
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
=SUMPRODUCT(--(B2:B21<>TRIM(B2:B21)))
=SUMPRODUCT(--REGEXMATCH(B2:B21,"[a-z]"))
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
=COUNTA(E2:E21)-COUNT(E2:E21)
=MIN(E2:E21)
=MAX(E2:E21)
=SUMPRODUCT(--(MOD(E2:E21,1)<>0))
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

**Finding:** Repeated prices were found among several products. These were not treated as duplicate product records because different products can legitimately have the same unit price. No evidence indicated that these records represented duplicate products.

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

### 6.1 Category Reference Validation

A category reference containing the following six category labels was available for comparison:

| Category | Description |
|---|---|
| Electronics | Technology and electronic goods |
| Appliances | Household appliances |
| Clothing | Apparel |
| Stationery | Office and school supplies |
| Household | Cleaning and household consumables |
| Home | Home and living products |

The observed category values were compared against these reference labels.

**Findings:**

- `Electronics`, `Appliances`, `Clothing`, `Stationery`, `Household`, and `Home` match the reference.
- `Electronic` does not match the reference label `Electronics`.
- `electronics` also does not match the reference because of its lowercase formatting.

The variations `Electronic` and `electronics` are likely inconsistent versions or possible typing errors involving the intended `Electronics` label. This is a probable explanation rather than a confirmed correction.

### 6.2 Category and Subcategory Inconsistencies

The investigation identified several products sharing the same subcategory but having different parent categories:

- P004 and P005 share `Computer Accessories`, but their categories are `Electronic` and `Electronics`.
- P006 and P007 share `Kitchen Appliances`, but their categories are `electronics` and `Appliances`.
- P016 and P017 share `Cleaning`, but their categories are `Electronic` and `Household`.

These differences raise category consistency concerns. However, the correct parent category cannot be established solely from the shared subcategory without confirmed business classification rules.

No automatic category replacements were made.

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

**Formatting formulas:**

```excel
=SUMPRODUCT(--(C2:C21<>TRIM(C2:C21)))
=SUMPRODUCT(--(D2:D21<>TRIM(D2:D21)))
```

**Finding:** No leading or trailing spaces were identified in either the category or subcategory values.

### 7.1 Category and Subcategory Relationship Check

The investigation examined whether products sharing a subcategory were consistently assigned to the same category.

**Formulas used:**

```excel
=COUNTIF($D$2:$D$21,G1)
=IFERROR(COUNTUNIQUE(FILTER($C$2:$C$21,$D$2:$D$21=G1)),0)
```

Three subcategories were identified as appearing under more than one category:

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
| P004 | Logitech Wireless Mouse | Electronic | Computer Accessories | Category does not match reference; differs from P005 |
| P005 | HP Wireless Keyboard | Electronics | Computer Accessories | Matches reference; differs from P004 |
| P006 | Defy Microwave 20L | electronics | Kitchen Appliances | Category does not match reference; differs from P007 |
| P007 | Russell Hobbs Kettle | Appliances | Kitchen Appliances | Matches reference; differs from P006 |
| P016 | Laundry Detergent 2L | Electronic | Cleaning | Category does not match reference; potential misclassification |
| P017 | Dishwashing Liquid 750ml | Household | Cleaning | Matches reference; different parent from P016 |
| P020 | Non-stick Frying Pan | Electronic | Cookware | Category does not match reference; potential misclassification |

The recorded values were checked against the original `products.csv` and matched the source file.

No confirmed product-category corrections were established during Phase 3.

## 9. Investigation Findings and Decisions

| Area investigated | Finding |
|---|---|
| Missing values | No missing values |
| Product IDs | Unique and consistently formatted |
| Product names | Unique, with no identified spacing issues |
| Unit prices | Numeric, with no zero or fractional values |
| Duplicate prices | Repeated prices found, but no evidence of duplicate products |
| Categories | Two category-label variations do not match the supplied reference |
| Subcategories | 15 distinct values; no spacing issues |
| Category relationships | Three subcategories occur under multiple categories |
| Source traceability | Investigated values match the original CSV |

The following decisions were made:

1. Original category and subcategory values remain unchanged during Phase 3.
2. `Electronic` and `electronics` are documented as probable inconsistent versions of `Electronics`.
3. The four products with category values that do not match the reference are flagged for review.
4. P016 and P020 require particular attention because their recorded categories may also indicate classification problems.
5. The relationships involving `Computer Accessories`, `Kitchen Appliances`, and `Cleaning` remain subject to review.
6. No category hierarchy or replacement values will be invented without business confirmation.
7. Repeated unit prices will not be treated as duplicate products without additional evidence.

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

- Review and standardise category labels against the supplied category reference.
- Confirm whether `Electronic` and `electronics` should be standardised to `Electronics`.
- Confirm the intended classifications of P016 and P020.
- Establish whether each subcategory must belong to one parent category.
- Preserve original source values and document all approved transformations.
- Maintain traceability between original and cleaned product records.

No changes were made to the original `products.csv` during Phase 3.

## 12. Conclusion

The Products dataset contains 20 complete product records with unique identifiers and product names. Unit prices are consistently numeric, and no missing values or duplicate product records were established.

The main data-quality concern is inconsistent product categorisation. Comparison with the supplied category reference identified two category-label variations that do not match the reference. These are likely naming or typing inconsistencies, but the intended classifications of individual products still require review.

The dataset's structural and basic validity checks were satisfactory. The identified category concerns have been documented for resolution during Phase 4.
