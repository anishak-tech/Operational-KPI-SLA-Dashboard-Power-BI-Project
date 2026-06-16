# Operational KPI & SLA Dashboard | Power BI Project

## Project Overview

The Operational KPI & SLA Dashboard is an enterprise-style Power BI reporting solution developed to monitor operational efficiency, SLA compliance, transaction performance, and team productivity across multiple business processes.

This dashboard centralizes operational data from various departments including Deal Desk, DDPR Review, Transaction Accounting, and TA Review into an interactive analytics platform for business monitoring and decision-making.

The project emphasizes accurate SLA tracking using working-day calculations that exclude weekends, ensuring realistic operational performance measurement.

---

# Business Problem

The organization required a centralized dashboard to solve several operational reporting challenges:

* Manual and inconsistent SLA tracking
* Difficulty monitoring operational performance
* Lack of visibility into request processing
* Delayed business reporting
* No centralized KPI monitoring system
* Inaccurate turnaround calculations due to weekends being included

The objective was to create an automated, scalable, and interactive dashboard capable of delivering real-time operational insights.

---

# Project Objectives

The key objectives of the project were:

* Build an interactive Power BI dashboard
* Monitor operational KPIs
* Track SLA compliance accurately
* Exclude weekends from turnaround calculations
* Analyze transaction values and revenues
* Compare team performance
* Improve operational visibility
* Enable data-driven decision making

---

# Tools & Technologies Used

| Technology        | Purpose                        |
| ----------------- | ------------------------------ |
| Power BI Desktop  | Dashboard Development          |
| DAX               | KPI & SLA Calculations         |
| Power Query       | Data Cleaning & Transformation |
| Excel / CSV Files | Source Data                    |
| GitHub            | Project Hosting                |
| Data Modeling     | Relationship Management        |

---

# Dataset Description

The project uses multiple operational datasets.

## Main Tables

### Data Table

Contains operational request-level data:

* Created Date
* Completed Date
* Deal Status
* Request Type
* Transaction Value
* In House Gross
* Team
* Ops Region
* SLA-related information

---

### Opportunity Data Table

Contains opportunity and submission-level information:

* Submitted Date
* Deal OM Approval Date
* Opportunity Stage
* Revenue Metrics
* Transaction Details

---

### Date Table

Custom calendar table created for:

* Time intelligence
* Monthly reporting
* Yearly analysis
* Date filtering

---

### Team Dimension Table

Contains:

* Employee mapping
* Team classification

---

# Data Modeling

The project follows a star-schema model.

## Fact Tables

* Data
* Opportunity Data

## Dimension Tables

* Date Table
* Team Dimension

Relationships were established using:

* Date fields
* Team mapping columns

This model improves:

* Report performance
* Filter propagation
* Scalability

---

# Key Features Implemented

## 1. SLA Working Days Calculation

One of the most important business requirements was:

> SLA calculations should exclude weekends.

A custom DAX formula was developed to calculate working days only.

---

## SLA Days Overall Process Calculation

```DAX
SLA Days Overall Process =
VAR StartDate = 'Data'[Created Date]
VAR EndDate = 'Data'[Completed Date]

RETURN
IF(
    NOT(ISBLANK(StartDate)) &&
    NOT(ISBLANK(EndDate)) &&
    StartDate <= EndDate,

    COUNTROWS(
        FILTER(
            CALENDAR(StartDate, EndDate),
            WEEKDAY([Date],2) <= 5
        )
    ) - 1,

    BLANK()
)
```

---

## Purpose of the Calculation

This logic:

* Excludes Saturdays and Sundays
* Calculates only working days
* Improves SLA accuracy
* Aligns with real business operations

---

# KPI Measures Created

## Total Created ERR

Tracks total created operational requests.

```DAX
Total Created ERR =
COUNTROWS('Data')
```

---

## Total Submitted ERR

Tracks submitted opportunity requests.

```DAX
Total Submitted ERR =
COUNTROWS('Opportunity Data')
```

---

## On Hold Total

Tracks requests currently on hold.

```DAX
On Hold Total =
CALCULATE(
    COUNTROWS('Data'),
    'Data'[Deal Status] = "On Hold"
)
```

---

## Avg SLA Days

Calculates average working-day SLA duration.

```DAX
Avg SLA Days =
AVERAGE('Data'[SLA Days Overall Process])
```

---

## Total SLA Met

Tracks requests completed within SLA threshold.

```DAX
Total SLA Met =
COUNTROWS(
    FILTER(
        'Data',
        NOT(ISBLANK('Data'[Completed Date])) &&
        'Data'[SLA Days Overall Process] <= 5
    )
)
```

---

## SLA Not Met

Tracks requests exceeding SLA threshold.

```DAX
SLA Not Met =
COUNTROWS(
    FILTER(
        'Data',
        NOT(ISBLANK('Data'[Completed Date])) &&
        'Data'[SLA Days Overall Process] > 5
    )
)
```

---

# Dashboard Pages

## 1. Process Overview

Provides a high-level summary including:

* Total Requests
* SLA Metrics
* Status Tracking
* Revenue Insights
* Team Performance
* Transaction Analysis

---

## 2. Deal Desk Dashboard

Tracks:

* Deal processing performance
* Gross transaction values
* Team contributions
* Deal status distribution

---

## 3. DDPR Review Dashboard

Analyzes:

* DDPR workflow efficiency
* SLA adherence
* Request processing performance

---

## 4. Transaction Accounting Dashboard

Monitors:

* Transaction accounting metrics
* Revenue analysis
* Team productivity

---

## 5. TA Review Dashboard

Provides insights into:

* Review processing
* SLA performance
* Operational trends

---

# Visualizations Used

The dashboard includes multiple interactive visuals:

* KPI Cards
* Clustered Bar Charts
* Donut Charts
* Line Charts
* Status Distribution Charts
* Team Performance Charts
* Revenue Analysis Charts
* Trend Analysis Visuals
* Interactive Slicers

---

# Interactive Features

Dynamic slicers were implemented for:

* Type
* Request Type
* Ops Region
* Processed By
* Year
* Month

This allows users to perform flexible report exploration.

---

# Major Challenges Solved

## Challenge 1: Weekend Exclusion in SLA

Problem:
Traditional date difference calculations included weekends, resulting in inaccurate SLA reporting.

Solution:
Implemented a custom working-day calculation using:

* CALENDAR()
* FILTER()
* WEEKDAY()

functions in DAX.

---

## Challenge 2: Dynamic SLA Classification

Problem:
Need to classify SLA Met and SLA Not Met dynamically.

Solution:
Created DAX measures using SLA thresholds and working-day logic.

---

## Challenge 3: Multi-Source Data Integration

Problem:
Operational data existed across multiple datasets.

Solution:
Built a relational data model with proper table relationships and filtering structure.

---

# Business Impact

The dashboard delivers several operational benefits:

* Improved SLA visibility
* Faster reporting process
* Better operational monitoring
* Enhanced decision-making
* Reduced manual effort
* Increased reporting accuracy
* Better workload analysis

---

# Final Outcome

The project successfully delivered:

* Automated operational dashboard
* Accurate SLA tracking system
* Interactive business intelligence solution
* Enterprise-style KPI reporting
* Scalable analytical framework

The dashboard now provides management with real-time operational insights and performance monitoring capabilities.

---

# Future Enhancements

Potential future improvements include:

* Holiday calendar integration
* Power BI Service deployment
* Scheduled refresh automation
* Predictive SLA analytics
* Drill-through detail pages
* Role-based security implementation
* AI-powered insights

---


# Skills Demonstrated

This project demonstrates expertise in:

* Power BI Development
* DAX Calculations
* Data Modeling
* Data Visualization
* KPI Development
* SLA Analytics
* Business Intelligence
* Dashboard Design
* Power Query Transformation

---

# Author

Anisha K

Data Analyst | Power BI Developer

---

# Conclusion

The Operational KPI & SLA Dashboard demonstrates the implementation of an enterprise-level Power BI reporting solution focused on operational analytics and SLA performance monitoring.

By integrating multiple datasets, implementing advanced DAX calculations, and creating interactive visualizations, the project delivers actionable business insights while ensuring accurate working-day SLA calculations through weekend exclusion logic.
