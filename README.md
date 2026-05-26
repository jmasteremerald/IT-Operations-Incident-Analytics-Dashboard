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
- Standardizing inconsistent naming conventions using Find & Replace to ensure accurate filtering, grouping, and relationship mapping within the data model.
- Trimming leading and trailing whitespace from records
- Validating column formatting and data consistency across related tables

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

#### Semantic Model

<img width="1370" height="654" alt="image" src="https://github.com/user-attachments/assets/d6435d8a-5e80-45d7-9fa3-dba9444faa6a" />


#### DAX Measures & Calculated Columns

| Measure / Column | Purpose |
|---|---|
| `SLA Compliance %` | Calculates the percentage of incidents resolved within SLA requirements to monitor service performance and operational compliance. |
| `Avg Ticket Age` | Measures the average age of tickets to help identify backlog growth and long-running unresolved incidents. |
| `Avg MTTR` | Calculates the average Mean Time to Resolution (MTTR) to evaluate incident resolution efficiency and support team performance. |
| `Ticket Age Days` | Calculates the number of days a ticket has remained open by comparing the open date against the close date (or current date if still open). Used for backlog aging analysis and ticket lifecycle reporting. |

```DAX
SLA Compliance % =
DIVIDE(
    CALCULATE(
        COUNT(Incidents[IncidentID]),
        Incidents[SLA_Breached] = FALSE()
    ),
    COUNT(Incidents[IncidentID])
)
```

```DAX
Avg Ticket Age =
AVERAGE(incidents[Ticket Age Days])
```
```DAX
Avg MTTR =
AVERAGE(Incidents[ResolutionTimeHours])
```
```DAX
Ticket Age Days =
DATEDIFF(
    incidents[OpenDateTime],
    COALESCE(incidents[ClosedDateTime], NOW()),
    DAY
)
```




# Data Visualization and Analysis  

## Dashboard 1 — Incident Analysis

| Visualization | Dashboard Preview |
|---|---|
| **Number of Incidents by Assignment Group**  <br><br> **Chart Type:** Horizontal Bar Chart  <br><br> **Purpose:** Used to compare workload distribution across IT support teams and identify which departments handle the highest incident volume. Horizontal bars improve readability for long assignment group names.  <br><br> **Insights:** Windows Server Team handled the highest number of incidents, while Unix Administration handled the fewest. The chart highlights operational workload distribution across support teams. | <img width="700" alt="Incidents by Assignment Group" src="https://github.com/user-attachments/assets/c5946c62-3df1-46af-914b-2b923094340d"/> |
| **SLA Compliance % by Yearly Quarter**  <br><br> **Chart Type:** Combo Chart (Bar + Line)  <br><br> **Metrics:** Incident Count, SLA Compliance %  <br><br> **Purpose:** Combines operational volume and SLA performance into a single visualization to evaluate whether ticket volume impacts SLA success rates.  <br><br> **Insights:** SLA compliance fluctuated across quarters, with Q1 2026 showing a noticeable drop despite consistent operational volume. | <img width="700" height="380" src="https://github.com/user-attachments/assets/7850d805-7c23-4911-ad2a-673a518e1e12"/> |
| **Incident Distribution by Environment**  <br><br> **Chart Type:** Clustered Column Chart  <br><br> **Purpose:** Used to compare incident volume across environments and identify where the majority of operational issues occur.  <br><br> **Insights:** Production generated the majority of incidents, while Development and QA environments produced significantly fewer tickets. | <img width="700" src="https://github.com/user-attachments/assets/85214d3b-7fd4-4f52-82ee-0e8a88607fb2"/> |
| **SLA Breach Distribution**  <br><br> **Chart Type:** Doughnut Chart  <br><br> **Metrics:** SLA_Breached (True/False)  <br><br> **Purpose:** Provides a high-level KPI view of SLA compliance versus breach rates.  <br><br> **Insights:** Most incidents met SLA requirements, though breaches still represented operational risk and service impact. | <img width="700" src="https://github.com/user-attachments/assets/cc82c775-e9c2-4f15-b1a3-bf9202738021"/> |
| **Average Resolution Time by Team**  <br><br> **Chart Type:** Horizontal Bar Chart  <br><br> **Metric:** Average MTTR  <br><br> **Purpose:** Compares operational efficiency between support teams and identifies resolution bottlenecks.  <br><br> **Insights:** Unix Administration showed the longest average resolution time, while the Backup & Recovery Team resolved incidents the fastest. | <img width="700" src="https://github.com/user-attachments/assets/0522bd3c-bc88-4aa0-b2cf-9b49d516e2c7"/> |

---

## Dashboard 2 — Trends & Monitoring

| Visualization | Dashboard Preview |
|---|---|
| **Incident Volume Trend**  <br><br> **Chart Type:** Line Chart  <br><br> **Metric:** Monthly Incident Count  <br><br> **Purpose:** Used for time-series trend analysis to identify increases, decreases, and seasonal operational spikes in incident activity.  <br><br> **Insights:** Incident activity peaked during mid-2024 and fluctuated across months, supporting operational forecasting and workload planning. | <img width="700" src="https://github.com/user-attachments/assets/24ccc62d-d6a8-4bf4-b2b1-2aadacb5b234"/> |
| **Ticket Status by Month**  <br><br> **Chart Type:** Stacked Column Chart  <br><br> **Metrics:** Open, In Progress, and Closed Tickets  <br><br> **Purpose:** Displays ticket lifecycle distribution over time and monitors backlog trends across operational workflows.  <br><br> **Insights:** Most tickets were successfully closed monthly, while open ticket counts remained relatively low. | <img width="700" src="https://github.com/user-attachments/assets/282682ad-d4b0-4bb3-97e2-feae0ee52cad"/> |
| **Incident Priority Distribution**  <br><br> **Chart Type:** Doughnut Chart  <br><br> **Metrics:** P1, P2, P3, and P4 Priority Counts  <br><br> **Purpose:** Highlights the proportional distribution of incident severity levels and operational risk exposure.  <br><br> **Insights:** P3 and P4 incidents represented the majority of tickets, while critical P1 incidents remained relatively rare. | <img width="420" alt="Incident Priority Distribution" src="https://github.com/user-attachments/assets/e3e9a387-f41d-4e58-ae55-f3178283b2ad"/> |
| **Incident Reopen Trend**  <br><br> **Chart Type:** Clustered Column Chart  <br><br> **Metrics:** Reopened (True/False)  <br><br> **Purpose:** Tracks service quality and ticket resolution effectiveness by monitoring reopen activity over time.  <br><br> **Insights:** Reopened incidents remained relatively low overall, though certain months experienced temporary spikes in reopen activity. | <img width="700" src="https://github.com/user-attachments/assets/e7d529de-b5cb-4cba-934b-6e173c4922e4"/> |






