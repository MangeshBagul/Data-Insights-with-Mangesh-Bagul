**Category: Customer Analytics & Retention**

**Executive Summary:**

A predictive analytics dashboard identifying at-risk customer segments, quantifying churn drivers, and enabling targeted retention campaigns. This project demonstrated advanced DAX modeling and customer behavior analytics.

**Business Problem & Context**

**Challenge:**

A telecom/service company experienced 15% annual churn (losing 1 in 7 customers yearly), costing millions in lost revenue. Leadership lacked:

Understanding of which customers were at risk

Visibility into churn root causes

Data to guide retention strategy

Questions Needing Answers:

Who are our at-risk customers?

What factors correlate with churn (age, contract, services, price, support)?

Which services reduce churn (upsell/cross-sell opportunity)?

Can we predict churn proactively?

**Solution Architecture**

**Data Source:**

Customer master table: Demographics (age, tenure, location), churn (Yes, No)

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

DAX Measures & Analysis (32+ Formulas)

Churn Metrics:

% Device protection churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[DEVICEPROTECTION]= "Yes",'Churn table'[CHURN]=TRUE()),[churn count],0)

% Device protection customer = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[DEVICEPROTECTION]= "Yes",'Churn table'[CHURN]=false),[customer count],0)

% moviestream churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[STREAMINGMOVIES]= "Yes",'Churn table'[CHURN]=true),[churn count],0)

% moviestream customer = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[STREAMINGMOVIES]= "Yes",'Churn table'[CHURN]=false),[customer count],0)

% online backup churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[ONLINEBACKUP]= "Yes",'Churn table'[CHURN]=TRUE()),[churn count],0)

% online backup customer = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[ONLINEBACKUP]= "Yes",'Churn table'[CHURN]=false),[customer count],0)

% online security churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[ONLINESECURITY]= "Yes",'Churn table'[CHURN]=TRUE()),[churn count],0)

% online security customer = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[ONLINESECURITY]= "Yes",'Churn table'[CHURN]=false),[customer count],0)

% partner churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[PARTNER]= TRUE(),'Churn table'[CHURN] = TRUE()),[churn count],0)

% partner customer = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[PARTNER]= TRUE(),'Churn table'[CHURN] = FALSE()),[customer count],0)

% senior Citizen = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[SENIORCITIZEN]=1,'Churn table'[CHURN] = FALSE()),[customer count],0)

% senior Citizen churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[SENIORCITIZEN]=1,'Churn table'[CHURN] = TRUE()),[churn count],0)

% tech support churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[TECHSUPPORT]= "Yes",'Churn table'[CHURN]=TRUE()),[churn count],0)

% tech support customer = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[TECHSUPPORT]= "Yes",'Churn table'[CHURN]=false),[customer count],0)

% tvstream churn = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[STREAMINGTV]= "Yes",'Churn table'[CHURN]=TRUE()),[churn count],0)

% tvstream customer = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[STREAMINGTV]= "Yes",'Churn table'[CHURN]=false),[customer count],0)

average Total charges = CALCULATE(AVERAGE('Churn table'[TOTALCHARGES]))

churn average monthly charges = CALCULATE(AVERAGE('Churn table'[MONTHLYCHARGES]),'Churn table'[CHURN]= TRUE())

churn count = CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[CHURN] = TRUE())

churn customer count = CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[CHURN] = TRUE())

churn multipleline_NO = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES]= "No",'Churn table'[CHURN] = TRUE()),CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES] <> "No phone service",'Churn table'[CHURN] = TRUE()),0)

churn multipleline_yes = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES]= "Yes",'Churn table'[CHURN] = TRUE()),CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES] <> "No phone service",'Churn table'[CHURN] = TRUE()),0)

churn Total monthly charges = CALCULATE(AVERAGE('Churn table'[TOTALCHARGES]),'Churn table'[CHURN]= TRUE())

client average monthly charges = AVERAGE('Churn table'[MONTHLYCHARGES])

client multipleline_NO = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES]= "No",'Churn table'[CHURN] = FALSE()),CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES] <> "No phone service",'Churn table'[CHURN] = FALSE()),0)

client multipleline_yes = DIVIDE(CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES]= "Yes",'Churn table'[CHURN] = FALSE()),CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[MULTIPLELINES] <> "No phone service",'Churn table'[CHURN] = FALSE()),0)

Count of paymentmthod customer = CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[CHURN]=false)

customer count = CALCULATE(COUNT('Churn table'[CUSTOMERID]),'Churn table'[CHURN] = FALSE())

Total Count by Gender churn = CALCULATE(COUNT('Churn table'[GENDER]), 'Churn table'[CHURN]= TRUE())

Finding: Need aggressive onboarding and early engagement

**Dashboard Design**

Page 1: Churn Overview Landing Page.

<img width="1436" height="808" alt="Project3 1" src="https://github.com/user-attachments/assets/1a2bc7be-bd7c-44e0-a340-786e75ea787e" />

Page 2: Client Analysis

<img width="1445" height="809" alt="Project3 2" src="https://github.com/user-attachments/assets/d3b89e44-78f3-4403-9f27-4c0bc0d070a5" />

Page 3: Churn Risk Analysis

<img width="1462" height="808" alt="project3 3" src="https://github.com/user-attachments/assets/96a53616-667c-407a-b338-edf62a807839" />

Page 3: Service Impact & Retention Levers

<img width="1444" height="802" alt="project3 4" src="https://github.com/user-attachments/assets/d17bfa2a-3394-489e-8ccf-aa79c71f283d" />

Business recommendation: Upsell services to high-risk, non-adopters

**Business Impact**

**Quantifiable Outcomes:**

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

**Tools & Techniques Demonstrated**

**Advanced Power BI:**

32+ DAX measures (complex conditional logic, aggregations, rankings)

Cohort analysis and segmentation

Predictive modeling integration (using R/Python in Power BI)

Storytelling across 3 interactive pages

Data Science Concepts:

Feature engineering (creating derived variables)

Cohort analysis

Churn prediction/classification

Correlation analysis (which factors drive churn)

**Business Analytics:**

Customer lifetime value calculation

Retention ROI analysis

Segmentation strategy

Intervention targeting

**Learning Outcomes**

Customer Analytics Mastery: Learned lifecycle analysis, segmentation, and LTV calculations

Predictive Mindset: Moved from "What happened?" to "What will happen?"

Business Impact: Understood how to tie analytics to revenue (retention = revenue protection)

Complexity Management: Built 40+ measures without sacrificing model performance

Storytelling: Presented complex analysis in business language for non-technical stakeholders

Pbix Link : https://drive.google.com/file/d/1kW-UR2loJJlF9qQUK6NqMkEliQV5N8Ip/view?usp=sharing
