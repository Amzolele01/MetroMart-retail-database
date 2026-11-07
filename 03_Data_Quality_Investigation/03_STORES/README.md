# Stores Dataset — Data Quality Investigation

## 1. Dataset Overview

**Source file:** `stores.csv`  
**Investigation phase:** Phase 3 — Data Quality Investigation  
**Project:** MetroMart Retail Database

The Stores dataset contains the store information used to identify and distinguish MetroMart's retail locations.

### Dataset structure

- **Total records:** 5
- **Total columns:** 4
- **Missing values:** 0

The dataset contains no missing values in the four investigated columns.

## 2. Store Identifier Investigation

The `store_id` column was examined to establish whether store identifiers were complete and unique.

### Findings

- All five records contain a store identifier.
- No duplicate store IDs were identified.
- Each store has a distinct identifier.
- All five identifiers were found in the employee and sales references examined.

**Conclusion:** The store identifiers are complete and unique, providing a suitable basis for identifying stores in the database.

## 3. Store Name Investigation

The store names were checked for missing values and duplicate entries.

### Findings

- No missing store names were identified.
- All five store names are unique.
- No duplicate store names were identified.

**Conclusion:** No data-quality issues were identified with store names.

## 4. Location Investigation

The location-related fields were examined to identify missing information and inconsistencies.

### Findings

- No missing city values were identified.
- No missing province values were identified.
- All five stores are located in Gauteng.
- Four records use `Johannesburg`, while one record uses `JHB`.

### Identified inconsistency

The values `Johannesburg` and `JHB` appear to represent the same city, but the dataset uses two different labels.

No correction was made because no approved location reference or standardisation rule was provided.

**Decision:** Preserve the original values during the investigation and record the inconsistency for consideration during Phase 4 — Data Cleaning and Validation.

## 5. Employee-to-Store Referential Integrity

The Employees dataset was examined to establish whether employee records reference valid stores.

The five store identifiers from `stores.csv` were imported into the Employees working spreadsheet using `IMPORTRANGE`.

### Validation formula

The following formula was used to compare each employee's `store_id` against the imported store identifiers:

```excel
=COUNTIF($H$1:$H$5,C2)
```

The formula was filled down for all 60 employee records.

### Findings

| Validation result | Number of records |
|---|---:|
| Valid references (1) | 60 |
| Unmatched references (0) | 0 |
| Multiple matches (>1) | 0 |
| **Total** | **60** |

During the initial validation, employee `E060` temporarily returned zero. Further investigation confirmed that its `store_id` was `S004`, which exactly matched the imported store identifier. The issue was traced to the validation setup, and the corrected formula returned 1.

**Conclusion:** All 60 employee records reference exactly one valid store identifier. No invalid employee-to-store references were identified.

## 6. Sales-to-Store Referential Integrity

The Sales dataset (`sales_2023_2025.csv`) was examined to establish whether sales records reference valid stores.

### 6.1 Store ID frequency analysis

The `store_id` column, located in column D, was examined to identify distinct store identifiers and their frequencies.

The following Google Sheets formula was used:

```excel
=QUERY(D2:D,"SELECT D, COUNT(D) WHERE D IS NOT NULL GROUP BY D LABEL D 'store_id', COUNT(D) 'record_count'",0)
```

### Findings

| Store ID | Sales records |
|---|---:|
| S001 | 20,028 |
| S002 | 19,887 |
| S003 | 19,938 |
| S004 | 20,199 |
| S005 | 19,948 |
| **Total** | **100,000** |

The frequency analysis identified five distinct store identifiers, all corresponding to identifiers present in `stores.csv`.

No blank `store_id` values appeared in the frequency results.

### 6.2 Referential integrity validation

The store identifiers from `stores.csv` were imported into the Sales working spreadsheet using `IMPORTRANGE`.

An `ARRAYFORMULA` was used to validate all sales records without manually dragging the formula down.

```excel
=ARRAYFORMULA(IF(D2:D100001="","",COUNTIF(IMPORTRANGE("STORES_SPREADSHEET_URL","A2:A6"),D2:D100001)))
```

`STORES_SPREADSHEET_URL` represents the URL of the Stores spreadsheet.

The validation results were placed in column O.

The following formula was used to calculate the sum of the validation results:

```excel
=SUM(O1:O100001)
```

### Findings

- All 100,000 sales records returned a validation result of 1.
- The sum of the validation results was 100,000.
- No unmatched store references were identified.
- No store identifier matched multiple entries in the Stores reference list.

**Conclusion:** All 100,000 sales records reference exactly one valid store identifier.

## 7. Summary of Findings

The Stores investigation identified no missing values, duplicate store identifiers, or duplicate store names.

The following referential integrity checks were completed:

| Relationship | Records checked | Valid references |
|---|---:|---:|
| Employees → Stores | 60 | 60 |
| Sales → Stores | 100,000 | 100,000 |

### Identified observation

The city field contains inconsistent labels:

- `Johannesburg`
- `JHB`

This inconsistency was recorded for consideration during the cleaning phase. No unsupported corrections were made.

## 8. Data Cleaning Decisions

The following decisions were made during the investigation:

1. No store records were removed.
2. No store identifiers were modified.
3. No store names were modified.
4. No city or province values were changed.
5. The `Johannesburg` / `JHB` inconsistency was retained for future standardisation.
6. Employee and sales store references were validated successfully.
7. The original source dataset was preserved unchanged.

## 9. Final Conclusion

The Stores dataset passed the investigated structural, completeness, uniqueness, and referential integrity checks.

All five store identifiers are unique, and all 60 employee records and 100,000 sales records reference valid store identifiers.

The only identified observation requiring further consideration is the inconsistent city labelling.

The Stores investigation is therefore complete for Phase 3. Any approved city-label standardisation will be addressed during Phase 4 — Data Cleaning and Validation, with the original source values preserved for traceability.
