# Phase 2: Data Profiling

## Overview

This phase focuses on understanding the structure, content, and characteristics of the source datasets provided for the MetroMart Retail Database Project.

The profiling exercise establishes an initial overview of the available data before detailed data quality investigation, preparation, and database implementation.

It examines dataset structures, field characteristics, record counts, missing values, uniqueness, value distributions, and potential relationships between datasets.

## Objectives

The objectives of this phase are to:

- Establish an inventory of all available source datasets.
- Document the fields and their intended business meanings.
- Examine the structure and characteristics of each dataset.
- Identify potential identifiers and repeated values.
- Record initial observations about missing values and inconsistent representations.
- Identify potential relationships between datasets.
- Establish a documented baseline for subsequent project stages.

## Documentation Structure

| File / Folder | Description |
|---|---|
| `01_Data_Source_Inventory.md` | Provides an overview of the supplied datasets, including their record counts, field counts, and general purpose. |
| `02_Data_Dictionary.md` | Documents the available business definitions and field descriptions across the source datasets. |
| `03_Dataset_Profiling/` | Contains individual profiling reports for all seven datasets. |
| `04_Relationship_Discovery.md` | Documents potential relationships identified between datasets. |
| `05_Profiling_Summary.md` | Consolidates the main findings and observations from the profiling exercise. |

## Dataset Profiles

The `03_Dataset_Profiling/` folder contains the following reports:

- [Customers](03_Dataset_Profiling/customers.md)
- [Legacy Customers](03_Dataset_Profiling/customer_export_legacy.md)
- [Employees](03_Dataset_Profiling/employees.md)
- [Stores](03_Dataset_Profiling/stores.md)
- [Products](03_Dataset_Profiling/products.md)
- [Sales](03_Dataset_Profiling/sales_2023_2025.md)
- [Returns](03_Dataset_Profiling/returns.md)

## Profiling Approach

The source datasets were examined using Google Sheets. Working copies were used for profiling and investigation while the original source files were preserved.

The profiling process focused on:

1. Dataset structure and field identification.
2. Record and field counts.
3. Missing-value checks.
4. Uniqueness checks on relevant fields.
5. Value distributions and repeated values.
6. Initial observations about field formats and representations.
7. Identification of potential relationships between datasets.

The results were documented without modifying the original source data.

## Scope and Limitations

This phase establishes an initial understanding of the source data. Its findings are exploratory and should not be interpreted as final data quality conclusions.

Potential identifiers and relationships require further validation before being implemented as database constraints or relationships.

Detailed data quality investigations and validation findings are documented separately in the project's data quality investigation documentation.

## Phase Outcome

The profiling exercise established a baseline understanding of the seven source datasets, comprising **103,455 records across 39 fields**.

The documented findings provide a foundation for subsequent data preparation, validation, and relational database development.
