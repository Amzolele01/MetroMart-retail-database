# Employee Dataset — Data Quality Investigation

**Project:** MetroMart Retail Database  
**Phase:** Phase 3 — Data Quality Investigation  
**Dataset:** `employees.csv`  
**Record Count:** 60  
**Investigation Status:** Completed  
**Data Modification:** None

## 1. Dataset Overview

The `employees.csv` dataset contains employee master records used to identify employees, their assigned stores, and their respective job roles.

| Column | Description |
|---|---|
| `employee_id` | Unique employee identifier |
| `employee_name` | Employee's full name |
| `store_id` | Store to which the employee is assigned |
| `role` | Employee's job role |

The investigation focused on the completeness, consistency, uniqueness, formatting, and referential integrity of employee records.

The investigation was conducted using a working copy of the source data. The original dataset was preserved unchanged.

## 2. Employee ID Investigation

The `employee_id` column was examined for completeness, uniqueness, formatting consistency, and sequence completeness.

### 2.1 Uniqueness and Completeness

These results were initially established during Phase 2 — Data Profiling and carried forward into Phase 3.

| Check | Result |
|---|---:|
| Total employee records | 60 |
| Distinct employee IDs | 60 |
| Blank employee IDs | 0 |
| Duplicate employee IDs | 0 |

**Finding:** All 60 employee records have distinct employee identifiers. No missing or duplicate employee IDs were identified.

### 2.2 Formatting and Sequence Validation

**Formulas used:**

Leading and trailing spaces:

```excel
=SUM(ARRAYFORMULA(N(A2:A61<>TRIM(A2:A61))))
```

ID format consistency:

```excel
=SUM(ARRAYFORMULA(N(NOT(REGEXMATCH(A2:A61,"^E[0-9]{3}$")))))
```

Missing IDs in the expected sequence:

```excel
=SUM(ARRAYFORMULA(N(COUNTIF(A2:A61,"E"&TEXT(SEQUENCE(60),"000"))=0)))
```

**Results:**

| Check | Result |
|---|---:|
| IDs with leading or trailing spaces | 0 |
| IDs with invalid formats | 0 |
| Missing IDs in expected sequence | 0 |

**Finding:** All 60 employee identifiers follow the expected E001–E060 format. No formatting issues or missing identifiers within the expected sequence were identified.

## 3. Employee Name Investigation

**Column:** `employee_name`

The investigation examined missing names, distinct name values, repeated names, and formatting consistency.

### 3.1 Missing Employee Names

**Formula:**

```excel
=COUNTBLANK(B2:B61)
```

**Result:** 0

**Finding:** No employee records have blank employee names.

### 3.2 Distinct Employee Names

**Formula:**

```excel
=COUNTUNIQUE(B2:B61)
```

**Result:** 50

**Finding:** The dataset contains 50 distinct employee names across 60 employee records.

### 3.3 Repeated Employee Names

**Formula:**

```excel
=QUERY(B2:B61,"SELECT B, COUNT(B) WHERE B IS NOT NULL GROUP BY B LABEL B 'Employee Name', COUNT(B) 'Occurrences'",0)
```

The investigation identified nine names appearing more than once.

| Employee Name | Occurrences |
|---|---:|
| Amanda Naidoo | 3 |
| David Mthembu | 2 |
| Kagiso Smith | 2 |
| Kagiso Williams | 2 |
| Karabo Williams | 2 |
| Mpho Williams | 2 |
| Nomsa Molefe | 2 |
| Sibusiso Naidoo | 2 |
| Thabo Mabena | 2 |

### 3.4 Verification of Repeated Names

**Formula:**

```excel
=FILTER(A2:B61,COUNTIF(B2:B61,B2:B61)>1)
```

The resulting employee records showed that all repeated names were associated with different employee IDs.

**Finding:** Repeated employee names represent separate employee records. No duplicate employee records were confirmed based on these repeated names.

### 3.5 Name Formatting Checks

Leading and trailing spaces:

```excel
=SUM(ARRAYFORMULA(N(B2:B61<>TRIM(B2:B61))))
```

Capitalization consistency:

```excel
=SUM(ARRAYFORMULA(N(B2:B61<>PROPER(B2:B61))))
```

**Results:**

| Check | Result |
|---|---:|
| Names with leading or trailing spaces | 0 |
| Names with capitalization inconsistencies | 0 |

**Employee Name Conclusion:** The `employee_name` column passed the investigated completeness and formatting checks. Repeated names were identified but were not classified as duplicate records because their associated employee IDs were distinct.

## 4. Employee Store Assignment Investigation

**Column:** `store_id`

The investigation examined missing store assignments, employee distribution across stores, and referential integrity against `stores.csv`.

### 4.1 Missing Store Assignments

**Formula:**

```excel
=COUNTBLANK(C2:C61)
```

**Result:** 0

**Finding:** All employee records contain a store assignment.

### 4.2 Employee Distribution Across Stores

**Formula:**

```excel
=QUERY(C2:C61,"SELECT C, COUNT(C) WHERE C IS NOT NULL GROUP BY C LABEL C 'Store ID', COUNT(C) 'Employee Count'",0)
```

**Results:**

| Store ID | Employee Count |
|---|---:|
| S001 | 5 |
| S002 | 9 |
| S003 | 12 |
| S004 | 20 |
| S005 | 14 |
| **Total** | **60** |

**Finding:** All 60 employees are assigned to one of five distinct stores.

### 4.3 Employee-to-Store Referential Integrity

The employee dataset's `store_id` values were compared against the store identifiers in `stores.csv`.

**Formula:**

```excel
=SUM(ARRAYFORMULA(COUNTIF(Stores!A2:A6,C2:C61)=0))
```

**Result:** 0

**Finding:** All employee store references exist in the Stores master dataset. No invalid store references were identified.

### Store Assignment Conclusion

The `store_id` column passed the investigated completeness and referential integrity checks. All employee records reference existing stores.

## 5. Employee Role Investigation

**Column:** `role`

The investigation examined missing role values, distinct roles, employee distribution, and formatting consistency.

### 5.1 Missing Role Values

**Formula:**

```excel
=COUNTBLANK(D2:D61)
```

**Result:** 0

**Finding:** No employee records have missing role values.

### 5.2 Distinct Employee Roles

**Formula:**

```excel
=QUERY(D2:D61,"SELECT D, COUNT(D) WHERE D IS NOT NULL GROUP BY D LABEL D 'Employee Role', COUNT(D) 'Employee Count'",0)
```

**Results:**

| Employee Role | Employee Count |
|---|---:|
| Cashier | 18 |
| Sales Assistant | 17 |
| Store Manager | 12 |
| Store Supervisor | 13 |
| **Total** | **60** |

**Finding:** Four distinct employee roles were identified across the dataset. The role names and counts were confirmed against the source data.

### 5.3 Role Formatting Checks

Leading and trailing spaces:

```excel
=SUM(ARRAYFORMULA(N(D2:D61<>TRIM(D2:D61))))
```

Capitalization consistency:

```excel
=SUM(ARRAYFORMULA(N(D2:D61<>PROPER(D2:D61))))
```

**Results:**

| Check | Result |
|---|---:|
| Roles with leading or trailing spaces | 0 |
| Roles with capitalization inconsistencies | 0 |

**Role Conclusion:** The `role` column passed the investigated completeness and formatting checks. All 60 employee records contain a role, and four distinct role values were identified.

## 6. Complete Duplicate Record Validation

The complete employee records were checked across all four columns to establish whether any two records were identical.

**Formula:**

```excel
=COUNTUNIQUE(ARRAYFORMULA(A2:A61&"♦"&B2:B61&"♦"&C2:C61&"♦"&D2:D61))
```

**Result:** 60

**Finding:** All 60 employee records are distinct across the four investigated columns. No complete duplicate employee records were identified.

## 7. Sales-to-Employee Referential Validation

The discovery workbook established that all employee IDs referenced in `sales_2023_2025.csv` exist in `employees.csv`.

This validation was established during Phase 2 — Data Profiling and carried forward into Phase 3 without unnecessary repetition.

**Finding:** No invalid employee references were recorded in the Sales dataset.

## 8. Consolidated Investigation Results

| Field | Investigation | Result |
|---|---|---|
| `employee_id` | Uniqueness | 60 distinct IDs |
| `employee_id` | Formatting | 0 invalid formats |
| `employee_id` | Sequence completeness | E001–E060 complete |
| `employee_name` | Missing values | 0 |
| `employee_name` | Distinct names | 50 |
| `employee_name` | Repeated names | 9 |
| `employee_name` | Formatting inconsistencies | 0 detected |
| `store_id` | Missing assignments | 0 |
| `store_id` | Distinct store references | 5 |
| `store_id` | Invalid store references | 0 |
| `role` | Missing values | 0 |
| `role` | Distinct roles | 4 |
| `role` | Formatting inconsistencies | 0 detected |
| Complete records | Duplicate records | 0 |

### 8.1 Referential Integrity Summary

| Relationship | Records checked | Valid references |
|---|---:|---:|
| Employees → Stores | 60 | 60 |
| Sales → Employees | Established during Phase 2 | No invalid references identified |

## 9. Data Quality Findings and Decisions

The investigation did not identify any confirmed data quality defects within the examined dimensions.

The repeated employee names were treated as informational observations rather than duplicate records because their associated employee IDs were distinct.

| Observation | Classification | Decision |
|---|---|---|
| Nine employee names appear more than once | Informational | Retain all records |
| All employee IDs are distinct | Passed validation | No correction required |
| Employee IDs follow E001–E060 | Passed validation | No correction required |
| All employee store references are valid | Passed validation | No correction required |
| Four distinct employee roles identified | Informational | Retain recorded role values |
| No complete duplicate records | Passed validation | No record removal required |

No corrective transformations were required based on the investigation results.

No changes were made to the original `employees.csv`.

## 10. Business Requirements Relevance

The investigation supports the following project requirements:

- **BR-07:** Preserve traceability between source records and the final database.
- **BR-08:** Prevent invalid relational records in the final database.
- **BR-10:** Document important cleaning and modelling decisions.

Employee identifiers and store assignments are particularly important for maintaining valid relationships between employee, store, and sales records.

## 11. Phase 4 Considerations

The following findings should be carried forward:

- Preserve employee identifiers and their established format.
- Retain repeated employee names unless additional evidence establishes duplicate identities.
- Maintain valid employee-to-store relationships.
- Use the four observed employee role values consistently in the final database.
- Preserve the original source data for traceability.

No specific corrective cleaning actions were identified as necessary from the Phase 3 investigation.

## 12. Final Conclusion

The Phase 3 investigation of `employees.csv` established that the dataset passed the examined checks for employee identifier uniqueness, formatting and sequence completeness, employee name completeness and formatting, store assignment completeness, store referential integrity, and employee role completeness and formatting.

Repeated employee names were identified and verified against employee identifiers. These records represent separate employee records rather than confirmed duplicates.

Additional validation confirmed that all 60 employee records are distinct across the four columns and that all employee identifiers follow the expected E001–E060 sequence.

The Sales-to-Employee relationship was also established as valid during Phase 2, with no invalid employee references recorded.

No confirmed data quality defects requiring corrective action were identified. No changes were made to the original dataset.

**Final Status: Investigation Completed — No Confirmed Defects Identified.**
