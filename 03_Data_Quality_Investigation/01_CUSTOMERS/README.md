# Customers Dataset — Data Quality Investigation

## 1. Overview

This document records the data quality investigation conducted on the `customers.csv` dataset as part of Phase 3 of the MetroMart Retail Database Project.

The purpose of the investigation was to assess the completeness, consistency, uniqueness and structural reliability of customer records before proceeding to data cleaning, validation and database implementation.

The investigation was performed using Google Sheets. The original source dataset was preserved, and all checks were conducted using a separate working copy.

## 2. Dataset Structure

The dataset contains 1,220 customer records and six attributes.

| Column | Attribute |
|---|---|
| A | customer_id |
| B | cust_name |
| C | phone |
| D | email |
| E | city |
| F | province |

**Total records:** 1,220  
**Total attributes:** 6

## 3. Data Completeness and Missing Values

All six attributes were checked for missing values.

| Attribute | Missing values |
|---|---:|
| customer_id | 0 |
| cust_name | 0 |
| phone | 25 |
| email | 0 |
| city | 0 |
| province | 0 |

**Finding:**

A total of 25 customer records have missing phone numbers. No missing values were identified in the remaining five attributes.

No attempt was made to populate missing phone numbers because no supporting source information was available.

## 4. Customer ID Investigation

The customer ID column was checked for uniqueness, duplicate values and identifier structure.

**Findings:**
- Total customer IDs: 1,220.
- Unique customer IDs: 1,220.
- Duplicate customer IDs: 0.
- Two identifier structures were observed: `C####` and `C#X###`.

Both structures were retained during the investigation. Their standardization, if required, will be considered during Phase 4.

## 5. Customer Name Investigation

Customer names were examined for distinct values, repetition, whitespace and capitalization inconsistencies.

**Findings:**
- Total customer records: 1,220.
- Distinct customer names: 225.
- Names appearing more than once: 219.
- Names appearing only once: 6.
- Records belonging to repeated-name groups: 1,214.
- Repeated occurrences beyond the first occurrence: 995.
- Leading or trailing whitespace: 0.
- Capitalization inconsistencies identified: 0.

**Interpretation:**

Repeated customer names do not automatically indicate duplicate customer records. Different customers may share the same full name. Therefore, repeated names were recorded as an observation rather than classified as duplicate records.

## 6. Phone Number Investigation

Phone numbers were examined for missing values, whitespace and digit-length consistency.

### 6.1 Missing phone numbers

A total of 25 records have missing phone numbers.

### 6.2 Whitespace formatting

Twenty phone numbers contain internal spaces.

These spaces appear to be formatting separators within the numbers, for example:

`074 418 8276`

No leading or trailing whitespace was identified in the phone number column.

### 6.3 Phone number lengths

After removing formatting characters and examining the digit lengths, two distinct lengths were identified:

| Digit length | Observation |
|---|---|
| 9 digits | Associated with customer IDs following the `C###` structure |
| 10 digits | Found in the other customer records |

**Interpretation:**

The phone number column contains two different length patterns. The 9-digit numbers associated with the `C###` customer ID group may require further investigation before standardization.

No phone numbers were changed or automatically corrected.

## 7. Email Address Investigation

Email addresses were examined for missing values, uniqueness, duplication, whitespace and basic formatting consistency.

### 7.1 Completeness and uniqueness

- Missing email addresses: 0.
- Distinct email addresses: 1,200.
- Repeated email occurrences beyond the first: 20.
- Distinct duplicated email addresses: 20.
- Customer records involved in duplicated email groups: 40.

### 7.2 Duplicated email addresses

Twenty email addresses were each associated with two customer records.

The following table records the affected customer IDs and email addresses.

| Customer ID | Duplicated email address |
|---|---|
| C9X019 | nomsa.smith110@example.com |
| C9X018 | sibusiso.mthembu695@example.com |
| C9X017 | nomsa.khumalo400@example.com |
| C9X016 | brian.ndlovu1129@example.com |
| C9X015 | zanele.mabena722@example.com |
| C9X014 | mpho.jacobs595@example.com |
| C9X013 | naledi.molefe281@example.com |
| C9X012 | david.dlamini35@example.com |
| C9X011 | sipho.dlamini129@example.com |
| C9X010 | naledi.williams1133@example.com |
| C9X009 | sipho.smith47@example.com |
| C9X008 | brian.mokoena751@example.com |
| C9X007 | sibusiso.dlamini831@example.com |
| C9X006 | david.van wyk152@example.com |
| C9X005 | kagiso.naidoo1012@example.com |
| C9X004 | karabo.mabena669@example.com |
| C9X003 | karabo.pillay142@example.com |
| C9X002 | zanele.jacobs1023@example.com |
| C9X001 | nomsa.nkosi458@example.com |
| C9X000 | nomsa.williams460@example.com |

The corresponding second customer IDs were:

| Customer ID | Duplicated email address |
|---|---|
| C1133 | naledi.williams1133@example.com |
| C1129 | brian.ndlovu1129@example.com |
| C1023 | zanele.jacobs1023@example.com |
| C1012 | kagiso.naidoo1012@example.com |
| C0831 | sibusiso.dlamini831@example.com |
| C0751 | brian.mokoena751@example.com |
| C0722 | zanele.mabena722@example.com |
| C0695 | sibusiso.mthembu695@example.com |
| C0669 | karabo.mabena669@example.com |
| C0595 | mpho.jacobs595@example.com |
| C0460 | nomsa.williams460@example.com |
| C0458 | nomsa.nkosi458@example.com |
| C0400 | nomsa.khumalo400@example.com |
| C0281 | naledi.molefe281@example.com |
| C0152 | david.van wyk152@example.com |
| C0142 | karabo.pillay142@example.com |
| C0129 | sipho.dlamini129@example.com |
| C0110 | nomsa.smith110@example.com |
| C0047 | sipho.smith47@example.com |
| C0035 | david.dlamini35@example.com |

The paired records were compared using other customer attributes. The investigation found matching customer details, including names and contact information after phone-number formatting was accounted for.

These findings suggest that the duplicated email addresses may represent corresponding customer records across the two identifier groups. They should not automatically be treated as errors or deleted.

### 7.3 Email whitespace and formatting

The investigation identified 80 email addresses containing whitespace.

All 80 affected addresses contain an internal space in the surname `van wyk`.

Example:

`david.van wyk152@example.com`

Additional checks found:
- Leading or trailing whitespace: 0.
- Repeated internal whitespace: 0.
- Basic email-format validation failures: 80.

The 80 basic format-validation failures correspond to the 80 email addresses containing internal whitespace.

**Interpretation:**

The email addresses exhibit a consistent formatting issue involving the surname `van wyk`. These records require standardization during Phase 4. The original values were retained during the investigation.

## 8. City and Province Investigation

The city and province attributes were examined for distinct values, record distribution, whitespace and capitalization consistency.

### 8.1 City distribution

Seven distinct city values were identified.

| City | Records |
|---|---:|
| Fourways | 192 |
| JHB | 155 |
| Midrand | 176 |
| RANDburg | 160 |
| Roodepoort | 189 |
| Sandton | 171 |
| Soweto | 177 |
| **Total** | **1,220** |

### 8.2 Province distribution

| Province | Records |
|---|---:|
| Gauteng | 1,220 |

All customer records are associated with Gauteng.

### 8.3 Location formatting

No leading or trailing whitespace was identified in the city or province attributes. No capitalization inconsistencies were identified by the checks performed.

However, the following city-label differences were observed:
- `JHB` and `Johannesburg`
- `RANDburg` and `Randburg`

The `Johannesburg` and `Randburg` forms were observed in the separate `customer_export_legacy.csv` dataset.

These differences should be considered during Phase 4 when standardizing location values across customer datasets.

## 9. Summary of Data Quality Findings

| Area | Finding |
|---|---|
| Dataset completeness | 25 missing phone numbers |
| Customer IDs | 1,220 unique IDs; no duplicates |
| ID structures | Two observed formats |
| Customer names | 219 names appear more than once |
| Phone numbers | 9- and 10-digit patterns |
| Phone formatting | 20 numbers contain internal spaces |
| Email duplication | 20 duplicated addresses involving 40 records |
| Email formatting | 80 addresses contain internal whitespace |
| City values | 7 distinct city labels |
| Province values | All 1,220 records contain Gauteng |
| Location naming | `JHB`/`Johannesburg` and `RANDburg`/`Randburg` differences |

## 10. Recommendations for Phase 4

The following items should be considered during data cleaning and validation:

1. Investigate the 25 missing phone numbers. Do not populate them without reliable supporting information.
2. Review the 9-digit phone number pattern associated with the `C###` customer ID group before deciding whether standardization is appropriate.
3. Standardize phone number formatting where justified, including the 20 numbers containing internal spaces.
4. Review the 80 email addresses containing internal spaces and establish a consistent email-formatting rule.
5. Investigate the duplicated email groups and preserve their relationship until the appropriate customer-record treatment is established.
6. Standardize city labels across customer datasets, particularly `JHB`/`Johannesburg` and `RANDburg`/`Randburg`.
7. Retain repeated customer names unless additional evidence establishes that records represent duplicate customers.

## 11. Investigation Methodology and Formulas

The investigation was conducted in Google Sheets using formulas and filtered outputs. The following formulas were used or applied during the investigation.

**Missing values — customer IDs**

`=COUNTBLANK(A2:A1221)`

The same `COUNTBLANK` approach was applied to the remaining attributes by changing the column reference.

**Duplicate customer IDs**

`=IFERROR(UNIQUE(FILTER(A2:A1221,COUNTIF(A2:A1221,A2:A1221)>1)),"None")`

**Distinct customer names**

`=COUNTUNIQUE(B2:B1221)`

**Names appearing more than once**

`=COUNTUNIQUE(FILTER(B2:B1221,COUNTIF(B2:B1221,B2:B1221)>1))`

**Repeated occurrences beyond the first**

`=COUNTA(B2:B1221)-COUNTUNIQUE(B2:B1221)`

**Records belonging to repeated-name groups**

`=COUNTIF(ARRAYFORMULA(COUNTIF(B2:B1221,B2:B1221)),">1")`

**Phone numbers containing whitespace**

`=FILTER({A2:A1221,B2:B1221,C2:C1221},REGEXMATCH(C2:C1221,"\s"))`

**Distinct phone-number lengths after removing formatting**

`=SORT(UNIQUE(ARRAYFORMULA(LEN(REGEXREPLACE(FILTER(C2:C1221,C2:C1221<>""),"[^0-9]","")))))`

**Distinct email addresses**

`=COUNTUNIQUE(D2:D1221)`

**Duplicated email addresses**

`=UNIQUE(FILTER(D2:D1221,COUNTIF(D2:D1221,D2:D1221)>1))`

**Email addresses containing whitespace**

`=FILTER({A2:A1221,D2:D1221},REGEXMATCH(D2:D1221,"\s"))`

**Email leading/trailing or repeated internal whitespace**

`=SUM(ARRAYFORMULA(N(LEN(D2:D1221)<>LEN(TRIM(D2:D1221)))))`

**Email addresses failing basic format validation**

`=SUM(ARRAYFORMULA(N(NOT(REGEXMATCH(D2:D1221,"^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$")))))`

**Distinct city values**

`=SORT(UNIQUE(E2:E1221))`

**City distribution**

`=QUERY(E2:E1221,"SELECT E, COUNT(E) WHERE E IS NOT NULL GROUP BY E LABEL COUNT(E) 'Records'",0)`

**Distinct province values**

`=SORT(UNIQUE(F2:F1221))`

**Province distribution**

`=QUERY(F2:F1221,"SELECT F, COUNT(F) WHERE F IS NOT NULL GROUP BY F LABEL COUNT(F) 'Records'",0)`

Additional whitespace and capitalization checks were also performed on customer names, phone numbers, email addresses, cities and provinces.

## 12. Conclusion

The investigation established that the `customers.csv` dataset contains 1,220 records with six attributes. Although most attributes are complete and customer IDs are unique, several data quality observations were identified, particularly missing phone numbers, inconsistent phone number lengths, email formatting issues, duplicated email addresses and location naming differences.

The findings have been recorded for consideration during Phase 4. No corrections were made to the original source dataset during this investigation.

**Investigation status: Completed.**# Customers Dataset — Data Quality Investigation Report

## 1. Dataset Overview

**Dataset:** `customers.csv`  
**Investigation phase:** Phase 3 — Data Quality Investigation  
**Total records:** 1,220  
**Total attributes:** 6

The Customers dataset contains customer information used by the MetroMart retail system.

The investigation was conducted using a working copy in Google Sheets. The original source dataset was not modified.

### Attributes investigated

| Column | Attribute |
|---|---|
| A | customer_id |
| B | cust_name |
| C | phone |
| D | email |
| E | city |
| F | province |

## 2. Completeness Investigation

The first investigation examined missing values across all six attributes.

### Results

- `customer_id`: 0 missing values
- `cust_name`: 0 missing values
- `phone`: 25 missing values
- `email`: 0 missing values
- `city`: 0 missing values
- `province`: 0 missing values

A total of 25 records have missing phone numbers.

This represents approximately 2.05% of the dataset.

### Formula used

The `COUNTBLANK` function was used to identify missing values in each attribute.

Example for the phone column:

```excel
=COUNTBLANK(C2:C1221)
```

### Investigation of missing phone numbers

The affected records were extracted for inspection.

The investigation established that:
- 25 customer records have no phone number.
- The other five attributes have no missing values.
- The missing phone numbers were not filled in because no supporting source information was available.

**Finding:** Missing phone numbers were identified in 25 records. These values were retained as missing rather than replaced with invented information.

## 3. Customer ID Investigation

The `customer_id` attribute was examined for uniqueness and consistency.

### Results

- Total customer records: 1,220
- Unique customer IDs: 1,220
- Duplicate customer IDs: 0
- Missing customer IDs: 0

The investigation also identified two groups of customer identifiers:

- 1,200 standard customer IDs.
- 20 legacy customer IDs.

Although the identifiers came from different ID groups, they were unique within the dataset.

### Formula used

```excel
=COUNTUNIQUE(A2:A1221)
```

**Finding:** All 1,220 customer records have unique customer IDs. No duplicate customer identifiers were identified.

The presence of legacy identifiers was recorded for consideration during later standardization and database design.

## 4. Customer Name Investigation

The `cust_name` attribute was examined for repeated names.

### Results

- Total customer records: 1,220
- Distinct customer names: 225
- Records containing repeated names: 995

Repeated names were investigated to determine whether they represented duplicate customer records.

The investigation established that repeated names alone were not sufficient evidence of duplicate customers because different customers can share the same name.

For example, Brian Van Wyk appeared in five records. Repeated names were therefore treated as observations requiring comparison with other customer attributes rather than automatic duplicate classifications.

**Finding:** Repeated customer names were identified, but they were not automatically classified as duplicate customer records.

## 5. Phone Number Investigation

The phone attribute was examined for missing values and its relationship with other customer information.

### Results

- Missing phone numbers: 25
- Customer records with available phone numbers: 1,195

The missing phone numbers were retained because there was no reliable supporting information available to fill them.

The investigation also checked the records with duplicated email addresses against missing phone numbers.

**Finding:** None of the records with duplicated email addresses had missing phone numbers.

No phone numbers were invented or added during the investigation.

## 6. Email Investigation

The `email` attribute was examined for repeated values and formatting inconsistencies.

### 6.1 Duplicate Email Addresses

The investigation identified 20 duplicated email addresses involving 40 customer records.

The affected customer IDs and their corresponding email addresses were recorded for reference.

Repeated email addresses were treated as potential data quality issues rather than automatic proof that the customer records were duplicates.

The investigation also established that none of these 40 records had missing phone numbers.

**Finding:** Twenty email addresses were duplicated across 40 customer records. These records require careful consideration during cleaning because a shared email address does not necessarily establish that two customer records represent the same person.

### 6.2 Email Whitespace Investigation

The investigation identified 80 email records containing whitespace inconsistencies.

These were recorded as formatting issues for consideration during Phase 4.

**Finding:** Email formatting inconsistencies were identified. The original values were retained during Phase 3.

## 7. City and Province Investigation

The `city` and `province` attributes were examined for completeness and naming consistency.

Both attributes had zero missing values.

The investigation identified city-label variations, including:

- `JHB`
- `Johannesburg`
- `RANDburg`
- `Randburg`

These observations were retained for consideration during the cleaning and standardization stage.

The presence of different labels was not treated as proof that the underlying customer locations were different.

**Finding:** City-label inconsistencies were identified for later standardization. No source values were changed during the investigation.

## 8. Investigation Decisions

The following decisions were established:

1. Missing phone numbers were retained because no reliable supporting information was available.
2. Repeated customer names were not automatically classified as duplicate customer records.
3. Duplicate email addresses were documented for further investigation.
4. Email whitespace inconsistencies were recorded for later cleaning.
5. Legacy customer identifiers were retained because they were unique.
6. City-label inconsistencies were deferred to the cleaning and standardization stage.
7. The original source dataset was not modified.

## 9. Conclusion

The investigation of `customers.csv` identified several data quality observations involving missing phone numbers, repeated names, duplicate email addresses, email whitespace and city-label inconsistencies.

The dataset contains 1,220 records and six attributes. All customer IDs are unique, and no missing values were identified outside the phone attribute.

The main findings are:

- 25 missing phone numbers.
- 1,220 unique customer IDs, including 1,200 standard IDs and 20 legacy IDs.
- 225 distinct customer names, with repeated names requiring careful interpretation.
- 20 duplicated email addresses involving 40 records.
- 80 email records containing whitespace inconsistencies.
- City-label variations requiring standardization.

No unsupported corrections were made during the investigation.

**Final investigation status:** Completed. The identified observations and unresolved issues were recorded for consideration during Phase 4 — Data Cleaning and Validation.
