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
