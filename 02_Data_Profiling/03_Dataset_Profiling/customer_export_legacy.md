# Legacy Customers Dataset Profile

## 1. Dataset Overview

The `customer_export_legacy` dataset contains customer information from a legacy customer export. It includes customer reference numbers, names, contact numbers, and city information.

The dataset was profiled to understand its structure, completeness, uniqueness, and general characteristics before further data quality investigation.

| Attribute | Details |
|---|---|
| Dataset | `customer_export_legacy` |
| Total records | 350 |
| Total fields | 4 |
| Profiling tool | Google Sheets |

## 2. Field-Level Profile

The following table summarises the initial profiling results.

| Field | Data Type | Total Records | Missing Values | Unique Values |
|---|---|---:|---:|---:|
| `cust_no` | String | 350 | 0 | 350 |
| `full_name` | String | 350 | 0 | 182 |
| `contact_number` | String | 350 | 0 | 350 |
| `city` | String | 350 | 0 | 7 |

## 3. Initial Profiling Observations

### 3.1 Customer Reference Number (`cust_no`)

- All 350 records contain a customer reference number.
- No missing values were identified.
- All 350 reference numbers are unique.

**Observation:** Every record has a distinct legacy customer reference number. Based on the initial profiling results, `cust_no` is a potential primary key within this dataset.

### 3.2 Customer Name (`full_name`)

- All 350 records contain a customer name.
- No missing values were identified.
- The dataset contains 182 unique names.
- There are 168 repeated occurrences beyond the first occurrence.
- Some names appear up to six times.

**Observation:** Customer names are repeated throughout the dataset. These repetitions may represent different customers sharing the same name or possible overlapping records. Repeated names alone do not establish duplicate customer records.

### 3.3 Contact Number (`contact_number`)

- All 350 records contain a contact number.
- No missing values were identified.
- All 350 contact numbers are unique.
- All recorded contact numbers contain nine digits.

**Observation:** The contact number field is complete and contains unique values throughout the dataset. The nine-digit representation is consistent with the expected format for South African mobile and contact numbers, although the validity of individual numbers has not been established through profiling.

### 3.4 City (`city`)

- All 350 records contain a city value.
- No missing values were identified.
- Seven unique city values were identified.

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

**Observation:** The dataset contains seven distinct city values, with records distributed across the listed locations. Unlike the main `customers` dataset, the legacy export uses `Johannesburg` rather than the abbreviation `JHB`.

## 4. Profiling Summary

The initial profiling established the following characteristics:

- The dataset contains 350 records across four fields.
- All customer reference numbers are populated and unique.
- Customer names have 182 unique values, with repeated names occurring throughout the dataset.
- All 350 contact numbers are populated and unique, with each containing nine digits.
- All customer records contain a city value.
- Seven distinct cities are represented in the dataset.

## 5. Profiling Conclusion

The `customer_export_legacy` dataset is complete across all four fields, with no missing values identified during initial profiling.

The customer reference numbers and contact numbers are unique within the dataset. Repeated customer names were observed and recorded as a characteristic requiring careful interpretation rather than automatic classification as duplicate records.

The city field contains seven distinct locations, with no missing values identified.

These findings provide an initial understanding of the legacy customer dataset. Any further investigation into record overlap, identifier relationships, or other data quality concerns is handled separately during the project's data quality investigation stage.

No changes were made to the original source data during profiling.
