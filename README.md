# Project Overview

<h3>IT-Operations Incident Analytics Dashboard</h3>
Developed a multi-page Power BI IT Operations Analytics Dashboard focused on incident management, SLA compliance, backlog monitoring, and operational performance tracking. The project includes interactive KPI reporting, incident trend analysis, MTTR tracking, ticket status monitoring, backlog aging analysis, and priority distribution visualizations using realistic enterprise-style ITSM data. Built with a focus on operational storytelling, dashboard design consistency, and business intelligence best practices.

<p align="center">
<h3>Incident Analysis</h3>
<img width="1241" height="684" alt="Trends and Backlog" src="https://github.com/user-attachments/assets/89c19727-3ce9-41b7-b49f-99f906b21f9f" />
</p>

<h3>Trends & Backlog</h3>
<img width="1241" height="684" alt="Incident Analysis" src="https://github.com/user-attachments/assets/4c93c890-b077-42ac-b225-0ec52281028b" />
</p>

# Project Breakdown

### Step 1 — Data Collection & Dataset Preparation

Collected and prepared datasets from multiple source files to simulate a realistic enterprise IT incident Ticket management environment. Mock operational data was generated using Tonic Fabric AI to replicate enterprise-style incident ticketing workflows and infrastructure relationships.

The project primarily utilized CSV and Excel source files; however, relational database design principles and table cardinality were considered throughout the data modeling process. The dataset structure could also be effectively migrated into a SQL-based relational DBMS environment.

#### Source Files
- `incidents.csv`
- `cmdb_servers.xlsx`
- `technicians.csv`
- `changes.csv`
- `calendar.csv`

### Step 2 — Data Cleaning & Transformation

Using Power BI’s Power Query Editor, I performed a series of data cleaning and transformation tasks on the CMDB server inventory and supporting datasets to improve data quality, consistency, and reporting accuracy.

Cleaning tasks included:
- Removing duplicate records
- Removing empty/null rows
- Standardizing inconsistent naming conventions using Find & Replace
- Trimming leading and trailing whitespace from records
- Validating column formatting and data consistency across related tables

Some records contained inconsistent environment and server naming conventions, which were standardized to ensure accurate filtering, grouping, and relationship mapping within the data model.

### Environment column before cleaning
<img width="515" height="729" alt="image" src="https://github.com/user-attachments/assets/dd67ef13-184c-4c1a-b568-1600cfae5f95" />

### Environment column after cleaning
<img width="515" height="729" alt="image" src="https://github.com/user-attachments/assets/9e84e2e8-8674-4e93-bef4-390057bba231" />

### Step 3 — Data Modeling & DAX Development

Designed and implemented a relational semantic data model in Power BI using a star schema architecture to support scalable reporting, KPI analysis, and cross-table filtering.

The model was structured around centralized fact tables containing operational business activity, while surrounding dimension tables provided descriptive and contextual data for reporting and analytics. One-to-many relationships and cardinality were configured to ensure accurate filtering behavior and optimized model performance.

Additional calculated measures and custom columns were created using DAX (Data Analysis Expressions) to support KPI tracking, SLA calculations, MTTR analysis, ticket aging metrics, and operational trend reporting.

#### Fact Tables
- `incidents.csv`
- `changes.csv`

#### Dimension Tables
- `cmdb_servers.xlsx`
- `technicians.csv`
- `calendar.csv`

#### Relationship Cardinality

| Relationship | Cardinality | Description |
|---|---|---|
| `calendar` → `incidents` | `1 : *` | One calendar date can relate to many incident records |
| `calendar` → `changes` | `1 : *` | One calendar date can relate to many change records |
| `CMDB Servers` → `incidents` | `1 : *` | One server can be associated with many incidents |
| `CMDB Servers` → `changes` | `1 : *` | One server can be associated with many change records |
| `technicians` → `incidents` | `1 : *` | One technician can be assigned to many incidents |






