# Project Foundation

## 1. Business Background

MetroMart Retail Group is a fictional South African general-retail business operating across Gauteng.

Over time, the business has accumulated operational data from multiple exports and systems. These sources contain information relating to customers, employees, products, stores, sales transactions and returns.

The fragmented nature of these sources, together with potential data-quality inconsistencies, has made it difficult for management to produce consistent and reliable business reports.

To address these challenges, MetroMart requires a structured approach to reviewing, validating and consolidating its operational data into a relational database that can support reliable operational and analytical reporting.

## 2. Problem Statement

MetroMart's operational data is distributed across multiple exports and systems, making it difficult to maintain consistency and produce reliable business reports.

The supplied source materials indicate potential challenges involving customer duplication, changes in store identifiers, inconsistent data exports, separately managed returns and unverified sales-total calculations.

Without a structured process for investigating and validating these records, data inconsistencies may affect the accuracy of reporting and the reliability of business decisions.

Furthermore, the absence of an approved database schema means that the business does not currently have an established relational structure for managing and connecting its operational information.

The project therefore needs to address both the quality of the available data and the lack of a structured database solution.

## 3. Project Purpose

The purpose of the MetroMart Retail Database Project is to investigate, validate and transform the supplied retail operational data into a structured relational database using PostgreSQL.

The project aims to establish a reliable and consistent data foundation by addressing identified data-quality issues, organising related business information into an appropriate relational structure and preserving traceability to the original source data wherever practical.

The resulting database will support repeatable SQL queries and reporting, enabling analysis of customers, products, stores, sales performance and returns.


## 4. Project Objectives

The project aims to achieve the following objectives:

1. **Investigate the source data:** Examine the supplied operational datasets and reference files to understand their structure, contents and relationships.

2. **Identify data-quality issues:** Profile and investigate the source data to identify missing values, duplicates, inconsistencies, invalid records and other potential quality concerns.

3. **Clean and validate data:** Apply appropriate cleaning and validation procedures while preserving the original source files and documenting important transformation decisions.

4. **Design a relational database:** Develop an appropriate relational database structure for managing customer, product, employee, store, sales and returns information.

5. **Implement the database:** Build and populate the designed database using PostgreSQL, applying appropriate keys, constraints and relationships to maintain data integrity.

6. **Support business analysis:** Develop repeatable SQL queries that support analysis of sales performance, products, customers, stores and returns.

7. **Maintain data traceability:** Preserve links between transformed records and their original sources wherever practical.

8. **Document the project:** Maintain technical documentation covering data investigations, cleaning decisions, database design, implementation and analytical findings.

## 5. Project Scope

### 5.1 In Scope

The project covers the following activities:

1. **Client and source-data review:** Review the supplied client documentation, operational datasets and supporting reference files.

2. **Data discovery and investigation:** Examine the structure, contents, quality and relationships of the available datasets.

3. **Data cleaning and validation:** Investigate identified data-quality issues, apply justified cleaning procedures and validate the resulting data.

4. **Relational database design:** Develop a relational database model covering the relevant retail business information, including customers, employees, products, stores, sales and returns.

5. **Database implementation:** Implement the approved database design using PostgreSQL, including appropriate tables, keys, relationships, constraints and indexes.

6. **SQL analysis and reporting:** Develop SQL queries to support the client's business questions and evaluate relevant retail performance indicators.

7. **Technical documentation:** Document project decisions, investigation findings, cleaning procedures, database design, implementation and analytical outputs.

### 5.2 Out of Scope

The project does not aim to:

- Replace or deploy a live point-of-sale system.
- Develop a complete retail management application or graphical user interface.
- Integrate directly with MetroMart's operational systems.
- Establish live, automated data feeds from external business systems.
- Implement a production cloud database environment.
- Modify the original client-provided source files.

### 5.3 Scope Boundaries

The project is based on the datasets and supporting documentation supplied in the client package.

The quality and completeness of the resulting database and analysis are therefore dependent on the available source information and the findings established during investigation.

Any additional requirements or capabilities beyond the defined project scope would require separate consideration.

## 6. Project Deliverables

The MetroMart Retail Database Project is expected to produce the following deliverables:

1. **Project Documentation:** Documentation establishing the business context, requirements, objectives, scope and project approach.

2. **Data Discovery and Investigation Reports:** Records of source-data profiling, data-quality findings, validation checks and investigation decisions.

3. **Cleaned and Validated Datasets:** Separate transformed datasets prepared for database implementation, with documented cleaning and validation procedures.

4. **Relational Database Design:** A documented database model defining the entities, attributes, relationships, primary keys and foreign keys.

5. **PostgreSQL Database:** An implemented relational database containing the prepared retail data, with appropriate integrity constraints and indexes.

6. **SQL Query Collection:** Reusable SQL queries supporting data validation, database operations and business analysis.

7. **Business Analysis Outputs:** Analytical findings addressing the client's business questions about sales, products, customers, stores and returns.

8. **Technical Documentation:** Documentation describing the database structure, implementation decisions, data transformations and analytical methods.

**Note:** The deliverables listed above represent the project's current expected outputs. They are provisional and may be revised as the project progresses to reflect the actual work completed and the final project outcomes.

## 7. Project Constraints and Assumptions

### 7.1 Project Constraints

The project is subject to the following constraints:

1. **Available source data:** The project is limited to the operational datasets and supporting reference files supplied in the original client package.

2. **Source-data quality:** The supplied datasets may contain missing, inconsistent, duplicated or invalid information that could affect cleaning, database design and analysis.

3. **Historical system differences:** Changes to the business's point-of-sale system and historical store identifiers may complicate the interpretation and integration of older records.

4. **Unverified business rules:** Certain business rules, including the calculation of recorded sales totals, require investigation before they can be reliably applied.

5. **No existing approved database schema:** The relational database structure must be designed as part of the project because the client has not supplied an approved schema.

### 7.2 Project Assumptions

The project currently operates under the following assumptions:

1. The supplied client package represents the source material available for the project.
2. The reference files are intended to support the interpretation and validation of selected operational datasets, subject to investigation.
3. The client's stated business requirements represent the expected capabilities of the proposed database solution.
4. Where source information is incomplete or ambiguous, decisions will be based on available evidence and documented rather than treated as confirmed business rules.
5. PostgreSQL will be used as the relational database management system for implementation.

These assumptions may be reviewed or revised as additional evidence becomes available during the project.

___
## 8. Project Methodology

The MetroMart Retail Database Project follows a structured, phased approach to data discovery, investigation, transformation, database development and analysis.

Each phase builds on the findings and outputs of the preceding phase. This approach helps ensure that database design and implementation decisions are supported by evidence gathered during the earlier stages of the project.

### 8.1 Project Phases

The project is organised into the following six phases:

1. **Project Discovery:** Establish the business context, review client requirements, understand the available source materials and define the project's objectives, scope and proposed approach.

2. **Data Discovery and Profiling:** Examine the supplied datasets to understand their structures, contents, distributions and initial quality characteristics.

3. **Data Quality Investigation:** Conduct detailed investigations into identified data-quality concerns, validate relationships and document findings and decisions.

4. **Data Cleaning and Transformation:** Apply justified cleaning procedures, resolve or isolate identified issues where appropriate and prepare validated datasets for database implementation.

5. **Database Design and Implementation:** Develop the relational database model and implement the database in PostgreSQL using the prepared datasets.

6. **Data Analysis and Reporting:** Use SQL to analyse the available retail information and produce findings that address the client's business questions.

### 8.2 Working Principles

The project follows these principles throughout its execution:

- Preserve original client-provided source files.
- Base decisions on investigation and available evidence.
- Document assumptions, findings and important decisions.
- Separate raw source data from working and transformed datasets.
- Validate data before using it for database implementation and analysis.
- Maintain traceability wherever practical.

### 8.3 Phase Dependencies


The phases are designed to build upon one another. Findings from data discovery and quality investigation inform cleaning decisions, while validated data informs database design and implementation.

Analytical reporting is performed using the implemented database and its validated information.

