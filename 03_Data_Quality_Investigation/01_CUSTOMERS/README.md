# Customers Dataset — Data Quality Investigation Report

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
