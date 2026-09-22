# IFEXA Retail Business Performance Intelligence Dashboard

## Project Overview

This project is a Power BI Business Performance Intelligence dashboard built for a Nigerian retail business scenario. The objective
was to turn raw retail transaction data into an interactive management reporting solution that answers three practical questions:

-  How is the business performing?
-  What is driving the performance?
-  Where should management focus?

The project combines data preparation, data modelling, DAX calculations, interactive visualisation, and business storytelling in a single Power BI report.

## Business Problem

Management needs a clear view of sales and profitability across products, categories, regions, customers, employees, and time. Raw transaction data makes it difficult to quickly identify overall revenue and profit performance, monthly changes, leading products and categories, regional differences, salesperson performance,
customer/payment patterns, and areas requiring further investigation.

## Project Objectives

- Consolidate key business KPIs into an executive view.
- Analyse revenue and profit by product, category, region, employee, and month.
- Identify high-performing and underperforming business segments.
- Calculate month-over-month revenue growth.
- Create dynamic management insights using DAX.
- Provide interactive filtering and report navigation.
- Support management discussion with evidence-based observations and
recommendations.

## Tools & Technologies 

### Microsoft Excel
Uses For:
Sourcing the original dataset which was provided in excel format.

### Power BI Desktop   

Used For:
- Data modelling
- Data visualisation
- Dashboard development
- DAX Calculations
  
### Power Query    
Used For:
- Data transformation
- Preparation of dataset for analysis
- Removing Errors
- Removing Duplicates

### DAX  
Used For:
- Calculating Measures
- KPIs
- Time based calculations
- Dynamic insights

## Dataset

The dataset was provided in excel which contains different related tables.
- Fact tables
- Fact_Sales
  The main table containing individual sales record.
- Order ID
- Order Date
- Quantity
- Unit Price
- Product ID
  
- Fact_Targets which target/performance reference data
- Fact_Inventory which contains inventoryrelated information
- Fact_Expenses which contains the expenses information
  
##   Dim_Employees
This contains the employee informations such as:
- Employee Name
- Employee ID
- Department
- Job Level

### Dim_Customers
  This contains the customer informations such as:
  - Customer Type
  - Region
  - State
  - Customer ID
  - City

### Dim_Date 
This are the calendar and time attributes used for time based analysis such as:
- Year
- Month
- Month Name
- Month Number
- Quarter

## Data Preparation

The workflow included reviewing and preparing the dataset for analysis:

- Checking column data types.
- Reviewing blanks and missing values.
- Reviewing duplicate records to prevent the same transaction from being counted more than once.
- Checking category and text consistency.
- Creating and using a dedicated Dim_Date table.
- Establishing relationships between fact and dimension tables.
- Ensuring sales calculations could be filtered by date, product,
customer, employee, and geography.
- A dedicated date dimension was important for monthly revenue analysis
and previous month and MoM calculations.

## Key DAX Measures

- Total Net Sales
Total Net Sales = CALCULATE(SUM(Fact_Sales[Net_Sales]), Fact_Sales[Order_Status] = "Completed")

- Total Revenue
  Total Revenue = SUM(Fact_Sales[Net_Sales])

- Previous Month Revenue
   Previous Month Revenue =CALCULATE([Total Revenue], DATEADD('Dim_Date'[Date], -1, MONTH))

- MoM Growth
  MoM Growth % = DIVIDE([Total Revenue] - [Previous Month Revenue], [Previous Month Revenue],  0)

- Average Order Value
  Average Order Value =DIVIDE( [Total Revenue],[Total Orders],0)

- Total Orders
   Total Orders =DISTINCTCOUNT(Fact_Sales[Order_ID])

- Unique Customers
  Unique Customers = DISTINCTCOUNT(Dim_Customers[Customer_ID])

- Top Category
 Top Category =CONCATENATEX(TOPN(1,ALLSELECTED(Fact_Sales[Category]),[Total Revenue],DESC), Fact_Sales[Category], ", ")

- Performance Insight
  Performance Insight = VAR GrowthValue = [MoM Growth %] RETURN SWITCH(TRUE(),
    GrowthValue >= 0.10, "Revenue is growing strongly.",
    GrowthValue > 0, "Revenue is showing positive growth.",
    GrowthValue = 0, "Revenue is unchanged.",
    GrowthValue > -0.10, "Revenue has declined slightly.",
    "Revenue has declined significantly."
)

This demonstrates the use of SWITCH(TRUE()) to translate a numerical
KPI into a business-friendly message.

## Dashboard Pages

### 1. Executive Overview
The Executive Overview provides a high level view of business overall performance.

Key analysis includes:

- Total Net Sales
- Sales by month
- Sales by employee
- Sales and profit by employee
- Sales and profit by region
- Profit by category
- Profit margin by category
- Sales by category
- Sales by product

### 2. Sales & Profit Analysis {#2-sales--profit-analysis}

This page focuses on the relationship between sales and profitability:

- Sales vs. profit by product
- Sales by product
- Sales by region
- Sales and profit by employee
- Sales and profit by category
- Profit by product

### 3. Management Analysis

This page turns the analysis into management-oriented insights,
including:

- Strongest category
- Weakest category
- Strongest region
- Weakest region
- Salesperson performance

### 4. Dynamic Insights
The Dynamic Insights page adds an executive reporting layer with:

- Total Revenue
- Previous Month Revenue
- MoM Growth %
- Total Orders
- Unique Customers
- Average Order Value
- Monthly Revenue Trend
- Revenue by State
- Revenue by Category
- Top 10 Products by Revenue
- Executive Insight

### 5. Tooltip

A dedicated report page tooltip provides:

- Total Net Sales
- Total Profit
- Profit Margin %
- Total Quantity
- Total Orders

### 6. Presentation

The presentation page structures the analysis around:

- What is happening?
- Why is it happening?
- Where is the biggest opportunity?
- What is the biggest problem?
- What could management do next?
= Key Business Findings
- Revenue
- 
## Dashboard Design & Interactivity

The dashboard includes several interactive features which includes:

- KPI cards
- Bar charts
- Column charts
- Line charts
- Donut chart
- Scatter plot
- Dynamic text insights
- Tooltip
- Navigation buttons
- Interactive filtering

## Skills Demonstrated

- Microsoft Power BI
- Power Query
- Data cleaning
- Data Preparation
- Data modelling
- KPI development
- Business question formulation
- Profitability analysis
- Comparative analysis
- Business storytelling
- Dashboard design
- Relationships
- Interactive visuals
- Report page tooltips
- Navigation
- Dynamic insight cards
- DAX

## Conclusion

The Business Performance Intelligence Dashboard demonstrates how raw data can be transformed into an interactive business intelligence solution. By combining data preparation, modelling, DAX, visualization, and business analysis, the dashboard provides management with a clearer understanding of sales performance, profitability, customers, products, regions, and areas requiring further attention.
