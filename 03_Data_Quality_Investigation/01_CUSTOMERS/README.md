# Data Quality Investigation Report: Customers Dataset

## 1. Dataset Overview

**Source file:** `customers.csv`  
**Investigation phase:** Phase 3 — Data Quality Investigation  
**Investigation tool:** Google Sheets  
**Total records:** 1,220  
**Total attributes:** 6

The Customers dataset was investigated to assess its completeness, uniqueness, consistency, structural reliability and potential data-quality issues before proceeding to data cleaning, validation and database implementation.

The investigation was conducted using a separate Google Sheets working copy. The original source dataset was preserved without modifications.

### Dataset Structure

| Column | Attribute |
|---|---|
| A | customer_id |
| B | cust_name |
| C | phone |
| D | email |
| E | city |
| F | province |

## 2. Data Completeness and Missing Values

All six attributes were examined for missing values.

| Attribute | Missing values |
|---|---:|
| customer_id | 0 |
| cust_name | 0 |
| phone | 25 |
| email | 0 |
| city | 0 |
| province | 0 |
| **Total** | **25** |

A total of 25 customer records contain missing phone numbers. No missing values were identified in the remaining five attributes.

This represents approximately 2.05% of the dataset.

### 2.1 Missing Phone Numbers by City

The missing phone records were grouped by city to examine their distribution.

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
- Matching names generally had different email addresses and, in several cases, different cities.
- No confirmed identity matches provided sufficient evidence to recover the missing phone numbers.

**Investigation decision:** All 25 missing phone values were retained as unresolved missing values. No phone numbers were populated without reliable supporting evidence.

## 3. Customer ID Investigation

The `customer_id` attribute was examined for completeness, uniqueness, duplicate identifiers and structural consistency.

### 3.1 Uniqueness and Completeness

**Findings:**

- Total customer records: 1,220.
- Unique customer IDs: 1,220.
- Duplicate customer IDs: 0.
- Missing customer IDs: 0.
- No embedded header values were identified in the data.

### 3.2 Customer ID Formats

Two distinct customer ID formats were identified.

| ID format | Number of records |
|---|---:|
| Standard format (`C` followed by four digits) | 1,200 |
| Legacy-style format (`C9X` followed by three digits) | 20 |
| **Total** | **1,220** |

The 20 legacy-style identifiers follow a consistent pattern, ranging from `C9X000` to `C9X019`.

Both formats were unique within the dataset.

### 3.3 ID Format Observation

The presence of two identifier formats may indicate that customer records originated from different systems or data-entry processes.

This remains a hypothesis and cannot be confirmed from the Customers dataset alone.

The identifiers were preserved during the investigation. Any decision about standardising or mapping these identifiers will be considered during Phase 4.

## 4. Customer Name Investigation

The `cust_name` attribute was examined for distinct values, repeated names, whitespace and capitalization inconsistencies.

### 4.1 Name Distribution

| Finding | Count |
|---|---:|
| Total customer records | 1,220 |
| Distinct customer names | 225 |
| Names appearing more than once | 219 |
| Names appearing only once | 6 |
| Records belonging to repeated-name groups | 1,214 |
| Additional occurrences beyond the first | 995 |

No leading or trailing whitespace or capitalization inconsistencies were identified by the checks performed.

### 4.2 Repeated Name Investigation

Repeated names were examined to determine whether they represented duplicate customer records.

Examples included Brian Van Wyk, who appeared in five customer records, as well as Amanda Mahlangu, Amanda Molefe and Zanele Ndlovu.

The investigation established that repeated names alone do not provide sufficient evidence to classify records as duplicates. Different customers may share the same full name, while other identifying attributes may differ.

**Investigation decision:** Repeated customer names were recorded as an observation rather than classified as confirmed duplicate records. No records were removed or merged based solely on matching names.

## 5. Phone Number Investigation

The `phone` attribute was examined for completeness, whitespace formatting and digit-length consistency.

### 5.1 Missing Phone Numbers

A total of 25 records have missing phone numbers.

The remaining 1,195 records contain populated phone values.

The missing values were retained because no reliable supporting information was available to recover them.

### 5.2 Phone Number Whitespace

Twenty phone numbers contain internal spaces.

These spaces appear to be formatting separators within the numbers.

Example:

`074 418 8276`

No leading or trailing whitespace was identified in the phone number column.

### 5.3 Phone Number Digit Lengths

After removing formatting characters and examining the digit lengths, two distinct patterns were identified.

| Customer ID group | Phone number length |
|---|---:|
| Standard-format IDs (`C####`) | 9 digits |
| Legacy-style IDs (`C9X###`) | 10 digits |

The observed digit-length patterns correspond to the two customer ID groups.

This relationship was recorded as an observation. The investigation did not establish that either pattern was incorrect.

**Investigation decisions:**

- Preserve all original phone values.
- Do not automatically add or remove digits.
- Retain the 20 phone numbers containing internal spaces for consideration during Phase 4.
- Investigate the different phone-number patterns before deciding whether standardisation is appropriate.

## 6. Email Address Investigation

The `email` attribute was examined for completeness, uniqueness, duplicated values, whitespace and basic formatting consistency.

### 6.1 Completeness and Uniqueness

| Finding | Count |
|---|---:|
| Total email records | 1,220 |
| Missing email addresses | 0 |
| Distinct email addresses | 1,200 |
| Duplicated email addresses | 20 |
| Repeated occurrences beyond the first | 20 |
| Customer records involved in duplicated email groups | 40 |

### 6.2 Duplicated Email Addresses

An exact-match frequency check identified 20 duplicated email addresses. Each address appeared in two customer records, creating 20 potential duplicate pairs involving 40 records.

The affected records were compared using other customer attributes.

The investigation found that each pair shared:

- The same email address.
- The same full customer name.
- The same city and province.
- Matching phone numbers after accounting for formatting spaces and an optional leading zero.

The main difference was the customer ID format: one record used a standard-format ID, while the other used a legacy-style ID.

### 6.2.1 Records with Duplicated Email Addresses

The following records were identified through the exact email-match investigation.

| Customer ID | Email address |
|---|---|
| C0035 | david.dlamini35@example.com |
| C9X012 | david.dlamini35@example.com |
| C0047 | sipho.smith47@example.com |
| C9X009 | sipho.smith47@example.com |
| C0110 | nomsa.smith110@example.com |
| C9X019 | nomsa.smith110@example.com |
| C0129 | sipho.dlamini129@example.com |
| C9X011 | sipho.dlamini129@example.com |
| C0142 | karabo.pillay142@example.com |
| C9X003 | karabo.pillay142@example.com |
| C0152 | david.van wyk152@example.com |
| C9X006 | david.van wyk152@example.com |
| C0281 | naledi.molefe281@example.com |
| C9X013 | naledi.molefe281@example.com |
| C0400 | nomsa.khumalo400@example.com |
| C9X017 | nomsa.khumalo400@example.com |
| C0458 | nomsa.nkosi458@example.com |
| C9X001 | nomsa.nkosi458@example.com |
| C0460 | nomsa.williams460@example.com |
| C9X000 | nomsa.williams460@example.com |
| C0595 | mpho.jacobs595@example.com |
| C9X014 | mpho.jacobs595@example.com |
| C0669 | karabo.mabena669@example.com |
| C9X004 | karabo.mabena669@example.com |
| C0695 | sibusiso.mthembu695@example.com |
| C9X018 | sibusiso.mthembu695@example.com |
| C0722 | zanele.mabena722@example.com |
| C9X015 | zanele.mabena722@example.com |
| C0751 | brian.mokoena751@example.com |
| C9X008 | brian.mokoena751@example.com |
| C0831 | sibusiso.dlamini831@example.com |
| C9X007 | sibusiso.dlamini831@example.com |
| C1012 | kagiso.naidoo1012@example.com |
| C9X005 | kagiso.naidoo1012@example.com |
| C1023 | zanele.jacobs1023@example.com |
| C9X002 | zanele.jacobs1023@example.com |
| C1129 | brian.ndlovu1129@example.com |
| C9X016 | brian.ndlovu1129@example.com |
| C1133 | naledi.williams1133@example.com |
| C9X010 | naledi.williams1133@example.com |

**Observation:** Every duplicated email address is shared between one standard-format customer ID and one legacy-style customer ID.

### 6.2.2 Potential Duplicate Customer Records

The matching attributes provide strong evidence that the 20 pairs may represent corresponding customer records across the two identifier groups.

However, the records have not been independently verified against an authoritative customer source.

**Investigation decision:** The 20 pairs are classified as potential duplicate customer records, not confirmed duplicates. All original records will be retained pending further validation.

None of the 40 records involved in duplicated email groups had a missing phone number.

### 6.3 Email Whitespace and Formatting

The investigation identified 80 email records containing internal whitespace.

All 80 affected addresses contain an internal space in the surname `van wyk`.

Examples include:

- `naledi.van wyk12@example.com`
- `kagiso.van wyk39@example.com`
- `david.van wyk152@example.com`

Additional checks established:

| Check | Finding |
|---|---:|
| Email records containing whitespace | 80 |
| Leading or trailing whitespace | 0 |
| Repeated internal whitespace | 0 |
| Basic email-format validation failures | 80 |

The 80 basic format-validation failures correspond to the 80 email addresses containing internal whitespace.

These findings indicate a consistent formatting issue. However, the investigation does not establish whether the affected email addresses correspond to active or deliverable mailboxes.

**Investigation decision:** Original email values were preserved. Email-format standardisation will be considered during Phase 4.

## 7. City and Province Investigation

The `city` and `province` attributes were examined for completeness, distinct values, record distribution, whitespace and capitalization consistency.

### 7.1 City Distribution

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

### 7.2 Province Distribution

| Province | Records |
|---|---:|
| Gauteng | 1,220 |

All customer records are associated with Gauteng.

### 7.3 Location Formatting and Naming Differences

No leading or trailing whitespace or capitalization inconsistencies were identified by the checks performed on the Customers dataset.

However, city-label differences were observed:

- `JHB` and `Johannesburg`
- `RANDburg` and `Randburg`

The `Johannesburg` and `Randburg` forms were observed in the separate `customer_export_legacy.csv` dataset.

These differences should be considered when standardising location values across the customer datasets.

**Investigation decision:** The original city and province values were retained. Cross-dataset location standardisation will be considered during Phase 4.

## 8. Consolidated Data Quality Findings

| Investigation area | Finding |
|---|---|
| Dataset completeness | 25 missing phone numbers |
| Customer IDs | 1,220 unique IDs; no duplicates |
| ID formats | 1,200 standard IDs and 20 legacy-style IDs |
| Customer names | 225 distinct names |
| Repeated-name groups | 219 names appearing more than once |
| Additional name occurrences | 995 |
| Phone number completeness | 1,195 populated values |
| Phone number formatting | 20 numbers contain internal spaces |
| Phone number lengths | 9-digit and 10-digit patterns associated with different ID groups |
| Duplicate emails | 20 duplicated addresses involving 40 records |
| Potential duplicate records | 20 potential pairs |
| Email formatting | 80 addresses contain internal whitespace |
| City values | 7 distinct city labels |
| Province values | All 1,220 records contain Gauteng |
| Location naming | JHB/Johannesburg and RANDburg/Randburg differences |

## 9. Investigation Decisions

The following decisions were established during Phase 3:

1. Preserve all 25 missing phone values because no reliable supporting information was available.
2. Retain both customer ID formats pending further consideration.
3. Do not classify repeated customer names as confirmed duplicate records.
4. Flag the 20 duplicated email pairs as potential duplicate customer records.
5. Preserve the original email values and flag the 80 affected records for formatting standardisation.
6. Retain the phone-number formatting and digit-length observations without automatically changing the values.
7. Preserve original city and province values.
8. Retain all original customer records. No records were deleted, merged or modified.
9. Maintain the original source dataset separately from the investigation and future cleaning copies.

## 10. Phase 4 Considerations

The following issues will require attention during the data cleaning and validation stage:

- Handling the 25 unresolved missing phone numbers.
- Reviewing the two customer ID formats and deciding whether standardisation or identifier mapping is appropriate.
- Reviewing the 9-digit and 10-digit phone-number patterns before deciding on standardisation.
- Standardising phone-number formatting where justified.
- Reviewing the 20 potential duplicate customer pairs before deciding whether any records should be merged or otherwise reconciled.
- Standardising the 80 email addresses containing internal spaces, while preserving traceability to their original values.
- Standardising city labels across customer datasets, particularly JHB/Johannesburg and RANDburg/Randburg.
- Validating customer ID relationships with sales and returns records during cross-dataset validation.

These are considerations for the subsequent phase, not corrections performed during this investigation.

## 11. Investigation Methods and Google Sheets Formulas

Google Sheets was used to perform data profiling, identify data-quality issues and validate investigation findings.

The formulas below document the checks performed during the investigation. The source data was not modified by these formulas.

### 11.1 Missing Values

**Purpose:** Count missing values in each attribute.

```excel
=COUNTBLANK(A2:A1221)
```

The formula was adjusted for each column by changing the column reference.

**Extract records with missing phone numbers:**

```excel
=FILTER(A2:F1221,C2:C1221="")
```

**Count missing phone numbers by city:**

```excel
=QUERY(FILTER(E2:E1221,C2:C1221=""),"SELECT Col1, COUNT(Col1) GROUP BY Col1 LABEL Col1 'City', COUNT(Col1) 'Missing Phones'",0)
```

### 11.2 Customer ID Validation

**Check for embedded header values:**

```excel
=COUNTIF(A2:A1221,"customer_id")
```

**Count standard-format IDs:**

```excel
=COUNTIF(A2:A1221,"C????")
```

**Count legacy-style IDs:**

```excel
=COUNTIF(A2:A1221,"C9X???")
```

**Check for duplicate IDs:**

```excel
=COUNTA(A2:A1221)-COUNTUNIQUE(A2:A1221)
```

**Extract duplicate customer IDs:**

```excel
=IFERROR(UNIQUE(FILTER(A2:A1221,COUNTIF(A2:A1221,A2:A1221)>1)),"None")
```

### 11.3 Customer Name Investigation

**Count distinct customer names:**

```excel
=COUNTUNIQUE(B2:B1221)
```

**Count names appearing more than once:**

```excel
=COUNTUNIQUE(FILTER(B2:B1221,COUNTIF(B2:B1221,B2:B1221)>1))
```

**Calculate additional occurrences beyond the first:**

```excel
=COUNTA(B2:B1221)-COUNTUNIQUE(B2:B1221)
```

**Calculate records belonging to repeated-name groups:**

```excel
=COUNTIF(ARRAYFORMULA(COUNTIF(B2:B1221,B2:B1221)),">1")
```

**Extract repeated names:**

```excel
=SORT(UNIQUE(FILTER(B2:B1221,COUNTIF(B2:B1221,B2:B1221)>1)))
```

**Calculate the frequency of a selected unique name (where J2 contains the name):**

```excel
=COUNTIF($B$2:$B$1221,J2)
```

### 11.4 Phone Number Investigation

**Extract phone numbers containing whitespace:**

```excel
=FILTER({A2:A1221,B2:B1221,C2:C1221},REGEXMATCH(C2:C1221,"\s"))
```

**Count populated phone numbers:**

```excel
=COUNTA(C2:C1221)
```

**Count missing phone numbers:**

```excel
=COUNTBLANK(C2:C1221)
```

**Examine distinct phone-number digit lengths after removing formatting characters:**

```excel
=SORT(UNIQUE(ARRAYFORMULA(LEN(REGEXREPLACE(FILTER(C2:C1221,C2:C1221<>""),"[^0-9]","")))))
```

**Group populated phone numbers by digit length:**

```excel
=QUERY(ARRAYFORMULA(IF(C2:C1221="","",LEN(REGEXREPLACE(C2:C1221,"[^0-9]","")))),"SELECT Col1, COUNT(Col1) WHERE Col1 IS NOT NULL GROUP BY Col1 LABEL Col1 'Digit Length', COUNT(Col1) 'Records'",0)
```

The digit-length results were examined alongside customer ID formats to identify the observed relationship between the two groups.

### 11.5 Duplicate Email Investigation

**Count distinct email addresses:**

```excel
=COUNTUNIQUE(D2:D1221)
```

**Generate a sorted list of unique email addresses:**

```excel
=SORT(UNIQUE(FILTER(D2:D1221,D2:D1221<>"")))
```

**Calculate the frequency of an email address (where L2 contains the email):**

```excel
=COUNTIF($D$2:$D$1221,L2)
```

**Extract duplicated email addresses:**

```excel
=UNIQUE(FILTER(D2:D1221,COUNTIF(D2:D1221,D2:D1221)>1))
```

**Retrieve all customer records associated with duplicated email addresses:**

```excel
=FILTER(A2:F1221,ISNUMBER(MATCH(D2:D1221,FILTER(L2:L1221,M2:M1221>1),0)))
```

### 11.6 Email Formatting Investigation

**Extract email addresses containing whitespace:**

```excel
=FILTER({A2:A1221,D2:D1221},REGEXMATCH(D2:D1221,"\s"))
```

**Count email addresses containing whitespace:**

```excel
=COUNTIF(D2:D1221,"* *")
```

**Check for leading, trailing or repeated internal whitespace:**

```excel
=SUM(ARRAYFORMULA(N(LEN(D2:D1221)<>LEN(TRIM(D2:D1221)))))
```

**Count email addresses failing basic format validation:**

```excel
=SUM(ARRAYFORMULA(N(NOT(REGEXMATCH(D2:D1221,"^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$")))))
```

### 11.7 City and Province Investigation

**Extract distinct city values:**

```excel
=SORT(UNIQUE(E2:E1221))
```

**Calculate city distribution:**

```excel
=QUERY(E2:E1221,"SELECT Col1, COUNT(Col1) WHERE Col1 IS NOT NULL GROUP BY Col1 LABEL Col1 'City', COUNT(Col1) 'Records'",0)
```

**Extract distinct province values:**

```excel
=SORT(UNIQUE(F2:F1221))
```

**Calculate province distribution:**

```excel
=QUERY(F2:F1221,"SELECT Col1, COUNT(Col1) WHERE Col1 IS NOT NULL GROUP BY Col1 LABEL Col1 'Province', COUNT(Col1) 'Records'",0)
```

Additional whitespace and capitalization checks were also performed on customer names, phone numbers, email addresses, cities and provinces.

## 12. Conclusion

The Customers dataset contains 1,220 records and six attributes. The investigation established that all customer IDs are unique and that no missing values occur outside the phone attribute.

Several data-quality observations were identified, particularly missing phone numbers, different customer ID and phone-number patterns, repeated customer names, duplicated email addresses, email-formatting inconsistencies and location naming differences.

The most significant findings include:

- 25 unresolved missing phone numbers.
- 1,220 unique customer IDs across two identifier formats.
- 225 distinct customer names, including 219 repeated-name groups.
- 20 duplicated email addresses involving 40 records, classified as 20 potential duplicate pairs.
- 80 email addresses containing internal whitespace.
- 20 phone numbers containing internal spaces.
- Two observed phone-number digit-length patterns associated with the customer ID groups.
- City-label differences requiring cross-dataset standardisation.

The investigation did not establish sufficient evidence to populate missing phone numbers or automatically merge potential duplicate customer records.

No corrections were made to the original source dataset. All identified issues, observations and investigation decisions have been retained for consideration during Phase 4 — Data Cleaning and Validation.

**Investigation status: Completed.**
