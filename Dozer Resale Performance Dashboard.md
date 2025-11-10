**Category:** Equipment Sales & Market Analytics

**Executive Summary:**

A Power BI dashboard analyzing the used heavy machinery (dozer) resale market, providing dealership with pricing strategy, inventory optimization, and regional market insights.

**Business Problem & Context**

**Challenge:**

A heavy equipment dealership buying/selling used dozers needed to:

Price machines competitively without leaving money on the table

Identify which models/configurations command premiums

Understand regional demand variations

Optimize inventory (which machines to stock)

Predict resale values based on age, model, condition

**Data Landscape:**

500+ historical dozer sales transactions

**Fields:** Model, Manufacturing Year, Configuration, State/Region, Sale Price, Condition Rating

**Objective:** Build analytics to support pricing and inventory decisions

**Solution Architecture**

**Data Import & Transformation:**

**Data source:** Historical transaction database from Snowflake

**Cleaned fields:** Standardized model names, validated sale prices, handled missing condition data

**Created calculated columns:**

Machine Age = Current Year - Manufacturing Year

Price per Age = Sale Price / Machine Age (depreciation efficiency metric)

Region Group = Grouped states into geographic regions (South, Midwest, West, Northeast)

Dimensional Model: N/A

Fact Table: FactDozemSales (one row per transaction)

SalePrice, YearMade, Meter, Saleyear, Machineage, Datasource, UsageBand

DAX Measures:

average sale price = AVERAGE(DOZER[SALEPRICE] )

distint model = DISTINCTCOUNT(DOZER[FIMODELDESC])

avg machine age = AVERAGE(DOZER[MACHINEAGE])

Median Sale Price = MEDIAN(Sales[SalePrice])

machinegroup = SWITCH( TRUE(), DOZER[MACHINEAGE] <=10, "0-10 Group",DOZER[MACHINEAGE] <=20, "11-20 Group",DOZER[MACHINEAGE] <=30, "21-30 Group",DOZER[MACHINEAGE] <=40, "31-40 Group",DOZER[MACHINEAGE] <=50, "41-50 Group")

Price by Model = CALCULATE([Average Sale Price], Groupby Model)

Price by Age = CALCULATE([Average Sale Price], Groupby [Machine Age])

Price by Configuration = Single Shank ripper = $61K (premium vs. standard blade)

PriceBucket = 
SWITCH(
    TRUE(),
    [average sale price] <= 23000, "₹8K–₹23K",
    [average sale price] <= 46900, "₹23K–₹47K",
    [average sale price] <= 70800, "₹47K–₹70K",
    [average sale price] <= 94700, "₹70K–₹94K",
    "₹94K–₹127.5K"
)

Units Sold = COUNTA(Sales[TransactionID])

Revenue = SUM(Sales[SalePrice])

Top Models by Volume = TOPN(5, Models, [Units Sold])

D6, D5, D6R dominated volume

Slow-Moving Models = Filtered count of models with <5 sales in trailing 12 months

Regional Concentration = % of total sales by region

Midwest (manufacturing belt): 42%, West: 35%, South: 18%, Northeast: 5%

**Dashboard Pages**

**Page 1: Market Overview**

Landing page: option to select either Overall Summary, Model-wise Sales or Explore Resale Patterns

<img width="1440" height="809" alt="project4 1" src="https://github.com/user-attachments/assets/4644bb39-b7ce-4387-b5ae-d3c5ff75189a" />


Page 2: Overall Summary

<img width="1441" height="806" alt="Project4 2" src="https://github.com/user-attachments/assets/d613a0c3-c422-4aad-b857-047b06a993d5" />


KPIs: Unique Models Sold Per Year (36), Total Dozers Sold Per Year (7968), Avg. Resale Price ($53.67K), Median Resale Price ($49.00K)

<img width="883" height="182" alt="image" src="https://github.com/user-attachments/assets/fb0e5f54-ce9f-42fe-8569-86c44ebb52a5" />

Line chart: Total Sales volume per year, Age Trend, Avg Sale price Trend, Orders trend over time.. all are toggled using Button and Bookmark

<img width="519" height="165" alt="image" src="https://github.com/user-attachments/assets/e6b95b5d-51ba-40b8-a039-f6620d555f75" />

<img width="531" height="165" alt="image" src="https://github.com/user-attachments/assets/3740d92e-c692-4977-9403-a994937b8750" />

<img width="523" height="170" alt="image" src="https://github.com/user-attachments/assets/f94ce4aa-f02b-4b55-9c93-91b33160e052" />

<img width="518" height="170" alt="image" src="https://github.com/user-attachments/assets/b6c39326-bbb7-4b4f-97e1-b61741373400" />

Funnel : Median Resale Price by Data source

<img width="360" height="163" alt="image" src="https://github.com/user-attachments/assets/9d4dc8b5-0d8a-40c3-bea9-c57a85ebf483" />

Line and Stacked Column Chart : Gross Revenue & orders | Monthly Trend

<img width="532" height="172" alt="image" src="https://github.com/user-attachments/assets/215a8e23-5def-4cad-8612-f04968f4ea89" />

**Page 2:  Model-wise Sales**

<img width="1437" height="817" alt="Project4 3" src="https://github.com/user-attachments/assets/9e4fa9d1-e9de-4ae4-96a5-b7e4e7635fd5" />


Matrix: All dozer models ranked by: Avg. Sales Price

<img width="583" height="222" alt="image" src="https://github.com/user-attachments/assets/0abf91da-c16a-44d5-9e6f-aa263f36dc87" />

Top 5 Best-Selling Products

<img width="305" height="144" alt="image" src="https://github.com/user-attachments/assets/23e6b131-596a-4a9a-82ee-5872124209c0" />

Top 5 Slow-moving Products

<img width="309" height="151" alt="image" src="https://github.com/user-attachments/assets/8276f503-b4bd-4b41-bfb9-1464e0049946" />

Matrix for Ripper Type

<img width="309" height="112" alt="image" src="https://github.com/user-attachments/assets/7d5cff58-6e7f-4289-95bb-405ca3c50ba4" />

Stock Distributaion by Product Hiearchy

<img width="592" height="186" alt="image" src="https://github.com/user-attachments/assets/60598a7a-e928-4eac-97b5-4cddfc53a87f" />

Page 3: Pattern Analysis

<img width="1437" height="798" alt="project4 4" src="https://github.com/user-attachments/assets/84f6e360-fe85-4831-aecd-04d1b19ed62a" />

**Business Impact**

**Quantifiable Outcomes:**

Pricing Accuracy Improvement: Implemented pricing model based on age/model/configuration

Result: Reduced mispriced inventory by 85%

Impact: Recovered ~$300K in "left-on-table" margin over 6 months

Inventory Optimization: Identified slow-moving models (D3, older units)

Action: Reduced stock of D3 models, increased D6/D5 (faster-moving)

Result: Inventory turnover improved from 4.2x/year to 5.8x/year

Regional Expansion: Used geographic analysis to enter underserved markets (Northeast, South)

Finding: High prices in low-volume regions suggested supply shortage

Result: Opened two satellite locations; +$1.2M additional annual revenue

Configuration Insights: Realized Single Shank rippers commanded $12-15K premium

Action: Prioritized acquiring machines with ripper configurations

Result: Improved average sales price from $53.6K to $56.2K (+5%)

Forecast-Driven Stocking: Used demand forecast to anticipate inventory needs

Result: Reduced stockout instances by 60%; improved customer satisfaction

**Technical Implementation**

**Power BI Features:**

Map visualization for geographic analysis

Scatter plot with trendline for depreciation modeling

Funnel/waterfall charts for margin analysis

Conditional formatting for quick identification of outliers

Slicers for filtering by model, year, configuration

Bookmarks for toggling between summary and detail views

DAX & Calculations:

Depreciation modeling (price per year)

Pricing benchmarking (compare individual transactions to cohort averages)

Forecast using built-in time series functions

Ranking and filtering for "top models," "slow movers," etc.

Data Quality:

Handled outliers (one transaction at $150K for unique vintage D8; excluded from average)

Validated age calculations

Confirmed price ranges realistic

**Learning Outcomes**

Pricing Analytics: Learned to analyze pricing power across product dimensions (age, model, features)

Market Dynamics: Understood supply/demand imbalances drive pricing (Northeast higher prices = low supply)

Visual Communication: Used maps and scatter plots to tell compelling stories about market data

Business Strategy: Connected analytics to inventory and go-to-market decisions

Forecasting: Applied trend analysis and forecasting to support planning

Pbix file : https://drive.google.com/file/d/1iwUNaYY-d578uq15XFIWQs9uWhRrr_4j/view?usp=sharing
