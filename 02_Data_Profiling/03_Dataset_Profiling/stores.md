# Stores Dataset Profile

## 1. Dataset Overview

The `stores` dataset contains information about MetroMart's physical store locations, including store identifiers, names, cities, and provinces.

The dataset was profiled to understand its structure, completeness, uniqueness, and geographical distribution.

| Attribute | Details |
|---|---|
| Dataset | `stores` |
| Total records | 5 |
| Total fields | 4 |
| Profiling tool | Google Sheets |

## 2. Field-Level Profile

The following table summarises the initial profiling results.

| Field | Data Type | Total Records | Missing Values | Unique Values |
|---|---|---:|---:|---:|
| `store_code` | String | 5 | 0 | 5 |
| `store_name` | String | 5 | 0 | 5 |
| `city` | String | 5 | 0 | 2 |
| `province` | String | 5 | 0 | 1 |

## 3. Initial Profiling Observations

### 3.1 Store Identifier (`store_code`)

- All five records contain a store code.
- No missing values were identified.
- All five store codes are unique.

**Observation:** Each store has a distinct identifier. Based on the initial profiling results, `store_code` is a potential primary key.

### 3.2 Store Name (`store_name`)

- All five records contain a store name.
- No missing values were identified.
- All five store names are unique.

The recorded store names are:

- Sandton
- Randburg
- Roodepoort
- Rosebank
- Fourways

**Observation:** Each store has a distinct recorded name, with no repeated store names identified during initial profiling.

### 3.3 City (`city`)

- All five records contain a city value.
- No missing values were identified.
- Two unique city values were identified.

| City | Store Records |
|---|---:|
| Johannesburg | 4 |
| JHB | 1 |
| **Total** | **5** |

**Observation:** The city field contains two different representations: `Johannesburg` and `JHB`. The abbreviation may refer to the same geographical location, but this has not been formally established.

This is recorded as a potential naming inconsistency for consideration during data quality investigation.

### 3.4 Province (`province`)

- All five records contain a province value.
- No missing values were identified.
- One unique province value was identified: `Gauteng`.

**Observation:** All five stores are associated with Gauteng. No variation in province values was identified during the initial profiling summary.

## 4. Profiling Summary

The initial profiling established the following characteristics:

- The dataset contains five records across four fields.
- All store codes are populated and unique.
- All store names are populated and unique.
- The city field contains two distinct representations: `Johannesburg` and `JHB`.
- All stores are associated with Gauteng.
- No missing values were identified in any of the four fields.

## 5. Profiling Conclusion

The `stores` dataset provides a compact reference of MetroMart's five store locations.

All records contain the required field values, and both store identifiers and store names are unique.

The main observation from the initial profiling concerns the two city representations, `Johannesburg` and `JHB`. This is retained as a preliminary observation rather than treated as a confirmed issue.

The dataset provides an initial reference for examining store assignments in the employee and sales datasets during subsequent project stages.

No changes were made to the original source data during profiling.
