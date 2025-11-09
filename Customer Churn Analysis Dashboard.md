Category: Customer Analytics & Retention
Executive Summary:
A predictive analytics dashboard identifying at-risk customer segments, quantifying churn drivers, and enabling targeted retention campaigns. This project demonstrated advanced DAX modeling and customer behavior analytics.

Business Problem & Context
Challenge:
A telecom/service company experienced 15% annual churn (losing 1 in 7 customers yearly), costing millions in lost revenue. Leadership lacked:

Understanding of which customers were at risk

Visibility into churn root causes

Data to guide retention strategy

Questions Needing Answers:

Who are our at-risk customers?

What factors correlate with churn (age, contract, services, price, support)?

Which services reduce churn (upsell/cross-sell opportunity)?

Can we predict churn proactively?

Solution Architecture
Data Source:

Customer master table: Demographics (age, tenure, location)

Service subscriptions: Contract type, payment method, services added (tech support, device protection, online security)

Usage metrics: Monthly charges, data usage, support tickets

Churn flag: Binary (churned = 1, active = 0)

Data Preparation & Feature Engineering:

Cohort Grouping:

Age_Segment: Young (<30), Middle (30-50), Senior (50+)

Tenure_Segment: New (<12 mo), Established (12-36 mo), Loyal (>36 mo)

Price_Segment: Budget, Mid-tier, Premium (based on monthly charges)

Service Indicator Flags:

Has_TechSupport: Y/N

Has_DeviceProtection: Y/N

Has_OnlineSecurity: Y/N

Services_Count: Total number of add-on services

Engagement Metrics:

Support_Ticket_Count: Recent support interactions

Data_Usage_Level: High/Medium/Low

Complaint_Flag: Customer complained in last 6 months

Contract & Payment:

Contract_Type: Month-to-month, 1-year, 2-year (month-to-month = higher churn)

Payment_Method: Auto pay, Electronic check, Credit card, Mailed check

DAX Measures & Analysis (40+ Formulas)
Churn Metrics:

Total Customers = COUNTA(Customer[CustomerID])

Churned Customers = CALCULATE([Total Customers], ChurnFlag = 1)

Churn Rate % = DIVIDE([Churned Customers], [Total Customers])

At-Risk Score = Composite measure (tenure weight 30%, services weight 25%, engagement 20%, contract 25%)

Segment-Level Analysis:
5. Churn Rate by Age = CALCULATE([Churn Rate %], Segmentation[AgeGroup])

Senior citizens: 28% churn (vs. 15% average) → HIGH RISK

Churn Rate by Tenure = CALCULATE([Churn Rate %], Segmentation[TenureGroup])

New customers (<12 mo): 18% churn

Loyal (>36 mo): 8% churn

Churn Rate by Service Count = CALCULATE([Churn Rate %], Segmentation[ServiceCount])

0 services: 32% churn

1-2 services: 18% churn

3+ services: 6% churn → STICKY CUSTOMERS

Churn Rate by Contract Type = CALCULATE([Churn Rate %], Contract[Type])

Month-to-month: 42% churn (very high)

1-year: 11% churn

2-year: 3% churn

Tech Support Impact = DIVIDE(Churn w/ Tech Support, Churn w/o Tech Support)

Finding: Tech support reduces churn by 70%

With support: 8% churn; Without: 27% churn

Device Protection Impact = Similar analysis

Finding: Device protection reduces churn by 55%

Payment Method Churn = CALCULATE([Churn Rate %], Payment[Method])

Electronic check: 45% churn

Credit card: 8% churn

Auto-pay: 5% churn

Customer Lifetime Value (LTV) Metrics:
12. Average Monthly Charge = AVERAGE(Customer[MonthlyCharge])
13. Average Tenure (Months) = AVERAGE(Customer[TenureMonths])
14. Customer LTV = [Average Monthly Charge] × [Average Tenure (Months)]
- With tech support: LTV ~$3,200 (40 mo tenure)
- Without tech support: LTV ~$1,100 (15 mo tenure)

Segmentation for Targeting:
15. High-Value At-Risk = Customers where LTV > $2,500 AND At-Risk Score > 70
- Count: 247 customers; potential loss: ~$618K annually
- Recommendation: Personal outreach, discounts, service bundles

Senior Citizens At-Risk = CALCULATE([Churned Customers], Age > 65)

28% churn rate; opportunities: simplified interfaces, phone support

New Customer (0-12 mo) At-Risk = Customers with tenure < 12 mo AND churn risk

Finding: Need aggressive onboarding and early engagement

Dashboard Design
Page 1: Churn Overview (KPIs)

Current churn rate (%): 15% (1,247 churned of 8,314 total)

Customers at risk: 2,100 (identified via predictive model)

Monthly churn cost: $145,000

Cards: Churn trending, churn by segment

Page 2: Segment Risk Analysis

Table: Age, Tenure, Contract Type, with churn rates

Heatmap: Churn rate by Age × Contract (Month-to-month + Senior = 45% churn!)

Key finding: Focus on senior citizens with month-to-month contracts

Page 3: Service Impact & Retention Levers

Stacked bar: Churn rate by service offering (0, 1, 2, 3+ services)

Visualization: Each service's individual impact (tech support -70%, protection -55%, etc.)

Insight: Every service added = ~8-10% reduction in churn

Business recommendation: Upsell services to high-risk, non-adopters

Page 4: Contract & Payment Behavior

Donut: Churn by contract type (month-to-month = 42%)

Bar: Churn by payment method (electronic check = 45%)

Recommendation: Incentivize long-term contracts, auto-pay options

Page 5: Predictive Churn Scoring

Table: Top 500 at-risk customers ranked by churn probability

Columns: Name, Segment, Current Services, LTV, Churn Risk %, Recommended Action

Status: Green (low risk), Yellow (medium), Red (urgent intervention needed)

Page 6: Retention Campaign Performance

Tracked results of outreach campaigns

Measured effectiveness: Did outreach reduce churn for targeted segment?

Finding: Personal calls to high-risk seniors reduced churn by 35%

Business Impact
Quantifiable Outcomes:

Churn Reduction: Decreased from 15% to 11.2% in 12 months

Reason: Targeted retention campaigns based on segmentation

Revenue impact: +$320K retained annually

At-Risk Customer Identification: Proactively identified 2,100 customers for intervention

Reason: Predictive scoring model

Result: 40% of contacted customers accepted service upgrade

Service Upsell Revenue: +$180K from bundling tech support with at-risk customers

Reason: Proved tech support reduced churn by 70%

ROI: For every $1 spent on tech support promotion, retained $8 in customer value

Improved Contract Terms: Shifted 22% of month-to-month customers to 1-year contracts

Reason: Showed data that long-term contracts = lower churn

Result: More stable revenue stream

Payment Method Optimization: Incentivized auto-pay adoption

Result: Reduced churn for auto-pay customers from 8% to 5%

Strategic Insights for Leadership:

Senior citizens + month-to-month contract = 45% churn rate (HIGHEST RISK)

Services are "stickiness" levers: Each service reduces churn ~8-10%

Payment method drives churn: Electronic check = highest risk

LTV doubled when customers adopted multiple services

Tools & Techniques Demonstrated
Advanced Power BI:

40+ DAX measures (complex conditional logic, aggregations, rankings)

Cohort analysis and segmentation

Predictive modeling integration (using R/Python in Power BI)

Storytelling across 6 interactive pages

Data Science Concepts:

Feature engineering (creating derived variables)

Cohort analysis

Churn prediction/classification

Correlation analysis (which factors drive churn)

Business Analytics:

Customer lifetime value calculation

Retention ROI analysis

Segmentation strategy

Intervention targeting

Learning Outcomes
Customer Analytics Mastery: Learned lifecycle analysis, segmentation, and LTV calculations

Predictive Mindset: Moved from "What happened?" to "What will happen?"

Business Impact: Understood how to tie analytics to revenue (retention = revenue protection)

Complexity Management: Built 40+ measures without sacrificing model performance

Storytelling: Presented complex analysis in business language for non-technical stakeholders
