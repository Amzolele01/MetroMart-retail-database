# Phase 3 — Data Quality Investigation: Customers Dataset

## 1. Dataset Overview

**Source file:** `customers.csv`

The Customers dataset was investigated to identify missing values, inconsistencies, duplicate records and other potential data-quality issues.

The investigation was performed on the original source data. No records or values were modified during this phase.

| Attribute | Finding |
|---|---:|
| Total records | 1,220 |
| Total columns | 6 |
| Unique customer IDs | 1,220 |
| Unique full customer names | 225 |
| Missing values | 25 |
| Columns with missing values | Phone |

**Columns investigated:**
- `customer_id`
- `customer_name`
- `phone`
- `email`
- `city`
- `province`

## 2. Missing Values Investigation

A missing-value assessment was performed across all six columns.

| Column | Missing values |
|---|---:|
| customer_id | 0 |
| customer_name | 0 |
| phone | 25 |
| email | 0 |
| city | 0 |
| province | 0 |
| **Total** | **25** |

All 25 missing values occur in the `phone` column.

The affected records retain their customer IDs, names, email addresses, cities and provinces.

### 2.1 Missing Phone Numbers by City

| City | Missing phone values |
|---|---:|
| Fourways | 2 |
| JHB | 4 |
| Midrand | 3 |
| RANDburg | 5 |
| Roodepoort | 4 |
| Sandton | 3 |
| Soweto | 4 |
| **Total** | **25** |

### 2.2 Investigation into Recovering Missing Phone Numbers

The 25 affected records were investigated to determine whether existing customer records could provide reliable evidence for recovering the missing phone numbers.

The investigation included:

- Checking for exact duplicate email addresses.
- Identifying repeated full customer names.
- Retrieving other records with matching names and populated phone numbers.
- Comparing available customer details, including email addresses and cities.

**Findings:**

- None of the 25 records shared an exact email address with another customer record.
- All 25 customer names appeared elsewhere in the dataset.
- However, matching names generally had different email addresses and, in several cases, different cities.
- No confirmed identity matches provided sufficient evidence to recover the missing phone numbers.

**Decision:** All 25 missing phone values are classified as unresolved missing values. No phone numbers will be filled without reliable supporting evidence.

## 3. Customer ID Investigation

The `customer_id` column was checked for missing values, duplicate identifiers and inconsistent ID formats.

**Findings:**

- No missing customer IDs were identified.
- All 1,220 customer IDs were unique.
- No embedded header values were found in the data.
- Two distinct ID formats were identified.

| ID format | Number of records |
|---|---:|
| Standard format (`C` followed by four digits) | 1,200 |
| Legacy-style format (`C9X` followed by three digits) | 20 |
| **Total** | **1,220** |

The 20 legacy-style IDs follow a consistent pattern, ranging from `C9X000` to `C9X019`.

### 3.1 ID Format Observation

The presence of two ID formats may indicate that records originated from different systems or data-entry processes.

This remains a hypothesis and cannot be confirmed from the customer dataset alone.

The IDs will be preserved during the investigation. Any decision about standardising identifiers will be considered during Phase 4.

## 4. Customer Name Investigation

The customer-name column was examined to identify repeated names.

**Findings:**

- 225 unique full customer names were identified.
- 995 occurrences represent additional appearances of names beyond their first occurrence.
- Repeated names were found across multiple customer IDs.

Further checks were performed on selected repeated names.

Examples included Amanda Mahlangu, Amanda Molefe and Zanele Ndlovu.

Although these names appeared multiple times, the associated records generally contained different customer IDs, phone numbers, email addresses or locations.

**Conclusion:** Repeated full names alone do not establish that customer records are duplicates. No customer records were classified as confirmed duplicates based solely on matching names.

## 5. Email Investigation

The email column was investigated for repeated addresses and formatting inconsistencies.

### 5.1 Duplicate Email Addresses

An exact-match frequency check identified:

| Finding | Count |
|---|---:|
| Duplicated email addresses | 20 |
| Records involved | 40 |
| Potential duplicate pairs | 20 |

Each duplicated email address appeared in two records.

The 20 pairs shared:
- The same email address.
- The same full customer name.
- The same city and province.
- Phone numbers that matched after accounting for spaces and an optional leading zero.

The main difference was the customer ID format: one record used a standard ID, while the other used a legacy-style ID.

### 5.2 Potential Duplicate Records

The matching pattern provides strong evidence of potential duplicate customer records.

However, the records have not been independently verified against an authoritative customer source.

**Conclusion:** The 20 pairs are classified as potential duplicate records, not confirmed duplicates.

All original records will be retained until the appropriate cleaning and validation stage.

### 5.3 Email Formatting Inconsistencies

A whitespace check identified **80 email records containing at least one space**.

The observed pattern included spaces within the local part of the email address, particularly between surname components.

Examples include:

- `naledi.van wyk12@example.com`
- `kagiso.van wyk39@example.com`
- `david.van wyk152@example.com`

These spaces indicate potential email-formatting problems.

The investigation identifies formatting inconsistencies but does not establish whether the affected email addresses correspond to active or deliverable mailboxes.

**Decision:** The original email values will be preserved during Phase 3. Email-format standardisation will be addressed in Phase 4.

## 6. Investigation Summary

| Investigation area | Result |
|---|---|
| Missing values | 25 missing phone numbers |
| Customer IDs | 1,220 unique IDs |
| ID formats | 2 formats identified |
| Customer names | 225 unique full names |
| Repeated names | 995 additional name occurrences |
| Duplicate emails | 20 duplicated addresses |
| Potential duplicate records | 20 pairs involving 40 records |
| Email formatting | 80 records contain spaces |
| Phone recovery | No values supported for recovery |

## 7. Data Quality Decisions

The following decisions were made based on the investigation:

1. Preserve all 25 missing phone values. No unsupported values will be inserted.
2. Retain both customer ID formats for further consideration during Phase 4.
3. Do not classify repeated full names as confirmed duplicate customers.
4. Flag the 20 duplicated email pairs as potential duplicate records for further validation.
5. Flag the 80 email records containing spaces for email-format standardisation.
6. Preserve the original source file without modifications.

## 8. Phase 4 Considerations

The following issues will require attention during the cleaning and validation stage:

- Handling unresolved missing phone numbers.
- Reviewing and standardising customer ID formats where appropriate.
- Validating and standardising email formatting.
- Reviewing the 20 potential duplicate customer pairs before deciding whether any records should be merged or removed.
- Preserving data integrity and maintaining traceability to the original source records.

## 9. Final Investigation Conclusion

The Customers dataset contains 1,220 records and six columns. The investigation identified missing phone values, two customer ID formats, repeated customer names, duplicated email addresses and email-formatting inconsistencies.

The most significant finding is the presence of 20 potential duplicate customer pairs involving standard and legacy-style customer IDs. The matching email addresses and other shared attributes provide strong evidence of possible duplication, although independent confirmation is still required.

The investigation also established that the 25 missing phone numbers cannot currently be recovered using the available customer records.

No changes were made to the original source data. All identified issues and observations have been retained for consideration during Phase 4 — Data Cleaning and Standardisation.
