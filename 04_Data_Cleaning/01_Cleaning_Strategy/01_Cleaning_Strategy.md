
# Data Cleaning Strategy

## 1. Purpose

This document defines the methodology and principles that will guide data cleaning and validation throughout the MetroMart Retail Database Project.

Following the completion of Project Discovery, Data Profiling and Data Quality Investigation, this stage focuses on addressing identified data quality issues and preparing reliable datasets for PostgreSQL database implementation.

The strategy establishes a consistent, controlled and traceable approach to cleaning while preserving the integrity of the original source information.

## 2. Scope

The cleaning process covers the seven source datasets:

- customers
- customer_export_legacy
- employees
- stores
- products
- sales_2023_2025
- returns

Cleaning activities will be guided by the findings documented during the previous data quality investigation phase.

Only issues supported by investigation findings or subsequent validation evidence will be considered for correction.

## 3. Data Preservation and Working Environment

Original source datasets will remain unchanged throughout the project.

All cleaning activities will be performed using separate working copies in Google Sheets.

The working process will distinguish between:

- **Original datasets:** Unmodified source files preserved under `01_Project_Discovery/00_Client_Source/`.
- **Working datasets:** Copies used for cleaning, testing and intermediate transformations.
- **Cleaned datasets:** Final outputs that have undergone the approved cleaning operations and validation procedures.

Temporary working copies will be maintained separately from the final project outputs. Only approved cleaned datasets will be transferred into the `03_Cleaned_Datasets/` directory.

## 4. Cleaning Decision Framework

Before applying any cleaning operation, identified issues will be evaluated and assigned an appropriate treatment.

The following classifications will guide decisions:

| Classification | Description |
|---|---|
| Requires Correction | An identified error or invalid value that can be corrected using sufficient supporting evidence. |
| Requires Standardisation | Valid information represented inconsistently that should follow an agreed format or convention. |
| Retain As-Is | An unusual or potentially problematic value that is nevertheless valid and should be preserved. |
| Requires Further Evidence | An issue that cannot be reliably resolved using the available information. |
| Excluded From Cleaning | A finding that does not require a transformation for the intended database implementation. |

Cleaning decisions must consider the business meaning of the information, relationships between datasets and the potential impact of each transformation.

Missing information will not be fabricated, and ambiguous values will not be corrected through unsupported assumptions.

## 5. Cleaning Methodology

Each dataset will follow a consistent cleaning process.

### 5.1 Review Existing Findings

Review the corresponding data quality investigation documentation to identify:

- Confirmed data quality issues.
- Previously identified inconsistencies.
- Potential relationships with other datasets.
- Issues intentionally retained during investigation.
- Findings that require no corrective action.

Previously completed investigations will not be repeated unless additional validation is necessary.

### 5.2 Establish Cleaning Decisions

Determine which findings require corrective action and document the intended treatment before making changes.

Each significant decision should include:

- The issue identified.
- The affected field or records.
- The proposed cleaning operation.
- The justification for the decision.
- Any limitations or potential impact.

### 5.3 Apply Cleaning Operations

Perform approved transformations using Google Sheets.

Depending on the dataset and identified issues, operations may include:

- Correcting confirmed invalid values.
- Standardising inconsistent text representations.
- Removing unnecessary leading or trailing spaces.
- Correcting data formats where appropriate.
- Handling missing values when reliable supporting information exists.
- Resolving confirmed duplicates where their removal is justified.
- Correcting other verified inconsistencies.

Transformations must preserve valid information and avoid unnecessary changes.

### 5.4 Record Changes

Significant cleaning operations must be traceable.

Documentation should identify:

- The affected dataset and field.
- The original condition.
- The cleaning operation applied.
- The formula or method used.
- The resulting condition.
- The reason for the transformation.

Where practical, before-and-after results will be retained to demonstrate the impact of cleaning.

## 6. Validation Methodology

Validation will be performed after cleaning operations to establish whether the resulting datasets satisfy the expected quality requirements.

Checks will be selected according to the dataset structure and the issues identified during investigation.

Validation may include:

| Validation Area | Purpose |
|---|---|
| Completeness | Verify required fields and assess remaining missing values. |
| Uniqueness | Confirm that fields expected to be unique contain no unintended duplicates. |
| Consistency | Check standardised values and formatting conventions. |
| Validity | Verify that values conform to expected formats, types and business rules. |
| Referential Integrity | Confirm that relevant identifiers correspond to valid records in related datasets. |
| Record Integrity | Confirm that cleaning has not caused unintended record loss or duplication. |

Validation results will be compared against the original investigation findings where applicable.

A dataset will not be considered fully validated merely because a cleaning operation completed successfully.

## 7. Handling Unresolved Issues

Not every identified data quality issue will necessarily be corrected.

Where reliable supporting information is unavailable, the affected information will be retained or handled according to an explicitly documented decision.

Unresolved issues will be recorded with:

- A description of the issue.
- The reason it remains unresolved.
- Its potential impact.
- Any considerations for subsequent database implementation.

The objective is to preserve data integrity rather than achieve artificial completeness.

## 8. Documentation and Traceability

Each dataset will have separate cleaning decision and validation documentation.

The documentation will provide an account of:

- Issues selected for cleaning.
- Approved cleaning decisions.
- Operations and formulas applied.
- Relevant before-and-after results.
- Validation procedures and outcomes.
- Issues intentionally retained.
- Outstanding limitations.

The overall cleaning process will be summarised in `05_Cleaning_Summary.md`.

GitHub will serve as the project's version-controlled documentation and final dataset repository.

## 9. Dataset Readiness Assessment

Following cleaning and validation, each dataset will receive a readiness assessment.

The assessment will consider:

- Whether approved cleaning operations have been completed.
- Whether relevant validation checks have passed.
- Whether unresolved issues have been documented.
- Whether the dataset is suitable for its intended role in the PostgreSQL implementation.

Possible outcomes will include:

- **Ready:** Cleaning and required validation have been completed, with no outstanding issues preventing implementation.
- **Ready With Documented Limitations:** The dataset is suitable for implementation, but certain issues have intentionally been retained or require consideration.
- **Further Work Required:** Outstanding issues or failed validation checks prevent the dataset from being approved for implementation.

Readiness will be determined by the actual validation results rather than by the number of issues corrected.

## 10. Expected Outcome

The completion of this phase should produce cleaned and validated datasets supported by documented decisions, reproducible operations and clear validation evidence.

The resulting datasets will provide the foundation for the next project stage: PostgreSQL database implementation.
