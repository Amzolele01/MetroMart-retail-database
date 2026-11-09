# Customers Dataset Profile

## 1. Dataset Overview

The `customers` dataset contains registered customer information, including customer identifiers, names, contact details, and geographical information.

The dataset was profiled to understand its structure, field characteristics, completeness, and the distribution of values before proceeding with detailed data quality investigation.

| Attribute | Details |
|---|---|
| Dataset | `customers` |
| Total records | 1,220 |
| Total fields | 6 |
| Profiling tool | Google Sheets |

## 2. Field-Level Profile

The following table summarises the initial profiling results for each field.

| Field | Data Type | Total Records | Missing Values | Unique Values |
|---|---|---:|---:|---:|
| `customer_id` | String | 1,220 | 0 | 1,220 |
| `customer_name` | String | 1,220 | 0 | 226 |
| `phone` | String | 1,220 | 25 | 1,194 |
| `email` | String | 1,220 | 0 | 1,200 |
| `city` | String | 1,220 | 0 | 7 |
| `province` | String | 1,220 | 0 | 1 |

## 3. Initial Profiling Observations

### 3.1 Customer Identifier (`customer_id`)

- All 1,220 records contain a customer identifier.
- No missing values were identified.
- All 1,220 identifiers are unique.

**Observation:** Each customer record has a distinct identifier. Based on the initial profiling results, `customer_id` is a potential primary key.

### 3.2 Customer Name (`customer_name`)

- All 1,220 records contain a customer name.
- No missing values were identified.
- The dataset contains 226 unique names.

**Observation:** Customer names occur repeatedly across the dataset. Repeated names alone do not establish that customer records are duplicates, as different customers may share the same name.

### 3.3 Phone Number (`phone`)

- The field contains 1,220 records.
- 25 values are missing.
- There are 1,194 unique nonblank values.
- The initial profile recorded 1,175 numeric values and 20 text values.
- Differences in value lengths and formatting were observed.
- The phone number `882884346` appears against customer identifiers `C0429` and `C0640`.

**Observation:** The phone field contains missing values and differences in how phone numbers are represented. A repeated phone number was also observed across two customer records.

These observations may require further investigation, particularly when assessing contact information consistency and possible customer-record overlap.

### 3.4 Email (`email`)

- All 1,220 records contain an email address.
- No missing values were identified.
- The dataset contains 1,200 unique email values.
- Twenty email addresses occur twice, affecting 40 records.

**Observation:** Repeated email addresses were identified across customer records. These may indicate potential customer-record overlap, but repeated email addresses alone do not confirm duplicate customer records.

### 3.5 City (`city`)

- All 1,220 records contain a city value.
- No missing values were identified.
- Seven unique city values were identified.
- The abbreviation `JHB` occurs in 155 records.

**Observation:** The dataset contains seven distinct city values. The use of `JHB` may represent a naming variation for Johannesburg, although its intended meaning has not been formally confirmed.

### 3.6 Province (`province`)

- All 1,220 records contain a province value.
- No missing values were identified.
- Only one unique value was identified: `Gauteng`.

**Observation:** All customer records are associated with Gauteng. No variation in province values was identified during initial profiling.

## 4. Profiling Summary

The initial profiling of the `customers` dataset established the following:

- The dataset contains 1,220 records across six fields.
- All customer identifiers are populated and unique, making `customer_id` a potential primary key.
- Customer names occur repeatedly, although this does not necessarily indicate duplicate records.
- Phone numbers contain missing values, formatting differences, and a repeated value across two customer identifiers.
- Email addresses are complete, but 20 addresses occur twice across 40 records.
- City values include the abbreviation `JHB`, which may represent a naming variation.
- All customer records contain `Gauteng` as their province.

## 5. Profiling Conclusion

The initial profiling provided an overview of the structure and characteristics of the customer dataset.

Several observations were identified involving contact information, repeated values, and geographical naming. These observations provide areas for consideration during the subsequent data quality investigation.

No cleaning decisions or changes to the original source data were made as part of this profiling exercise.

The detailed investigation of identified data quality concerns is documented separately in the project's data quality investigation stage.
