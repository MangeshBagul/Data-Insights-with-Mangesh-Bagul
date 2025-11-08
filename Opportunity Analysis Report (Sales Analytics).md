**Category: Sales Analytics**

**Executive Summary:**
A comprehensive Power BI dashboard designed to provide sales leadership with real-time visibility into pipeline opportunities, enabling data-driven decision-making across regions, sales channels, and deal stages.

**Business Problem:**
Sales leadership needed real-time, accurate visibility of the sales pipeline value—across multiple regions, channels, and stages. Existing reporting was manual, error-prone, and prevented data-driven opportunity prioritization.

**Technical & Business Analysis:**

  Data modeling: Created a star schema in Power BI using Fact_Opportunities and dimension tables for regions, stages, reps, and channels.

  DAX measures: Developed formulas for win rate, pipeline value by stage, deal size, and cycle duration. Leveraged Time Intelligence for period-over-period analysis.

  Visualizations: Multi-page report with executive summary, funnel breakdown, win/loss by territory, and channel performance.

  Interactivity: Enabled filtering/drill-down to individual rep/channel/territory.

  <img width="1442" height="807" alt="project1 1" src="https://github.com/user-attachments/assets/e268b20c-535e-4ecb-9bc8-7c1ebb95c876" />
  
**Business Impact & Outcomes**

**Quantifiable Results:**

**Forecast Accuracy:** Improved from 65% to 89% within 3 months

Reason: Real-time pipeline visibility enabled better predictions

**Sales Cycle Time:** Reduced average deal cycle from 120 to 95 days

Reason: Visibility into bottlenecks (e.g., Stage 3 averaging 45 days) allowed targeted intervention

**Win Rate Improvement:** Increased from 18% to 24% YoY

Reason: Identified and replicated best practices from high-performing reps/channels

**Pipeline Visibility:** 100% real-time accuracy (vs. manual spreadsheets with 2-3 day lag)

Reason: Direct connection to CRM data, automated refresh

**Management Efficiency:** Reduced monthly reporting time from 8 hours to 2 hours

Reason: Automated dashboard vs. manual consolidation

**Qualitative Benefits:**

Sales leadership gained confidence in forecasting

Teams aligned on pipeline health weekly

Easier to allocate resources to underperforming channels

Enabled data-driven compensation and incentive discussions

**Tools, Technologies & Skills Demonstrated**

**Power BI Features Used:**

Star schema data modeling (Tabular Model)

DAX (Data Analysis Expressions) for 13+ complex calculations

Power Query for ETL and data transformation

Row-Level Security (RLS) to limit rep view to their own deals

Bookmarks for dashboard interactivity

Drill-through for deep analysis

**SQL/Database Skills:**

Query writing to extract opportunity data from CRM (Salesforce/Dynamics)

Data validation and reconciliation

**Data Quality Practices:**

Identified and handled NULL values in stage/amount fields

Validated deal dates for logical consistency

Standardized stage names across data sources

**Power BI Advanced Features:**

Dynamic titles using DAX

Conditional formatting on KPI cards

Tooltips with additional metrics

Custom sort orders for categorical axes

Performance optimization (removed unused columns, optimized DAX)

**Learning Outcomes & Skills Growth**

Data Modeling Expertise: Deepened understanding of dimensional modeling and fact/dimension relationships

DAX Proficiency: Mastered complex calculations including time intelligence and cross-filter logic

Business Acumen: Learned sales metrics, pipeline terminology, and business drivers

Communication: Learned to present data insights in executive-friendly language

Problem-Solving: Debugged performance issues and optimized dashboard load times

**Downloadable Assets**

PBIX File: [Link]([url](https://drive.google.com/file/d/1UF0kX0b0HtsmtEJ_ybQzA6JvvuUWws9o/view?usp=sharing)))

PDF Report: [Link]([url](https://drive.google.com/file/d/1R1B97ILv5q-gynRMuAxWKKi5Sikicf35/view?usp=sharing))

Data Dictionary: N/A
