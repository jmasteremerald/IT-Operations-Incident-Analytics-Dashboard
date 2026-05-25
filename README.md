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

Collected and prepared datasets from multiple source files to simulate a realistic enterprise IT incident management environment. Mock operational data was generated using :contentReference[oaicite:0]{index=0} to replicate enterprise-style incident ticketing workflows and infrastructure relationships.

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

<p align="center">
<img width="541" height="729" alt="image" src="https://github.com/user-attachments/assets/7fd538b9-d20a-42f8-aa34-8d710e7d807d" />
<img width="379" height="326" alt="Screenshot 2026-05-25 at 10 51 55 AM" src="https://github.com/user-attachments/assets/71d1bb14-6c00-4cf1-8abf-81c7a4ced5da" />
</p>



