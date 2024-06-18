# <img src="https://media.licdn.com/dms/image/D4D0BAQFONtccW6kb_Q/company-logo_200_200/0/1692808405632?e=2147483647&v=beta&t=5-c1hlCyZ6eWKCDV5g9-B9tiZcc9GRE2MkQVg-vCmv8" width="4%" height="4%"> MeriSKILL - Sales Analysis

<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/blob/main/Assets/MeriSKILL%20Repo%20Banner.jpg" width="900px" height="600px"> </div>

This repository serves as my documentation for the MeriSKILL Sales Analysis - Power BI Project.

It was created as a learning project as part of my Internship assignment at: [MeriSKILL](https://sites.google.com/view/meriskill/home) during May - June 2024.

It showcases my competancy to work with Microsoft Power BI and demonstrates my proficiency in essential Power BI concepts like Data Profiling, ETL with Power Query, Semantic Data Modelling, DAX Measures & DAX Calculated Columns, Dashboard Designing, Visualization, Conditional Formating, Filters, Bookmarks, Page Navigation, Publishing and Report Optimization etc.

The entire project has been implemented using Microsoft Power BI Desktop 2.128.751.0 and published on Microsoft Power BI Service.

---

## Purpose:
This report delves into a comprehensive analysis of the sales dataset provided by MeriSkill identify trends, top-selling products and revenue metrics aimed at extracting valuable insights to facilitate strategic data-driven business decision-making and create visualizations to present my findings effectively.

## Table of Contents:
Please find the resource links for the project below:
- [Sales Raw Data](https://github.com/5ifar/MeriSKILL_Sales_Analysis/tree/main/Sales%20Raw%20Data)
- [Data Model](https://github.com/5ifar/MeriSKILL_Sales_Analysis/blob/main/Power%20BI%20Dashboard/Data%20Model.JPG)
- [Project Implementation](https://github.com/5ifar/MeriSKILL_Sales_Analysis/blob/main/Project%20Implementation/Documentation.md)
- [Live Dashboard Link](https://app.powerbi.com/view?r=eyJrIjoiZDgxZTkxMDEtN2JkMi00N2Y5LTgwY2ItMmJmNTNmZDEzNjMzIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)

## Tools used:
1. Microsoft Power BI: for Data Cleaning, Data Analysis, Data Visualization & Dashboarding
2. GitHub - for Documentation

## Skills & Methodologies implemented:
1. Data Cleaning: Power Query
2. Data Manipulation: DAX Measures & Columns
3. Data Modelling and Normalization
4. Data Visualization
5. Dashboarding: Filters, Custom Icon Buttons, Bookmarks, Page Navigation
6. Report Publishing and Report Optimization
7. Documentation

## About the Dataset:
The original raw dataset spans from 1 January 2019 to 1 January 2020 and includes information about product sales, quantities, revenue and geographic data. It contains only 1 table with 10 columns and 1,85,950 rows.

The data was later normalized into 3 tables - fact_Sales, dim_Product & dim_Location during project implementation. The cleaned dataset has - fact_Sales (1,85,950 rows), dim_Product (19 rows) & dim_Location (1,40,787 rows). Addional dim_Date table was created which has 365 rows.

Data Overview: Year: 2019, Months: 12, Products: 19, States: 8, Cities: 9 & Addresses: 1,40,787.

### Sales Data Dictionary:
|Column Name|Type|Description|
|-|-|-|
|Order Id|int|Unique product sales order id|
|Product|char|Name of Product|
|Quantity Ordered|int|Quantity of product sold|
|Price Each|float|Product price per unit|
|Order Date|date|Date of product sale|
|Purchase Address|char|Location of product order|
|Month|int|Month of sale|
|Sales|float|Sales order value|
|City|char|City of product order|
|Hour|int|Hour of product sale|

## Data Integrity:
ROCCC Evaluation:
- Reliability: LOW - The raw dataset is created and updated by MeriSKILL. It has only 1 file.
- Originality: MED - First party provider (MeriSKILL)
- Comprehensiveness: LOW - Only 1 CSV File was provided. Dataset contains few parameters for Products & Location.
- Current: LOW - Dataset was created on 2019, almost 5 years old. So its very obsolete & not very relevant.
- Citation: LOW - No official citation/reference available.

---

## Data Model:
### Entity Relationship Diagram (ERD):

<img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/blob/main/Assets/MeriSKILL%20Sales%20Analysis%20Data%20Model.JPG" width="100%" height="100%">

---

## Analysis Insights:
Key findings from data trend analysis constitute insights into product preferences, sales trends, and regional variations. The Sales data revealed a significant spike in sales figures during December, which can be potentially attributed to the festive season.

**I. Top Cities by Revenue:**

- **San Francisco** (8.3M $) leads in revenue, possibly due to the in demand tech market and higher consumer spending power in the Silicon Valley.
- **Los Angeles** (5.5M $) and **New York City** (4.7M $) follow, likely owing to their large population density and economic activity.
<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/149a9260-b241-4184-a905-05b12fb35b8c" width="40%" height="40%"> </div>

**II. Top States by Order Value:**

- **Georgia** state (196.1 $) boasts the highest Average Order Value despite being the 5th state by Revenue and Total Orders.
- **California** state (192.1 $) lags behind as the 3rd lowest Average Order Value state despite being the highest state by Revenue and Total Orders.
<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/0be7a536-7d36-4518-9dae-79293de56665" width="40%" height="40%"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/51e66426-51c3-4617-9fdd-45948f10b893" width="41%" height="41%"> </div>

**III. Product Insights:**

- Apple products, especially **MacBooks** (8M $) and **iPhones** (4.8M $) are the largest contributors to revenue, possibly due to high product demand and new product releases during year-end.
<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/a17a3bd9-9cf4-4196-8fb2-94f10417e22f" width="40%" height="40%"> </div>

- **AAA Battery** (31K) and **AA Battery** (28K) while sold in high quantities, generate less revenue (93K $ and 106K $ respectively) indicating lower product prices.
<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/27eeed52-067e-4e3c-9863-fb6fb6326fae" width="40%" height="40%"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/431305aa-256e-4dc4-b63b-74087c895220" width="40%" height="40%"> </div>

- **Thinkpad Laptop** (4.1K) while sold in low quantity, generates the 3rd largest revenue (4.1M $) indicating higher product prices.
<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/4a67eb50-75cb-4059-bb8a-16db015b867d" width="40%" height="40%"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/d49b09d9-18c2-4137-ab9a-7836b2e363b6" width="40%" height="40%"> </div>

**IV. Sales by Month and Year:**

- Sales peak in the month of **December**, aligning with the holiday season and gifting tradition.
- An increase in **April** might suggest spring-related sales or promotions.
<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/e23df96d-5293-4b89-8f53-5b4f4066a2fc" width="40%" height="40%"> </div>

**V. Sales by Time:**

- Peaks at **12 PM** and **7 PM** suggest lunchtime and after-work hours as prime buying times. Further analysis could explore targeted marketing during these hours for enhanced sales.

---

## Data-driven Recommendations:
Based on the insights derived, it is recommended to capitalize on the festive season by strategizing marketing campaigns and product promotions. Additionally, efforts should be directed towards understanding consumer preferences to enhance product offerings and drive sales.

- Holiday Season Planning:
— Strategize targeted marketing campaigns and inventory management in the month of November for a expected surge in sales during the holiday season especially in **December**. Highlight popular high sales volume and revenue products and offer special discounts to boost sales.
- Apple Product Promotions:
— Align promotions and marketing efforts for Apple products, especially **MacBooks** and **iPhones** around **December** to maximize revenue during the year-end product release season.
- Product Diversification:
— Consider diversifying product offerings to include more high-margin items like the **Thinkpad Laptop** (4.1M $) while balancing revenue generation with high quantities and low-margin affordable products.
- Customer Engagement:
— Engage customers with loyalty programs or special offers on lower revenue generating months like **January** (1.8M $) and **September** (2.1M $) to boost sales.

These recommendations aim to optimize sales strategies based on the observed patterns, promoting revenue growth and customer engagement.

---

## Dashboard Preview:
<div align="center"> <img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/d85474fb-c013-4b56-b484-749a362b9c17" width="100%" height="100%"> </div>

[MeriSKILL Sales Analysis Live Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZDgxZTkxMDEtN2JkMi00N2Y5LTgwY2ItMmJmNTNmZDEzNjMzIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)

