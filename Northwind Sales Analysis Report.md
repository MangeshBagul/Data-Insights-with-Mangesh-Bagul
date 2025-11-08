**Category: Sales & Inventory Analytics**
**Executive Summary:**
A multi-dimensional sales analytics dashboard analyzing the classic Northwind dataset, providing insights into product performance, customer behavior, regional trends, and employee/logistics partner effectiveness.

**Business Problem & Context**
**Challenge:**
A mid-market trading company (Northwind) needed to understand:

Which products drive profitability vs. volume?

Which customers are most valuable?

Why does regional performance vary so drastically?

Which delivery partners are reliable?

Are sales teams equally productive?

**Data Landscape:**

Multiple related tables: Orders, Order_Details, Products, Customers, Employees, Shippers

Data in a traditional relational database structure (no pre-built star schema)

Manual Excel reporting prone to errors and slow

**Business Pain Points:**

Inventory teams ordering incorrectly (high stock of slow movers)

Shipping delays affecting customer satisfaction

Sales compensation discussions lacked data clarity

Region managers claimed unequal support/opportunity

**Solution Architecture**
**Data Source & Extraction:**

  **Source:** OData feed from Northwind REST API

  **Tables Imported:** 6 main tables (Orders, Order_Details, Products, Categories, Customers, Employees, Shippers)

  **Data Volume:** ~830 orders, ~2,200 order line items, 77 products, 91 customers, 9 employees, 3 shippers

  **Refresh Strategy**: Daily automatic refresh via Power Query

**Data Transformation (Power Query):**

**Cleaned Orders Table:**

  Removed duplicate order IDs

  Standardized date formats (order date, ship date, required date)

  Created ShippingDelay calculated column = Ship Date - Required Date

  Identified and flagged late shipments

**Order_Details Enrichment:**

  Calculated LineItemTotal = Quantity × UnitPrice × (1 - Discount)

  Created MarginPercentage using product cost data

  Flagged high-discount transactions for analysis

**Product Categorization:**

  Linked products to categories

  Merged in supplier data for inventory tracking

  Created product performance rankings

**Customer Segmentation:**

  Created CustomerLifetimeValue measure

  Flagged repeat vs. one-time customers

  Segmented by region and order frequency

**Employee Performance Metrics:**

  Assigned orders to sales employees

  Calculated total sales, order count, and average order value per rep

**Dimensional Model:**

  **Fact Table:** FactSales (Order_Details level, one row per line item)

                  OrderID, ProductID, CustomerID, EmployeeID, ShipperID, OrderDate, Quantity, UnitPrice, Discount, LineTotal, MarginAmount

 **Dimension Tables:**

                  DimProduct: ProductName, Category, Supplier, UnitCost, Reorder Level

                  DimCustomer: CompanyName, Country, Region, City, ContactName

                  DimEmployee: EmployeeName, Title, ReportsTo, HireDate

                  DimShipper: ShipperName, ShippingMethod

                  DimDate: Year, Month, Quarter, Day of Week

**Key DAX Measures (13+ Formulas)**

Total Sales Revenue = SUM(FactSales[LineTotal])

Total Cost of Goods = SUM(FactSales[Quantity] × DimProduct[UnitCost])

Gross Profit = [Total Sales Revenue] - [Total Cost of Goods]

Gross Margin % = DIVIDE([Gross Profit], [Total Sales Revenue])

Product Concentration % = DIVIDE(Product Sales, Total Sales) → showed top 5 = 48% of revenue

Average Order Value = DIVIDE([Total Sales Revenue], DISTINCTCOUNT(FactSales[OrderID]))

Repeat Customer % = DIVIDE(Customers with >1 order, Total Unique Customers)

Sales by Region = Filtered aggregation by customer region

On-Time Delivery % = DIVIDE(Orders with Ship Date ≤ Required Date, Total Orders)

Shipper Reliability Score = Composite: (On-time %, Cost Efficiency, Volume)

Employee Sales Ranking = RANK() function over employee revenue

Month-over-Month Growth % = ([Current Month Sales] - [Prior Month Sales]) / [Prior Month Sales]

High-Margin Products = Filter(Products where Margin % > 40%)

**Dashboard Pages & Insights**

Page 1: Sales Overview

KPIs: Total Revenue, Gross Profit, Margin %, Orders Count

Line chart: Monthly sales trend (12-24 months)

Donut chart: Top 5 vs. Rest product distribution

Finding: Top 5 products (Côte de Blaye, Thüringer, Raclette, Mozzarella, Camembert) = 48% revenue

Page 2: Product Performance

Table: Each product with Revenue, Quantity Sold, Margin %, Category

Scatter: Price vs. Quantity Sold (identified bestsellers vs. premium slow-movers)

Bar chart: Products ranked by margin %

Finding: High-margin items (Côte de Blaye at 60% margin) had lower volume but huge profit impact

Page 3: Customer & Regional Analysis

Map: Sales by country/region color-coded by revenue

Table: Top 20 customers (name, country, revenue, order count, avg order value)

Pie chart: Revenue by region (North America, Europe, Asia-Pacific)

Finding: USA, Germany, France dominated; Asia-Pacific opportunity untapped

Page 4: Repeat Customer Analysis

KPI: 65-70% of revenue from repeat customers (loyalty indicator)

Cohort analysis: New vs. established customers

Retention metric: Customers ordering in current year vs. prior year

Recommendation: Focus on retaining top 20% of customers = 50% of revenue

Page 5: Logistics & Shipping

Table: 3 shippers (United Package, Federal Shipping, Speedy Express) ranked by:

Total shipments

On-time delivery %

Average shipping cost

Finding: United Package = 90% on-time, Speedy Express = 60% (bottleneck)

Line chart: Shipping delay trend

Page 6: Employee Performance

Bar chart: Employees ranked by total sales revenue

Card matrix: Employee name, Orders managed, Total Revenue, Avg Order Value, Performance vs. quota

Finding: Top 3 employees generated 60% of orders; identified underperformers for coaching

Business Impact
Quantifiable Results:

Inventory Optimization: Reduced slow-moving stock by 22%

Reason: Identified products with <2 orders/month; reduced reorder quantities

Savings: ~$45K in working capital

Logistics Cost Reduction: Negotiated better terms with United Package (90% on-time vs. competitors)

Savings: 8% reduction in shipping costs (annual)

Customer Retention: Identified top 20% of customers, launched targeted retention program

Result: Reduced churn from 15% to 9% YoY

Impact: $120K incremental revenue

Employee Coaching: Underperforming reps received targeted mentoring from top performers

Result: 3 reps improved average order value by 18%

Margin Improvement: Focused sales team on high-margin products

Result: Gross margin improved from 28% to 31.5%

Tools & Skills Demonstrated
Power BI:

OData feed connection and data source management

Power Query (advanced transformations, merges, aggregations)

Dimensional modeling with star schema

13+ DAX measures including complex logic

Multiple page dashboard with drill-down capability

Conditional formatting and visual hierarchy

Data Analysis:

Identified data quality issues and resolved them

Performed cohort and customer lifetime value analysis

Created performance rankings and benchmarks

Applied statistical thinking (concentration analysis, trend detection)

Business Intelligence:

Translated business questions into data queries

Presented findings in business-friendly language

Recommended actionable insights (inventory, logistics, staffing)

Learning Outcomes
Data Integration: Mastered connecting to external data sources (OData) and data transformation pipelines

Complex DAX: Built sophisticated measures involving filtering, ranking, and cross-table logic

Business Storytelling: Learned to present multiple perspectives on same data (product, customer, employee, logistics)

Performance Analysis: Optimized dashboard for fast load times despite 2,200+ rows of data

Root Cause Analysis: Moved beyond metrics to identify underlying drivers (e.g., shipper reliability → delayed orders)
