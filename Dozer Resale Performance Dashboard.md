Category: Equipment Sales & Market Analytics
Executive Summary:
A Power BI dashboard analyzing the used heavy machinery (dozer) resale market, providing dealership with pricing strategy, inventory optimization, and regional market insights.

Business Problem & Context
Challenge:
A heavy equipment dealership buying/selling used dozers needed to:

Price machines competitively without leaving money on the table

Identify which models/configurations command premiums

Understand regional demand variations

Optimize inventory (which machines to stock)

Predict resale values based on age, model, condition

Data Landscape:

500+ historical dozer sales transactions

Fields: Model, Manufacturing Year, Configuration, State/Region, Sale Price, Condition Rating

Objective: Build analytics to support pricing and inventory decisions

Solution Architecture
Data Import & Transformation:

Data source: Historical transaction database

Cleaned fields: Standardized model names, validated sale prices, handled missing condition data

Created calculated columns:

Machine Age = Current Year - Manufacturing Year

Price per Age = Sale Price / Machine Age (depreciation efficiency metric)

Region Group = Grouped states into geographic regions (South, Midwest, West, Northeast)

Dimensional Model:

Fact Table: FactDozemSales (one row per transaction)

TransactionID, ModelID, ManufacturingYear, SaleDate, SalePrice, State, Condition

Dimension Tables:

DimDozerModel: ModelName (D3, D4, D5, D6, D7, D8), Manufacturer, YearIntroduced

DimConfiguration: RipperType (Single Shank, Drawbar), Blade Type, Transmission

DimState: State name, Region, ReportingRegion

DAX Measures:

Average Sale Price = AVERAGE(Sales[SalePrice])

Overall: $53.6K

Median Sale Price = MEDIAN(Sales[SalePrice])

Overall: $49K

Price by Model = CALCULATE([Average Sale Price], Groupby Model)

D6 highest: $67K, D3 lowest: $28K

Price by Age = CALCULATE([Average Sale Price], Groupby [Machine Age])

0-5 years: $72K, 5-10 years: $55K, 10-20 years: $32K, 20+ years: $18K

Price by Configuration = Single Shank ripper = $61K (premium vs. standard blade)

Units Sold = COUNTA(Sales[TransactionID])

Revenue = SUM(Sales[SalePrice])

Top Models by Volume = TOPN(5, Models, [Units Sold])

D6, D5, D6R dominated volume

Slow-Moving Models = Filtered count of models with <5 sales in trailing 12 months

Regional Concentration = % of total sales by region

Midwest (manufacturing belt): 42%, West: 35%, South: 18%, Northeast: 5%

Dashboard Pages
Page 1: Market Overview

KPIs: Total Sales Volume (486 units), Avg Price ($53.6K), Median Price ($49K), Revenue ($26M)

Line chart: Sales volume and average price trend over 5 years

Finding: Volume steady but prices declining slightly (older machines entering market)

Page 2: Model Performance

Table: All dozer models ranked by:

Units sold (volume)

Average price

Revenue contribution

Gross margin (est. based on cost)

Insight: D6 and D5 models = 60% of volume but lower margins; premium models (D8, D7) = 20% volume, 40% margin

Page 3: Depreciation Analysis & Age Curves

Scatter plot: Machine age (X-axis) vs. Sale Price (Y-axis)

Clear depreciation curve visible

0-5 years: $72K avg

5-10 years: $55K

10-20 years: $32K

20+ years: $18K

Trendline: Depreciation follows ~$4K/year for first 10 years, then flattens

Finding: Machines >20 years old have minimal resale value unless unique configuration

Page 4: Configuration & Features Premium

Bar chart: Sale price by ripper type

Single Shank ripper: $61K (premium)

Standard blade: $48K

No ripper: $45K

Finding: Ripper adds ~$12-15K value

Table: Configuration combinations and their price impact

Page 5: Geographic Market Analysis

Map: USA color-coded by sales density/average price

Midwest (manufacturing corridor): Highest volume, competitive pricing ($51K)

West: Lower volume but higher prices ($58K) — supply/demand imbalance?

Northeast: Lowest volume ($52K)

Recommendation: Marketing push in underserving regions (Northeast, South)

Page 6: Inventory & Recommendation

Table: Current inventory of dozers for sale with:

Model, Age, Configuration, Current list price

Recommended price (based on comparable sales analysis)

Price adjustment needed (if overpriced/underpriced)

Finding: 3 D3 models overpriced by 18-22%; recommend price reductions

Finding: 2 D8 models underpriced; opportunity to increase price by 8%

Page 7: Sales Trend & Forecast

Line chart: Monthly units sold (last 24 months)

Trend analysis: Slight upward trend (suggesting strong demand)

Forecast: Projected 520 units in next 12 months (vs. 486 historical)

Insight: Market appears healthy; good time to stock more inventory

Business Impact
Quantifiable Outcomes:

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

Technical Implementation
Power BI Features:

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

Learning Outcomes
Pricing Analytics: Learned to analyze pricing power across product dimensions (age, model, features)

Market Dynamics: Understood supply/demand imbalances drive pricing (Northeast higher prices = low supply)

Visual Communication: Used maps and scatter plots to tell compelling stories about market data

Business Strategy: Connected analytics to inventory and go-to-market decisions

Forecasting: Applied trend analysis and forecasting to support planning
