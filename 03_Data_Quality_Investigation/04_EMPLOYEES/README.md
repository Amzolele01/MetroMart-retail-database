# Employee Data Quality Investigation

**Project:** MetroMart Database Project  
**Phase:** Phase 3 — Data Quality Investigation  
**Dataset:** `employees.csv`  
**Record Count:** 60  
**Investigation Status:** Completed  
**Data Modification:** None

---

## 1. Dataset Overview

The `employees.csv` dataset contains employee master records used to identify employees, their assigned stores, and their respective job roles.

| Column | Description |
|---|---|
| `employee_id` | Unique employee identifier |
| `employee_name` | Employee's full name |
| `store_id` | Store to which the employee is assigned |
| `role` | Employee's job role |

The investigation focused on the completeness, consistency, uniqueness and referential integrity of the employee records.

## 2. Previously Established Results

The following results were established during Phase 2 — Data Profiling and carried forward into this investigation.

### 2.1 Employee ID Uniqueness

| Check | Result |
|---|---:|
| Total employee records | 60 |
| Distinct employee IDs | 60 |
| Blank employee IDs | 0 |
| Duplicate employee IDs | 0 |

**Finding:** All 60 employee records have distinct employee identifiers. No missing or duplicate employee IDs were recorded during profiling.

### 2.2 Sales-to-Employee Referential Validation

The discovery workbook established that all employee IDs referenced in `sales_2023_2025.csv` exist in `employees.csv`.

**Finding:** No invalid employee references were recorded in the sales dataset.

These checks were not unnecessarily repeated during Phase 3.

---

## 3. Employee Name Investigation

**Column:** `employee_name`

The investigation examined missing names, distinct name values, repeated names and formatting consistency.

### 3.1 Missing Employee Names

Formula:

`=COUNTBLANK(B2:B61)`

Result: **0**

Finding: No employee records have blank employee names.

### 3.2 Distinct Employee Names

Formula:

`=COUNTUNIQUE(B2:B61)`

Result: **50**

Finding: The dataset contains 50 distinct employee names across 60 employee records.

### 3.3 Repeated Employee Names

Formula:

`=QUERY(B2:B61,"SELECT B, COUNT(B) WHERE B IS NOT NULL GROUP BY B LABEL B 'Employee Name', COUNT(B) 'Occurrences'",0)`

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

Formula:

`=FILTER(A2:B61,COUNTIF(B2:B61,B2:B61)>1)`

The resulting employee records showed that all repeated names were associated with different employee IDs.

**Finding:** Repeated employee names represent separate employee records. No duplicate employee records were confirmed based on this investigation.

### 3.5 Name Formatting Checks

Leading and trailing spaces:

`=SUM(ARRAYFORMULA(N(B2:B61<>TRIM(B2:B61))))`

Result: **0**

Capitalization consistency:

`=SUM(ARRAYFORMULA(N(B2:B61<>PROPER(B2:B61))))`

Result: **0**

**Finding:** No leading or trailing spaces or capitalization inconsistencies were detected.

### Employee Name Conclusion

The `employee_name` column passed the investigated completeness and formatting checks. Repeated names were identified but were not classified as duplicate records because their associated employee IDs were distinct.

---

## 4. Employee Store Assignment Investigation

**Column:** `store_id`

The investigation examined missing store assignments, employee distribution across stores and referential integrity against `stores.csv`.

### 4.1 Missing Store Assignments

Formula:

`=COUNTBLANK(C2:C61)`

Result: **0**

Finding: All employee records contain a store assignment.

### 4.2 Employee Distribution Across Stores

Formula:

`=QUERY(C2:C61,"SELECT C, COUNT(C) WHERE C IS NOT NULL GROUP BY C LABEL C 'Store ID', COUNT(C) 'Employee Count'",0)`

Results:

| Store ID | Employee Count |
|---|---:|
| S001 | 5 |
| S002 | 9 |
| S003 | 12 |
| S004 | 20 |
| S005 | 14 |
| **Total** | **60** |

Finding: All 60 employees are assigned to one of five distinct stores.

### 4.3 Referential Integrity Validation

The employee dataset's `store_id` values were compared against the `store_code` column in `stores.csv`.

Formula:

`=SUM(ARRAYFORMULA(COUNTIF(Stores!A2:A6,C2:C61)=0))`

Result: **0**

Finding: All employee store references exist in the store master dataset.

No invalid store references were identified.

### Store Assignment Conclusion

The `store_id` column passed the investigated completeness and referential integrity checks. All employee records reference existing stores.

---

## 5. Employee Role Investigation

**Column:** `role`

The investigation examined missing role values, distinct roles, employee distribution and formatting consistency.

### 5.1 Missing Role Values

Formula:

`=COUNTBLANK(D2:D61)`

Result: **0**

Finding: No employee records have missing role values.

### 5.2 Distinct Employee Roles

Formula:

`=QUERY(D2:D61,"SELECT D, COUNT(D) WHERE D IS NOT NULL GROUP BY D LABEL D 'Employee Role', COUNT(D) 'Employee Count'",0)`

Results:

| Employee Role | Employee Count |
|---|---:|
| Cashier | 18 |
| Sales Assistant | 17 |
| Store Manager | 12 |
| Store Supervisor | 13 |
| **Total** | **60** |

Finding: Four distinct employee roles were identified across the dataset.

### 5.3 Role Formatting Checks

Leading and trailing spaces:

`=SUM(ARRAYFORMULA(N(D2:D61<>TRIM(D2:D61))))`

Result: **0**

Capitalization consistency:

`=SUM(ARRAYFORMULA(N(D2:D61<>PROPER(D2:D61))))`

Result: **0**

Finding: No leading or trailing spaces or capitalization inconsistencies were detected.

### Role Conclusion

The `role` column passed the investigated completeness and formatting checks. All 60 employee records contain a role, and four distinct role values were identified.

---

## 6. Consolidated Investigation Results

| Field | Investigation | Result |
|---|---|---|
| `employee_id` | Uniqueness | 60 distinct IDs |
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

## 7. Data Quality Findings and Corrective Actions

The investigation did not identify any confirmed data quality defects within the examined dimensions.

The repeated employee names were treated as informational observations rather than duplicate records because the associated employee IDs were distinct.

| Observation | Classification | Corrective Action |
|---|---|---|
| Nine employee names appear more than once | Informational | None required |
| All employee IDs are distinct | Passed validation | None required |
| All employee store references are valid | Passed validation | None required |
| Four distinct employee roles identified | Informational | None required |

No changes were made to the original dataset.

No corrective transformations were required based on the investigation results.

## 8. Final Conclusion

The Phase 3 investigation of `employees.csv` established that the dataset passed the examined checks for employee identifier uniqueness, employee name completeness and formatting, store assignment completeness, store referential integrity, and employee role completeness and formatting.

The investigation also identified repeated employee names, which were verified against employee identifiers and determined not to represent confirmed duplicate records.

No confirmed data quality defects requiring corrective action were identified.

**Final Status: Investigation Completed — No Confirmed Defects Identified.**
