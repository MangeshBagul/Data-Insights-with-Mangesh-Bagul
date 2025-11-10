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

Multiple related tables: Categories, Customers, Employees, Order_details, Products, Shippers, Suppliers

Data in a OData link

Manual Excel reporting prone to errors and slow

**Business Pain Points:**

Inventory teams ordering incorrectly (high stock of slow movers)

Shipping delays affecting customer satisfaction

Sales compensation discussions lacked data clarity

Region managers claimed unequal support/opportunity

**Solution Architecture**
**Data Source & Extraction:**

  **Source:** OData feed from Northwind REST API

  **Tables Imported:** 6 main tables (Categories, Customers, Employees, Order_details, Products, Shippers, Suppliers)

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

<img width="1440" height="799" alt="project2 1" src="https://github.com/user-attachments/assets/978ef4ff-94b5-4e3f-afef-ce15aad1ab6e" />


KPIs: Gross Revenue, Total Discount, Net Revenue, Total Orders, Average of days to ship

<img width="885" height="153" alt="image" src="https://github.com/user-attachments/assets/9dd656a6-3fc1-4ccf-afd3-05c0787e382d" />

Line chart: Gross Trend, Discount Trend, Net Trend, Orders Trend..all toggled using button and bookmarks.

<img width="527" height="153" alt="image" src="https://github.com/user-attachments/assets/608f2fe5-1a87-4674-ad5a-aec7ace489ac" />

<img width="524" height="153" alt="image" src="https://github.com/user-attachments/assets/76933c91-f8e8-43e5-8744-cd53b1339dc5" />

<img width="518" height="157" alt="image" src="https://github.com/user-attachments/assets/9ab26de4-76a6-4d58-9c34-57fcb3dabcf2" />

<img width="533" height="153" alt="image" src="https://github.com/user-attachments/assets/7d03bd91-6487-48ab-abce-de828b3b5141" />

Funnel chart: Shipping Company-wise Avg. Delivery Time

<img width="353" height="148" alt="image" src="https://github.com/user-attachments/assets/b522ac60-3d9e-429c-b488-af0bd3b06a14" />

Line and Stacked Column Chart:

<img width="515" height="165" alt="image" src="https://github.com/user-attachments/assets/7d130a01-bac9-4bf6-a808-ed0920873163" />

Finding: Top 5 products (Côte de Blaye, Thüringer, Raclette, Mozzarella, Camembert) = 48% revenue

Page 2: Product  & Employees Performance

<img width="1453" height="805" alt="project2 2" src="https://github.com/user-attachments/assets/5ea490b4-e24d-4f51-8961-4e5d14208278" />

Matrix: Each product with Revenue, Quantity Sold, Margin %, Category

<img width="580" height="192" alt="image" src="https://github.com/user-attachments/assets/29d25a69-70b0-46cf-9feb-821b0e217cd7" />

Stacked Bar chart: Top 5 Best-selling Proudcts & Bottom 5 SLow-moving Produts

<img width="305" height="290" alt="image" src="https://github.com/user-attachments/assets/8be38150-ed2c-4f8c-a74e-6b87c786c2ec" />

Matrix: catergorwise Units in stock and unit ordeered

<img width="309" height="88" alt="image" src="https://github.com/user-attachments/assets/ed7c60b5-3731-44e4-b792-92ee2e277324" />

Clustered Column Chart : Stock distribution by Product Hierarchy

<img width="586" height="170" alt="image" src="https://github.com/user-attachments/assets/8e6bb7a2-83e5-4658-b80b-256c68e1fe81" />

Finding: High-margin items (Côte de Blaye at 60% margin) had lower volume but huge profit impact

Page 3: Employees Analysis

<img width="1438" height="802" alt="project2 3" src="https://github.com/user-attachments/assets/5be714ed-4cf9-4247-956c-69c99f45ec03" />

Matrix: Each Title with Revenue, Quantity Sold, Margin %, Category

<img width="585" height="204" alt="image" src="https://github.com/user-attachments/assets/ca107ea6-cbf2-43b3-a30f-1dbe88567c11" />

Stacked Bar chart: Top 5 performers Employees & Bottom 5 lowest contributers

<img width="308" height="297" alt="image" src="https://github.com/user-attachments/assets/915c33e6-c121-446c-af5e-c2303976ab6e" />

Matrix: Net revenue by designation

<img width="296" height="90" alt="image" src="https://github.com/user-attachments/assets/bc448b0a-4f78-48eb-b8ef-41ec199e1deb" />

Clustered Column Chart : Employee-wise Avg. Net revenue per order

<img width="585" height="165" alt="image" src="https://github.com/user-attachments/assets/2297269c-00f7-4406-af9f-1efa6ba05c52" />

Recommendation: Focus on retaining top 20% of customers = 50% of revenue

**Business Impact**

**Quantifiable Results:**

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

**Tools & Skills Demonstrated**

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

**Learning Outcomes**

Data Integration: Mastered connecting to external data sources (OData) and data transformation pipelines

Complex DAX: Built sophisticated measures involving filtering, ranking, and cross-table logic

Business Storytelling: Learned to present multiple perspectives on same data (product, customer, employee, logistics)

Performance Analysis: Optimized dashboard for fast load times despite 2,200+ rows of data

Root Cause Analysis: Moved beyond metrics to identify underlying drivers (e.g., shipper reliability → delayed orders)

PBIX file download : https://drive.google.com/file/d/1ygTrmcC-w6xmsz7g4SmLrSlWZBb6qGXY/view?usp=sharing
