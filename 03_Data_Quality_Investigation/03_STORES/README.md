# Data Quality Investigation
## Dataset: stores.csv

### 1. Dataset overview
- Records: 5
- Fields: 4
- Business purpose: Store Master File
- Fields: `store_code`, `store_name`, `city`, `province`

### 2. Profiling results

| Field | Records | Missing | Unique values |
|---|---:|---:|---:|
| store_code | 5 | 0 | 5 |
| store_name | 5 | 0 | 5 |
| city | 5 | 0 | 2 |
| province | 5 | 0 | 1 |

### 3. Data quality observations

**DQ observation — City naming inconsistency**

- `Johannesburg`: 4 occurrences.
- `JHB`: 1 occurrence.
- The legacy customer export uses full geographical names and contains no `JHB` abbreviation.
- The geographical meaning of `JHB` has not been independently verified.
- Standardization is deferred until Phase 4.

**Store identifier validation**

- Five distinct store codes were identified.
- All five codes appeared in the employee store references examined.
- All five codes appeared in the sales dataset.
- No invalid store references were identified in the reported checks.

### 4. Investigation conclusion

The dataset contains no identified missing values or duplicate store identifiers/names.

One potential naming inconsistency remains unresolved: `JHB` versus `Johannesburg`.

No changes were made to the original source data.

### 5. Outstanding action

Revisit the geographical naming inconsistency during Phase 4 cleaning and document the standardization decision, supporting evidence and source-to-cleaned-data traceability.

### 6. Investigation status

Investigation completed provisionally. City naming clarification remains pending.
