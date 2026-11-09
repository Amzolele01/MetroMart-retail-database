# Employees Dataset Profile

## 1. Dataset Overview

The `employees` dataset contains information about MetroMart employees, including employee identifiers, names, assigned stores, and job roles.

The dataset was profiled to understand its structure, completeness, uniqueness, and distribution of employee information.

| Attribute | Details |
|---|---|
| Dataset | `employees` |
| Total records | 60 |
| Total fields | 4 |
| Profiling tool | Google Sheets |

## 2. Field-Level Profile

The following table summarises the initial profiling results.

| Field | Data Type | Total Records | Missing Values | Unique Values |
|---|---|---:|---:|---:|
| `employee_id` | String | 60 | 0 | 60 |
| `employee_name` | String | 60 | 0 | 50 |
| `store_id` | String | 60 | 0 | 5 |
| `role` | String | 60 | 0 | 4 |

## 3. Initial Profiling Observations

### 3.1 Employee Identifier (`employee_id`)

- All 60 records contain an employee identifier.
- No missing values were identified.
- All 60 identifiers are unique.

**Observation:** Every employee record has a distinct identifier. Based on the initial profiling results, `employee_id` is a potential primary key.

### 3.2 Employee Name (`employee_name`)

- All 60 records contain an employee name.
- No missing values were identified.
- The dataset contains 50 unique names.
- 41 names occur once.
- Eight names occur twice.
- One name, `Amanda Naidoo`, occurs three times.

**Observation:** Employee names are repeated across some records. These repetitions do not necessarily indicate duplicate employee records, as different employees may share the same name.

### 3.3 Store Assignment (`store_id`)

- All 60 records contain a store reference.
- No missing values were identified.
- Five unique store identifiers were recorded.

| Store ID | Employee Records |
|---|---:|
| S001 | 5 |
| S002 | 9 |
| S003 | 12 |
| S004 | 20 |
| S005 | 14 |
| **Total** | **60** |

**Observation:** All five store identifiers are represented in the employee dataset. Employee distribution varies across the stores, with S004 having the highest number of assigned employees.

### 3.4 Employee Role (`role`)

- All 60 records contain a job role.
- No missing values were identified.
- Four unique roles were identified.

| Role | Employee Records |
|---|---:|
| Cashier | 18 |
| Sales Assistant | 17 |
| Store Manager | 12 |
| Store Supervisor | 13 |
| **Total** | **60** |

**Observation:** The dataset contains four distinct employee roles. Cashiers represent the largest group, followed by Sales Assistants, Store Supervisors, and Store Managers.

## 4. Profiling Summary

The initial profiling established the following characteristics:

- The dataset contains 60 records across four fields.
- All employee identifiers are populated and unique.
- Employee names contain 50 unique values, with some names appearing more than once.
- All employee records contain a store assignment.
- Five distinct store identifiers are represented.
- Four distinct employee roles are recorded.
- No missing values were identified in any of the four fields.

## 5. Profiling Conclusion

The `employees` dataset is complete across all four fields, with no missing values identified during initial profiling.

The employee identifiers are unique and provide a potential primary key for the dataset. Repeated employee names were observed but do not independently establish duplicate records.

The dataset also provides an overview of employee distribution across the five stores and four recorded job roles.

These findings establish the initial structure and characteristics of the employee dataset. Further validation of store references and other potential data quality concerns is handled separately during the project's data quality investigation stage.

No changes were made to the original source data during profiling.
