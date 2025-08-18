# 🚴 Adventure Works Cycles Analysis

Adventure Works is a **Microsoft sample database** that simulates a multinational manufacturing company producing and selling cycles and related products.  
In this project, I connected and shaped the raw data using **Power Query**, built a **relational data model**, and created **calculated fields with DAX measures**.  
Finally, I developed an **interactive Power BI Dashboard** to analyze the company’s sales performance, customer demographics, and product profitability.  

---

## 💡 Project Overview
This project aims to provide **actionable insights** for Adventure Works management by answering key business questions such as:
- Which customers and regions contribute the most to profit?  
- What product categories drive sales growth?  
- How do demographics (income, occupation) affect customer behavior?  
- How does pricing impact profitability (via What-If analysis)?  

The final dashboard is designed to help stakeholders make **data-driven decisions** and track performance effectively.  

---

## 🛠 Tools Used  
- **Excel** (data prep/sample dataset)
👉 [Datasets File](./Datasets/)
- **Power BI** – Data visualization and dashboarding  
- **Power Query** – Data cleaning and shaping  
- **DAX (Data Analysis Expressions)** – Calculations and measures
- **What‑If parameter** for single-value slicer

---

## 🗂️ Schema Diagram

Here is the schema used for data modeling in Power BI:

<img width="1646" height="637" alt="image" src="https://github.com/user-attachments/assets/098fd486-6feb-4368-865f-40ad0a5108fd" />

<sup>*ERD showing relationships among dimension and fact tables*</sup>

---
---

## ❓ Key Business Questions Answered
1. Which customers and regions are most profitable?  
2. What product categories contribute the most revenue & profit?  
3. How do income levels and occupations affect purchasing?  
4. What is the effect of price adjustment (What-If parameter) on total profit?  
5. How does sales performance vary across time (year/quarter/month)?  

---

---

## 🧮 Key Measures (DAX examples)

```DAX
-- Core
Total_Order = DISTINCTCOUNT(AW_Sales_Data_2015_17[OrderNumber])
Total_Revenue = SUMX(AW_Sales_Data_2015_17,AW_Sales_Data_2015_17[OrderQuantity]*RELATED(AW_Products[ProductPrice]))
Total_Cost = SUMX(AW_Sales_Data_2015_17,AW_Sales_Data_2015_17[OrderQuantity]*RELATED(AW_Products[ProductCost]))
Total Profit  = [Total Revenue] - [Total Cost]

-- What‑If parameter (auto-created by Power BI when you add a Numeric Range parameter)
-- 'Price Adjustment (%)'[Price Adjustment (%)]  -- between -1 and +1 for -100%..+100%

Adjusted_Price = [Avg_retail_Price]*(1+'Price_Adjustment(%)'[Price_Adjustment(%) Value])

-- Example: Income banding
Income Level = 
IF(
    AW_Customers[AnnualIncome] <= 40000, "Low",
    IF(
        AW_Customers[AnnualIncome] <= 90000, "Average",
        IF(
            AW_Customers[AnnualIncome] <= 130000, "High",
            "Very High"
        )
    )
)
```

---
