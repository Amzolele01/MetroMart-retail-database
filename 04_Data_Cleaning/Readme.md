# Phase 4: Data Cleaning and Validation

## Overview

This phase focuses on preparing the MetroMart retail datasets for reliable PostgreSQL database implementation.

Following the completion of Project Discovery, Data Profiling and Data Quality Investigation, the identified data quality issues will be reviewed and addressed through controlled cleaning operations and validation procedures.

The objective is to produce consistent, reliable and well-documented datasets while preserving valid business information and maintaining the integrity of the original source data.

## Objectives

- Review completed data quality investigation findings.
- Establish and document appropriate cleaning decisions.
- Create separate working copies of the original datasets.
- Apply justified and traceable cleaning operations.
- Validate cleaned datasets against defined quality requirements.
- Document cleaning formulas, transformations, decisions and unresolved issues.
- Assess dataset readiness for PostgreSQL implementation.

## Source Datasets

This phase covers the following seven datasets:

| Dataset | Original Records |
|---|---:|
| customers | 1,220 |
| customer_export_legacy | 350 |
| employees | 60 |
| stores | 5 |
| products | 20 |
| sales_2023_2025 | 100,000 |
| returns | 1,800 |
| **Total** | **103,455** |

Original source files are preserved under `01_Project_Discovery/00_Client_Source/` and will not be modified.

## Cleaning Approach

Cleaning will be performed using separate working copies in Google Sheets.

Each dataset will follow a controlled process:

1. Review previously documented investigation findings.
2. Identify issues requiring corrective action.
3. Document and justify proposed cleaning decisions.
4. Apply approved cleaning operations.
5. Validate the resulting dataset.
6. Document completed changes and any retained issues.

No information will be invented or corrected without sufficient supporting evidence.

## Phase Structure

| Directory / File | Purpose |
|---|---|
| `01_Cleaning_Strategy.md` | Cleaning methodology and workflow. |
| `02_Cleaning_Decisions/` | Dataset-specific cleaning decisions and justifications. |
| `03_Cleaned_Datasets/` | Cleaned dataset working copies. |
| `04_Validation/` | Validation procedures, formulas and results. |
| `05_Cleaning_Summary.md` | Overall cleaning outcomes and readiness assessment. |

## Working Principles

- Preserve all original source files.
- Perform cleaning on separate working copies.
- Retain valid business information.
- Avoid unsupported assumptions and corrections.
- Record significant transformations and their justifications.
- Validate every applied cleaning operation.
- Distinguish corrected issues from intentionally retained issues.
- Maintain traceability throughout the process.

## Expected Outcome

At the completion of this phase, each dataset should have a documented cleaning history, validated results and a clear assessment of its readiness for the next stage of the project: PostgreSQL database implementation.
