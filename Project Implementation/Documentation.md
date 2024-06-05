# 🧬 MeriSKILL Sales Analysis Project Phase-wise Implementation

---

## Table of Contents
- [Phase 1: ETL with Power Query](#phase-1-etl-with-power-query)
- [Phase 2: Data Modelling & Calculated Columns](#phase-2-data-modelling--calculated-columns)
- [Phase 3: Home View](#phase-3-home-view)
- [Phase 4: Insights View](#phase-4-insights-view)

---

## Phase 1: ETL with Power Query

### Step 1: Extraction & Transforming Data:

- Extract Data: Get Data → Text/CSV → `Sales Data.csv` → Transform Data
- Set Column data types: Transform Tab → Detect Data Type. This action will automatically identify the data type of each column and convert them as needed.

  Ensure these columns: Order ID, Month → Text (to avoid unnecessary aggregation) Price Each, Sales → Fixed Decimal Number (to be treated as Currency)
- Split the Orderdate data into Orderdate and Ordertime stamp data using the Split Column by Space Delimiter. Set Data types as Date and Time respectively.
- Remove unnecessary hour column from Sales Data. Rename Sales Data → `fact_Sales`.
- Normalize Location Data:
1. Get and Load the Sales Data Table again to the Power Query and rename the new table as `dim_Location`. Only keep Purchase Address and City columns. Remove Duplicates from the Purchase Address column.
2. Duplicate the Purchase address column and Split the Purchase Address column by each Comma delimiter to get Street Data and again split based on Space delimiter to get State and Postal Code data. Replace State Abbreviations by State Name.
3. Merge `fact_Sales` and `dim_Location` using Left Outer Join and expand to show the Location Key column. Remove the Purchase Address column from `fact_Sales` since now Location Key will act like the Foreign Key to `dim_Location` table.
- Normalize Product Data:
1. Get and Load the Sales Data Table again to the Power Query and rename the new table as `dim_Product`. Only keep the Product column.
2. Remove duplicates and add Index Column. Add a Prefix ‘P’ to the Index column to act as a Primary Key for Products table.
3. Merge `fact_Sales` and `dim_Product` using Left Outer Join and expand to show the Product Key column. Remove the Product column from `fact_Sales` since now Product Key will act like the Foreign Key to `dim_Product` table.
- For both the above cases of Normalization we cannot use Reference tables since we’ll eventually be unable to merge the Primary Key Column created in the dim tables with the fact table if the dim table is a reference of the fact table.

### Step 2: Creating custom Date Table:

1. New Source → Blank Query → Custom M Code: `= {Number.From(#date(2019,1,1))..Number.From(#date(2020,1,1))}` → Will create a list of date values → Convert to Table → Set Data type as Date → Rename column as Date
2. Add columns → Day, Day Name, Start of Week, Start of Month & Month Name.
3. Rename as dim_Date and Close & Apply changes to load data to PBI Frontend.

---

## Phase 2: Data Modelling & Calculated Columns

### Step 1: Creating Table Relationships

- A robust data model was established, linking key tables to enable efficient analysis.

|Primary Key (Dimension table) (1)||Secondary Key (Fact table) (*)|
|-|-|-|
|Date (dim_date)|→|Orderdate (fact_Sales)|
|Location Key (dim_Location)|→|Location Key (fact_Sales)|
|Product Key (dim_Product)|→|Product Key (fact_Sales)|

<img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/aeb9cfc3-5eaa-49b3-9521-3d7f9e58c166" width="40%" height="40%">

---

## Phase 3: Home View

### Step 1: Configure Slicers

- Add a Product Slicer with Multi-Select enabled and Select All option shown.
- Add a City Slicer with Multi-Select enabled and Select All option shown.

### Step 2: Creating Measures Table

- To collect all report measures in a single place we’ll create a measures table to store all the measures together.
- Data View → Enter Data → Rename as measure.

### Step 3: Basic Measures

- `Revenue = SUM(fact_Sales[Sales])`
- `Total Orders = DISTINCTCOUNT(fact_Sales[Order ID])`
- `Total Qty Sold = SUM(fact_Sales[Quantity Ordered])`
- `Avg Order Value = [Revenue] / [Total Orders]`

### Step 4: Revenue by Month Visual

- Create a Area Chart visual with Months on the X Axis and Revenue measure on the Y Axis.
- Filter out the Jan 2020 data using visual level filters to avoid unusual trend due to incomplete data.
- To create a Chronological order for the months, follow these steps:

  Select the column containing the months → Navigate to the "Column Tools" and choose "Sort Column." → Select "Sort by Month Number" to sort the months in chronological order.
- Add Week and Date field to the X Axis to enable Data drilling. Setup zoom slider to view drilled data better.

### Step 5: Revenue by States Visual and Custom Revenue - Avg Order Value Toggle

- Add a Shape Map with State location data and Color legend gradient based on Revenue measure.
- Set the Map Settings Projection to Albers USA and Zoom on selection.
- Setup a toggle between Revenue and Avg Order Value measure fields using custom icon blank button.
- Use the Toggle Setup to switch between US State Maps plotted against Revenue or Avg Order Value.

### Step 6: Products by Revenue Visual

- Create a Clustered Bar Chart visual with Product on Y Axis and Revenue on X Axis.
- Filter out to display on the Top 5 Products by configuring a Top N Filter on the visual Product field based on Revenue field.
- Duplicate the above visual and edit the filter to display the Bottom 5 Products by configuring a Top N Filter on the visual Product field based on Revenue field.

### Step 7: Products by Quantity Sold Visual

- Create a Clustered Bar Chart visual with Product on Y Axis and Total Qty Sold measure on X Axis.
- Filter out to display on the Top 5 Products by configuring a Top N Filter on the visual Product field based on Total Qty Sold field.
- Duplicate the above visual and edit the filter to display the Bottom 5 Products by configuring a Top N Filter on the visual Product field based on Total Qty Sold field.

### Step 8: Custom Revenue - Quantity Sold Value Toggle

- Setup a toggle between Revenue and Quantity Sold Value measure fields using custom icon blank button.
- Create Bookmarks: Products by Revenue & Products by Quantity Sold.
- Use the Toggle Setup Action to switch between Top and Bottom 5 Products plotted against Revenue or Quantity Sold Value.
- Revenue Toggle Button → Action: Bookmark: Products by Quantity Sold → Displays the Top & Bottom 5 Products by Quantity Sold Visuals
Quantity Sold Toggle Button → Action: Bookmark: Products by Revenue → Displays the Top & Bottom 5 Products by Revenue Visuals

### Step 9: Sales Performance Matrix Visual

- Create a Matrix visual with State and City as Row fields and Revenue, Total Orders and Avg Order Value measures as Value fields.
- Format Revenue values in Millions and Total Orders values in Thousands.
- Apply Data Bars and Font Color Formatting on Revenue and Avg Order Value Columns respectively.

### Step 10: Slicers

- Create Slicer visualizations by drag and drop the Product, City, Month & Day fields into the slicer option.
- Display the slicer in a vertical list by accessing the slicer settings and choosing the option for a vertical column layout.
- Add a Reset Button and configure the Button Action to Reset all the Slicers applied.

### Step 11: Insights Button

- Add an Information Icon button and set Button Action to Page Navigation to Insights View.

---

## Phase 4: Insights View

### Step 1: Back Button

- Add an Back Icon button and set Button Action to Page Navigation back to Home View.

### Step 2: Insights and Findings

Key findings from data trend analysis constitute insights into product preferences, sales trends, and regional variations. The Sales data revealed a significant spike in sales figures during December, which can be potentially attributed to the festive season.

**Top Cities by Revenue:**

- **San Francisco** (8.3M $) leads in revenue, possibly due to the in demand tech market and higher consumer spending power in the Silicon Valley.
- **Los Angeles** (5.5M $) and **New York City** (4.7M $) follow, likely owing to their large population density and economic activity.

**Top States by Order Value:**

- **Georgia** state (196.1 $) boasts the highest Average Order Value despite being the 5th state by Revenue and Total Orders.
- **California** state (192.1 $) lags behind as the 3rd lowest Average Order Value state despite being the highest state by Revenue and Total Orders.

**Product Insights:**

- Apple products, especially **MacBooks** (8M $) and **iPhones** (4.8M $) are the largest contributors to revenue, possibly due to high product demand and new product releases during year-end.
- **AAA Battery** (31K) and **AA Battery** (28K) while sold in high quantities, generate less revenue (93K $ and 106K $ respectively) indicating lower product prices.
- **Thinkpad Laptop** (4.1K) while sold in low quantity, generates the 3rd largest revenue (4.1M $) indicating higher product prices.

**Sales by Month and Year:**

- Sales peak in the month of **December**, aligning with the holiday season and gifting tradition.
- An increase in **April** might suggest spring-related sales or promotions.

**Sales by Time:**

- Peaks at **12 PM** and **7 PM** suggest lunchtime and after-work hours as prime buying times. Further analysis could explore targeted marketing during these hours for enhanced sales.

### Step 3: Recommendations

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
