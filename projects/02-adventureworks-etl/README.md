# AdventureWorks | Data Engineering & ETL

**Individual academic project · Power Query (M) · Data quality · Relational modelling**

## Project overview
Developed an ETL workflow for the AdventureWorks Cycles dataset to prepare raw **sales, returns, customer, product and territory** data for business intelligence. The objective was to identify and resolve data-quality issues, standardise information from different sources and create a consistent analytical foundation for downstream reporting.

This was an **individual project**.

## Problem and technical approach

### 1. Data ingestion and consolidation
- Designed a **folder-based ingestion workflow** to consolidate multiple CSV files.
- Organised the source data into a reusable transformation process rather than treating each file as an isolated input.

### 2. Data quality and standardisation
- Investigated inconsistencies across sales, customers, products and geographic records.
- Applied cleaning and standardisation steps to improve consistency between tables.
- Handled missing values using conditional transformations.

### 3. Custom Power Query M transformations
- Developed **Power Query M logic** to reconstruct product information from inconsistently structured text.
- Extracted and standardised product attributes that were not reliably represented in the raw data.
- Used conditional logic to deal with incomplete or irregular source values.

### 4. Integration and analytical modelling
- Combined product, category and subcategory information using **table joins**.
- Prepared and structured **fact and dimension tables** to support relationships and downstream analysis.
- Built a more coherent analytical data foundation for business intelligence.

## Technical challenges
The main challenge was not simply importing data, but turning heterogeneous and imperfect source files into structured, reusable analytical tables. In particular, recovering product attributes from inconsistent text required custom transformation logic rather than only standard menu-driven cleaning steps.

## Outcome
Produced cleaned, structured and reusable datasets suitable for subsequent analysis and reporting. The project demonstrates practical experience in **ETL design, data validation, Power Query M, relational structuring and problem-solving**.

## Tools and skills
**Power BI · Power Query · M language · CSV ingestion · ETL · Data cleaning · Conditional transformations · Table joins · Fact and dimension modelling**

## Access to the full project
> **Full project available upon request.** The completed Power BI file is stored privately and may be made available for professional or recruitment review.

Only the technical overview is published here; the full worked file is not part of this public repository.
