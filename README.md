# Sales Analysis

##  Objective

Design an interactive dashboard for business stakeholders.
- Choose right KPIs (Sales, Profit, Growth)
- Use slicers/filters for interactivity
- Include time-series analysis
- Add cards for totals/summary
- Apply consistent color theme
- Create navigation menu (if possible)

 Dataset: Any  Sales_Financial dataset (from kaggle)
 Outcome: Learn how to create dashboards that inform business decisions.
 
## 🗺️ Project Overview  

This project focuses:  
- **Data Modeling** – creating clean, aggregated views for products and customers.  
- **Data Visualization with Power BI** – building interactive dashboards.  
- **Insights & Recommendations** – delivering actionable solutions aligned with the problem statement. 

## 🛠️ Tools & Technologies  

| Tool          | Purpose                                     |  
|----------------|---------------------------------------------|
| **Power BI**    | Data Modeling, Visualization, Dashboards  |  
| **DAX**         | Calculated Measures, Advanced Analytics   |  

## 🌟 Project Highlights  

- ✅ Created **3 comprehensive Power BI dashboards**:  
  1. Sales Performance Summary + Time Series analysis + Geographical analysis
  2. Product Insights  
  3. Customer Insights  

- ✅ Built advanced DAX measures for MoM/YoY growth, moving averages, and forecasting.  
- ✅ Delivered clear insights on revenue drivers, customer behavior, and market opportunities.

##  Dataset overview
- gold.fact_sales.csv : All sales transacion records for all purchases (fact table) 
- gold.dim_customers.csv : Customer Information (dimension table)
- gold.dim_products.csv : Products information (dimension table)


## 📊 Data Visualization – Power BI Dashboards  

### 📄 Page 1: Sales Performance Overview + Time Series + Geographical  

#### 🎯 Purpose: High-level KPIs, revenue, time series, and geographical insights.  

#### 🔸 Visuals:  
- KPI Cards: Revenue, Total Orders, Total Customers, YoY Growth %  
- Revenue by Country (Column Chart)  
- Top 5 Products by Revenue (Column Chart)  
- Donut Charts:  
  - Revenue by Customer Segment  
  - Revenue by Product Segment  
  - Revenue by Weekday vs Weekend  
- Time Series:  
  - Yearly & Monthly Revenue (Line Chart)  
  - Cumulative Revenue (Area Chart)  
  - Monthly Growth % (Column Chart)  
  - Revenue Forecast (2 Years Ahead)  
  - 3-Month Moving Avg (Line Chart)  
- Slicers: Year, Country, Category  
- Page Navigation Enabled

DAX:

    Total Sales = SUM(fact_sales[sales_amount])

    Total Orders = DISTINCTCOUNT(order_number)

YoY Growth using:

    Latest Year = MAX('Date Table'[Year])
    Latest Year Revenue = CALCULATE( [Total Revenue], 'Date Table'[Year] = MAX('Date Table'[Year]))
    Previous Year Revenue = 
    CALCULATE(
        [Total Revenue],
        'Date Table'[Year] = MAX('Date Table'[Year]) - 1
    )

    YoY Growth % = 
    DIVIDE([Latest Year Revenue] - [Previous Year Revenue], [Previous Year Revenue])

Monthly growth using: - 
    
    Previous Month Revenue = 
    CALCULATE(
        [Total Revenue],
        PREVIOUSMONTH('Date Table'[Date]))

    MoM Growth % = 
    IF(NOT ISBLANK([Previous Month Revenue]), DIVIDE([Total Revenue] - [Previous Month Revenue], [Previous Month Revenue], BLANK()))

For Cumulative revenue graph -
    
    Running Total Revenue = 
    CALCULATE(
    [Total Revenue],
    FILTER(
        ALLSELECTED('Date Table'[Date]),
        'Date Table'[Date] <= MAX('Date Table'[Date])
        )
    )
    

For 3- month moving avg -

    3-Month Moving Avg = 
    AVERAGEX(
    DATESINPERIOD(
        'Date Table'[Date],
        MAX('Date Table'[Date]),
        -3,
        MONTH
        ), [Total Revenue]
    )

### 🚴‍♂️ Page 2: Product Insights  

#### 🎯 Purpose: Deep dive into product performance.  

#### 🔸 Visuals:  
- Scatter Plot: Avg Order Value vs Total Quantity (Bubble size: Total Sales, Color: Category)  
- Donut Charts (x3): Revenue by Subcategory for Bikes, Clothing, Accessories  
- Total Orders by Product Segment  
- Total Revenue by Product Segment  
- Product KPI Table (report_product view)  
- Slicers: Year, Country, Category
- Page Navigation Enabled
  
### 👥 Page 3: Customer Insights  

#### 🎯 Purpose: Analyze customer behavior and value.  

#### 🔸 Visuals:  
- Customer Lifecycle Scatter Plot (Lifespan vs Recency)  
- Donut Charts:  
  - Customer Segments (VIP, Regular, New)  
  - Revenue by Customer Segment  
  - Revenue by Age Group (Bar Chart)  
  - Revenue by Gender (Bar Chart)  
- Customer Count by Country (Bar Chart)  
- Customer KPI Table (report_customer view)  
- Slicers: Year, Country, Category
- Page Navigation Enabled

## 🔥 Key Insights & Solutions  

### 📌 Insights:  
- Bikes generate ~60% of revenue.  
- Clothing has high sales volume but lower revenue contribution.  
- VIP customers drive a disproportionate share of revenue.  
- USA and Germany are top-performing countries.  
- Strong seasonal peaks (summer).  
- Several products underperform and may need promotions or removal.  

### 🏆 Solutions:  
- Retention Focus: Prioritize engagement for VIPs and Regular customers.
- Increase inventory for high-performing products.  
- Marketing Strategy: Target countries with high sales potential; promote during peak months.  
- New Customer Acquisition: Target **female customers** (nearly 50% of revenue); design products like bikes with compartments for essentials.  
  - Capture younger customers for long-term growth.  
- Collaborate with **touring groups** to rent tour bikes, which currently underperform.

# Snapshot of the Dashboard
## Sales Performance
<img width="1269" height="715" alt="image" src="https://github.com/user-attachments/assets/b68584fb-6d0c-4244-bcb0-55ba161a9743" />


## Product Insights
<img width="1268" height="712" alt="image" src="https://github.com/user-attachments/assets/2218af53-da3e-4c43-bd35-536fc0805f08" />


## Customer Insights
<img width="1268" height="714" alt="image" src="https://github.com/user-attachments/assets/a0938228-cea2-401f-bb52-cfb86da738bf" />
