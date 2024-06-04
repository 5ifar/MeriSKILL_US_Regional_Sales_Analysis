# 🧬 MeriSKILL Sales Analysis Project Phase-wise Implementation

---

## Table of Contents
- [Phase 1: ETL with Power Query](#phase-1-etl-with-power-query)
- [Phase 2: Data Modelling & Calculated Columns](#phase-2-data-modelling--calculated-columns)

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

## Phase 2: Data Modelling & Calculated Columns

### Step 1: Creating Table Relationships

- A robust data model was established, linking key tables to enable efficient analysis.

|Primary Key (Dimension table) (1)||Secondary Key (Fact table) (*)|
|-|-|-|
|Date (dim_date)|→|Orderdate (fact_Sales)|
|Location Key (dim_Location)|→|Location Key (fact_Sales)|
|Product Key (dim_Product)|→|Product Key (fact_Sales)|

<img src="https://github.com/5ifar/MeriSKILL_Sales_Analysis/assets/146955609/aeb9cfc3-5eaa-49b3-9521-3d7f9e58c166" width="40%" height="40%">

## Phase 3: Home View - Visualization

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

### Step 4: Revenue by Month  Visual

- Create a Area Chart visual with Months on the X Axis and Revenue measure on the Y Axis.
- Filter out the Jan 2020 data using visual level filters to avoid unusual trend due to incomplete data.
- To create a Chronological order for the months, follow these steps:

  Select the column containing the months → Navigate to the "Column Tools" and choose "Sort Column." → Select "Sort by Month Number" to sort the months in chronological order.
- Add Week and Date field to the X Axis to enable Data drilling. Setup zoom slider to view drilled data better.
