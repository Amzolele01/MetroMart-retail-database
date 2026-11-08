# Customer Export Legacy — Data Quality Investigation

## 1. Dataset Overview

**Source file:** `customer_export_legacy.csv`  
**Investigation phase:** Phase 3 — Data Quality Investigation  
**Records:** 350  
**Columns:** 4

The dataset contains legacy customer information with the following columns:

| Column | Description |
|---|---|
| `cust_no` | Customer identifier |
| `full_name` | Customer's full name |
| `contact_number` | Customer contact number |
| `city` | Customer's city |

Each row represents one customer record.

## 2. Structure and Completeness

The dataset contains 350 records and four columns.

The record count was checked using:

```excel
=COUNTA(A2:A)
```

### Missing-value investigation

The following formulas were used:

```excel
=COUNTBLANK(A2:A351)
=COUNTBLANK(B2:B351)
=COUNTBLANK(C2:C351)
=COUNTBLANK(D2:D351)
```

| Column | Missing values |
|---|---:|
| `cust_no` | 0 |
| `full_name` | 0 |
| `contact_number` | 0 |
| `city` | 0 |

**Finding:** No missing values were identified in the four columns.

## 3. Customer Identifier Investigation

The `cust_no` column was checked for uniqueness, format consistency and identifier range.

### Uniqueness

Formulas:

```excel
=COUNTA(A2:A351)
=COUNTUNIQUE(A2:A351)
=COUNTA(A2:A351)-COUNTUNIQUE(A2:A351)
```

| Measurement | Result |
|---|---:|
| Total customer IDs | 350 |
| Unique customer IDs | 350 |
| Duplicate occurrences | 0 |

**Finding:** All 350 customer identifiers are unique.

### Identifier format and range

Format check:

```excel
=COUNTIF(A2:A351,"C????")
```

Result: 350.

Minimum numeric identifier:

```excel
=MIN(ARRAYFORMULA(VALUE(REGEXEXTRACT(A2:A351,"\d+"))))
```

Result: 4.

Maximum numeric identifier:

```excel
=MAX(ARRAYFORMULA(VALUE(REGEXEXTRACT(A2:A351,"\d+"))))
```

Result: 1190.

**Finding:** All identifiers follow the `C` followed by four digits format. The numeric identifier range is C0004 to C1190. The range does not imply that every identifier between these values exists in the dataset.

## 4. Full Name Investigation

The `full_name` column was examined for repeated names.

Formulas:

```excel
=COUNTUNIQUE(B2:B351)
```

```excel
=COUNTA(B2:B351)-COUNTUNIQUE(B2:B351)
```

| Measurement | Result |
|---|---:|
| Total records | 350 |
| Unique full names | 182 |
| Excess repeated occurrences | 168 |

Repeated names were extracted using:

```excel
=UNIQUE(FILTER(B2:B351,COUNTIF(B2:B351,B2:B351)>1))
```

The investigation identified multiple occurrences of the same names, including examples such as Kagiso Mabena and Mpho Van Wyk.

Repeated names alone do not establish duplicate customer records. Different customers may share the same name.

## 5. Contact Number Investigation

The contact numbers were checked for uniqueness, completeness and length.

### Uniqueness

```excel
=COUNTUNIQUE(C2:C351)
```

```excel
=COUNTA(C2:C351)-COUNTUNIQUE(C2:C351)
```

Results:

- Unique contact numbers: 350
- Excess repeated occurrences: 0

No repeated contact numbers were identified.

### Length and numeric values

```excel
=COUNTIF(ARRAYFORMULA(LEN(TO_TEXT(C2:C351))),9)
```

Result: 350.

```excel
=COUNT(C2:C351)
```

Result: 350.

To identify values with a different length:

```excel
=FILTER(A2:C351,LEN(TO_TEXT(C2:C351))<>9)
```

The formula returned `#N/A`, indicating that no records matched the condition.

**Finding:** All 350 contact numbers are numeric, unique and exactly nine digits long.

The numbers appear to be missing the leading zero commonly used in South African mobile-number formatting. This was recorded as a formatting observation, not changed during the investigation.

## 6. Full Name and City Combination Investigation

The combination of `full_name` and `city` was examined to identify repeated name-and-city pairs.

Unique combinations:

```excel
=COUNTUNIQUE(ARRAYFORMULA(B2:B351&"|"&D2:D351))
```

Result: 309.

Excess repeated occurrences:

```excel
=COUNTA(B2:B351)-COUNTUNIQUE(ARRAYFORMULA(B2:B351&"|"&D2:D351))
```

Result: 41.

Repeated combinations were extracted using:

```excel
=UNIQUE(FILTER(B2:B351&" | "&D2:D351,COUNTIF(B2:B351&"|"&D2:D351,B2:B351&"|"&D2:D351)>1))
```

Their frequencies were checked using:

```excel
=COUNTIFS($B$2:$B$351,TRIM(LEFT(I2,FIND("|",I2)-1)),$D$2:$D$351,TRIM(MID(I2,FIND("|",I2)+1,LEN(I2))))
```

The frequency results were also used to calculate the total excess occurrences:

```excel
=SUM(J2:J37)-COUNTA(J2:J37)
```

This returned 41, agreeing with the aggregate calculation.

**Finding:** There are 309 unique full-name-and-city combinations, with 41 excess repeated occurrences.

These combinations are not automatically duplicate records. An example investigated was:

| Customer ID | Full name | Contact number | City |
|---|---|---|---|
| C1074 | David Mabena | 843629729 | Sandton |
| C0729 | David Mabena | 788909809 | Sandton |

The records have different customer identifiers and different contact numbers.

No records were classified as confirmed duplicate customers based solely on repeated names and cities.

## 7. City Investigation

The city column was examined for distinct values, record distribution and whitespace inconsistencies.

Formula:

```excel
=QUERY(D2:D351,"SELECT D, COUNT(D) WHERE D IS NOT NULL GROUP BY D LABEL D 'City', COUNT(D) 'Records'",0)
```

### City distribution

| City | Records |
|---|---:|
| Fourways | 54 |
| Johannesburg | 37 |
| Midrand | 52 |
| Randburg | 44 |
| Roodepoort | 53 |
| Sandton | 56 |
| Soweto | 54 |
| **Total** | **350** |

Whitespace check:

```excel
=SUMPRODUCT(ARRAYFORMULA(--(D2:D351<>TRIM(D2:D351))))
```

Result: 0.

**Finding:** Seven city labels were identified. All 350 records were accounted for. No leading or trailing whitespace was detected, and no inconsistent city spelling or abbreviation was identified in this dataset.

## 8. Cross-Dataset Customer Reference Validation

Customer identifiers in Sales were compared against both customer datasets:

- `customer_export_legacy.csv`
- `customers.csv`

### Comparison with the legacy dataset

The Sales dataset contained 848 unique customer IDs that were not present in the legacy dataset.

The comparison formula was:

```excel
=FILTER(E1:E,E1:E<>"",COUNTIF($A$2:$A$351,E1:E)=0)
```

### Comparison with the main customer dataset

The main `customers` dataset contained 1,220 unique customer IDs in the imported reference range.

The Sales IDs absent from the legacy dataset were then compared against the main customer dataset.

Final comparison formula:

```excel
=FILTER(F1:F,F1:F<>"",COUNTIF($G$1:$G$1220,F1:F)=0)
```

Result: `C0012`.

The final result was counted using:

```excel
=COUNTIF(H1:H,"C*")
```

Result: 1.

### Confirmed unmatched reference

| Customer ID | Sales records referencing the ID | Found in legacy dataset | Found in main dataset |
|---|---:|---|---|
| C0012 | 87 | No | No |

**Finding:** `C0012` is referenced in 87 Sales records but is absent from both customer datasets. This is a confirmed unmatched customer reference and a referential integrity issue requiring investigation.

No customer record was created or altered to resolve this finding.

## 9. Summary of Findings

| Investigation area | Finding |
|---|---|
| Dataset structure | 350 records, 4 columns |
| Missing values | None |
| Customer ID uniqueness | 350 unique IDs |
| Customer ID format | Consistent C + 4 digits |
| Full-name duplication | 182 unique names; 168 excess occurrences |
| Contact number uniqueness | All 350 unique |
| Contact number length | All 350 are 9 digits |
| Name-and-city combinations | 309 unique combinations; 41 excess occurrences |
| City consistency | 7 city labels; no whitespace issues |
| Cross-dataset validation | C0012 unmatched in both customer datasets |

## 10. Cleaning Considerations and Decisions

The following observations should be carried forward to Phase 4 — Data Cleaning and Validation.

| Observation | Decision |
|---|---|
| Repeated full names | Do not remove records based on names alone. |
| Repeated full-name-and-city combinations | Retain pending further evidence; these are not confirmed duplicate customers. |
| Nine-digit contact numbers | Investigate the apparent missing leading zero and determine an appropriate standardisation rule. |
| Customer ID C0012 absent from both customer datasets | Investigate the unmatched reference before deciding how it should be handled. |
| City values | No standardisation issue identified in this dataset. |
| Missing values | None identified. |

**Important:** The original source file remains unchanged. Any cleaning, standardisation or correction will be performed on a separate working copy during the cleaning phase.

## 11. Investigation Conclusion

The investigation found that `customer_export_legacy.csv` is complete across its four columns, contains unique customer identifiers and unique contact numbers, and has consistent city labels.

Repeated names and name-and-city combinations were identified, but these were not sufficient evidence to classify records as duplicate customers.

The main outstanding data quality concern is the unmatched customer reference `C0012`, which appears in 87 Sales records but is absent from both customer datasets.

The findings and cleaning considerations will be carried forward into the next phase of the MetroMart project.
