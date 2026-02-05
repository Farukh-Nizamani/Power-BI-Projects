This repository is for for my first Power BI report called "Sales vs Target Performance Tracker"
and this README.md is a detailed documentation of it.

<br>

**<h1>Sales VS Target Performance Report</h1>**



Sales vs Targt Performance Report's documntation is split into the following sections:

-- About the Report

-- Data Source 

-- The use of SQL

-- Power BI features Used

-- Report Navigation

-- Visuals I decided to exclude

-- Limitations
<br>
<br>


**About The Report:**

IMPORTANT NOTE: I have mostly focused on the simplicity, usability, and utility of the report instead of its appereance.


It consists of 4 pages in total (excluding tool-tip pages) out of which 2 pages will only be shown to the end-user when they drill-through the charts on the first and second page:
1) Summary
2) Sales Analysis
3) Product Performance (hidden)
4) Regional Performance (hidden)
<br>



<br>
Summary Page:
<br>

<img width="872" height="487" alt="image" src="https://github.com/user-attachments/assets/f056653b-816c-4bef-a6db-d7d96edcbbe8" />




<br>
Sales Analysis Page:
<br>

<img width="867" height="485" alt="image" src="https://github.com/user-attachments/assets/cf2fffe3-c905-4913-8f5a-98564084f091" />




<br>
Product Performance Page (hidden):

<img width="870" height="488" alt="image" src="https://github.com/user-attachments/assets/cf769584-7a07-4a97-bfd6-728f14358f73" />




<br>
Regional Performance Page (hidden):

<img width="870" height="491" alt="image" src="https://github.com/user-attachments/assets/c685a56f-32e7-4b85-83c2-23efe2763ffe" />

<br>
<br>
Tooltip Pages:
<br>
tooltip page for main page:
<br>
<img width="647" height="480" alt="image" src="https://github.com/user-attachments/assets/5b17a7b1-a949-4712-bca9-a8f0c6ad7032" />




<br>
tooltip page date related visuals:
<br>
<img width="649" height="483" alt="image" src="https://github.com/user-attachments/assets/d919c9b9-1558-4d2f-bb87-6536d0fca203" />






<br>
Tooltip page for drill-through (hidden) pages:
<br>
<img width="648" height="483" alt="image" src="https://github.com/user-attachments/assets/e3f101e9-3c86-4d13-8a16-332d65dcf56a" />
<br>
<br>
Tooltips is the pop-up info which appears when you hover over a visual, and tooltip pages are the pages of a report that act as tooltips.


<br>
<br>
<br>


**Data Source:** <br>
I downloaded the Sales Dataset from Kaggle and here's the link of it:<br>
https://www.kaggle.com/datasets/kyanyoga/sample-sales-data?resource=download




<br>
<br>
<br>

**The use of SQL:**<br>
I used the MySQL DBMS to transform and design the dataset into a Star Schema having two Fact Tables (Sales and Target table) and 5 denormalized dim tables, linking both of them to the Fact tables using foreign keys. while data transformation I used Recursive CTEs to fill in the missing dates in the Date Table, and CASE statements to change the data of Target Table so its not just a duplicate of Sales Table.


dataset only consisted of a single table with column names before i worked on it:

ORDERNUMBER

QUANTITYORDERED

PRICEEACH

ORDERLINENUMBER

SALES

ORDERDATE

STATUS

QTR_ID

MONTH_ID

YEAR_ID

PRODUCTLINE

MSRP

PRODUCTCODE

CUSTOMERNAME

CITY

STATE

POSTALCODE

COUNTRY

TERRITORY

CONTACTLASTNAME

CONTACTFIRSTNAME

DEALSIZE

<br>
<img width="1348" height="487" alt="image" src="https://github.com/user-attachments/assets/36a3b56d-3753-4555-aa1a-3343cccaf023" />

<br>
<img width="1007" height="495" alt="image" src="https://github.com/user-attachments/assets/d4b83a31-d670-4b7e-8990-d469dd71d3b9" />

<br>
<br>
<br>

Sample of the queries i wrote
<br>
Since my dataset contained no columns or table for target_sales or target_table, i had to created a copy of sales_table as target_table, change a couple column names then write the following query and many others similar queries to modify the columns planned_quantity, target_amount and unit_price
```sql
  UPDATE TARGET_TABLE T
  JOIN LOCATION_TABLE L ON T.LOCATION_ID = L.LOCATION_ID
  JOIN DATE_TABLE D ON T.DATE_ID = D.DATE_ID
  SET
      T.PLANNED_QUANTITY = CASE
          WHEN D.MONTH_ID BETWEEN 1 AND 3 THEN T.PLANNED_QUANTITY + 13
          WHEN D.MONTH_ID BETWEEN 4 AND 8 THEN T.PLANNED_QUANTITY + 20
          WHEN D.MONTH_ID BETWEEN 9 AND 12 THEN T.PLANNED_QUANTITY + 27
      END
  WHERE T.PLANNED IS NOT NULL
  AND (
          L.LOCATION_ID BETWEEN 7 AND 21
          OR L.LOCATION_ID BETWEEN 57 AND 74
  );
```
<br>
<br>

Recursive Common Table Expression to update my date_table to be continuous, making it compatible with Power BI's time intelligence functions
```sql
    INSERT INTO DATE_TABLE (ORDER_DATE)
    WITH RECURSIVE DATE_SERIES AS (
      SELECT
          MIN(ORDER_DATE) AS MIN_DATE,
          MAX(ORDER_DATE) AS MAX_DATE
      FROM
          DATE_TABLE_BACKUP

      UNION ALL

      SELECT
        MIN_DATE + INTERVAL 1 DAY,
        MAX_DATE
      FROM
          DATE_SERIES
      WHERE
          MIN_DATE + INTERVAL 1 DAY <= MAX_DATE
)

SELECT
  MIN_DATE
FROM
  DATE_SERIES;

```
<br>
<br>






<br>
<br>
dataset after i cleaned, deduplicated, standardized, normalized and structured it into a Star Schema:
<br>

<br>
SALES_TABLE
<br>
<img width="255" height="213" alt="image" src="https://github.com/user-attachments/assets/e3deea59-415c-4cfa-b20b-8a475661bce5" /><br>
<img width="859" height="310" alt="image" src="https://github.com/user-attachments/assets/e86f3eb3-2ce1-4e65-b6fc-277aef2b30d5" />
<br>


<br>


<br>
TARGET_TABLE
<br>
<img width="278" height="220" alt="image" src="https://github.com/user-attachments/assets/8b6540ca-75ea-44cb-9fb2-fd5c29c2b044" /><br>
<img width="816" height="331" alt="image" src="https://github.com/user-attachments/assets/4a01738c-71a5-416f-b390-d0ca9c9914f9" />
<br>



<br>



<br>
CUSTOMER_TABLE
<br>
<img width="275" height="129" alt="image" src="https://github.com/user-attachments/assets/9545496e-1597-4e98-9579-b4126178a2e7" /><br>
<img width="299" height="311" alt="image" src="https://github.com/user-attachments/assets/e037e8e6-251b-44b7-8251-e8643197c461" />
<br>

<br>

<br>
DATE_TABLE
<br>
<img width="257" height="200" alt="image" src="https://github.com/user-attachments/assets/8ec48da3-caf7-43b0-badc-271a4c1bbd08" /><br>
<img width="507" height="332" alt="image" src="https://github.com/user-attachments/assets/fd2c8bdf-0395-4dd2-b17d-e3b38495f1fc" />
<br>


<br>


<br>
LOCATION_TABLE
<br>
<img width="256" height="289" alt="image" src="https://github.com/user-attachments/assets/d0a732bf-5619-4ca6-9c4a-f6ca97a9e0ae" /><br>
<img width="344" height="313" alt="image" src="https://github.com/user-attachments/assets/127a00be-6f46-4651-a0d6-f491de7a7e05" />
<br>

<br>

<br>
ORDER_TABLE
<br>
<img width="266" height="227" alt="image" src="https://github.com/user-attachments/assets/af6e9674-35bf-4f4a-bd68-2765b63bea07" /><br>
<img width="600" height="328" alt="image" src="https://github.com/user-attachments/assets/0056fb31-e5c1-4ef3-9836-894abbc931ae" />
<br>


<br>


<br>
PRODUCT_TABLE
<br>
<img width="279" height="209" alt="image" src="https://github.com/user-attachments/assets/e141426c-a421-4b80-83a9-ea7e6039f76c" /><br>
<img width="241" height="143" alt="image" src="https://github.com/user-attachments/assets/a6505f93-1913-4ca4-a152-c0ad6037d58a" />
<br>



<br>
<br>


Model view of star schema of my tables in power bi
<img width="977" height="504" alt="image" src="https://github.com/user-attachments/assets/ce2a9af4-db34-4dbd-87ac-a8e0d56880e5" />
<br>


<br>
<br>
<br>


**Power BI Features and Measures Used:**
<br>
-- Navigation: Drill-Throughs and Drill-Downs for granular Data Exploration, and a navigation bar to move between pages


-- Guidance: Custom Tooltip pages and Help-Tooltips for on-hover insights


-- Interactivity: Slicers and Field Parameters for dynamic axis/dimension switching 


-- Visual Polish: Conditional Formatting, Dynamic Titles, Dynamic Tooltip pages, and Dynamic Cards that change based on user selection so that users always see the appropriate data


-- Scenario Analysis: "What-If" parameters to simulate different business outcomes


-- Data Structure: Utilization of both Implicit and Explicit Hierarchies to support drill-downs


-- Customization: Integration of Bullect Chart Visuals to meet specific reporting need






<br>
<br>
<br>



**Report Navigation:**<br>
You can drill-down on almost all the visuals

<br>
To access the Product or Regional Performance pages, right-click a specific Product or Country on the Summary or Sales Analysis, hover over the drill-through option and then select Regional Performance/Product Performance. This automatically filters the destination page by your selected product or region
<br>

<br>
Here's a little demonstration, let's say i want to know more detail about the country 'finland', i will right-click on it and select drill-through option
<br>
<img width="959" height="538" alt="image" src="https://github.com/user-attachments/assets/f0701a3b-8d0c-4797-8747-c96c52221394" />
<br>
<img width="962" height="544" alt="image" src="https://github.com/user-attachments/assets/331e9453-69c2-457a-8d06-43f1950c22a1" />
<br>
the destination page (we drill-through a country so its regional performance page) is now filtered by the country Finland

<br>
<br>
<br>

On the matrix visuals, the intensity of the blue shading represents revenue, darker blue indicates higher earnings. Note that a darker shade does not necessarily mean a target was met. performance against targets is specifically indicated by the Green-Upward and Red-Downward arrows. Green-Upward arrow means we have met the target and Red-Downward arrow means we have not



<br>
<br>
<br>


**Visuals I decided to exclude:** <br>
Accelaraion Variance % Waterfall Chart -- i had created this visual on sales analysis page but soon realized it answers the questions like "how much % did our business's growth accelerated over X-amount of time" and that information would almost be of no use for most end-user so i built Sales Variance WaterFall Chart instead, which undoubtly answers important questions the end-user would need to know the answer of, for example the questions "which product/country/month is how far off our target" and thus "how much more sales do we need to reach the target", "Which regions/products are dragging us down the most", "Which products are over-performing", "in which months do we over and under perform?"


<br>

Scatter Plot -- Had plotted a Scatter Plot on the Product Performance page to show whether its quantity or the sales amount that is driving our revenue, later I assumed the end-user must already know that usually quantity is driver of the revenue so i replaced it with a Bar Chart showing the sales and target of all countries for the filtered product which is pretty useful for informing the end-user which country is generating the most sales for a particular product

<br>

Heatmap -- I thought of building a Heatmap on the region Performance page showing (by color intensities) which countries has the most sales, it made my report page look classy and cluttered simultaneously. I eventually replaced it by a matrix after some contemplation, matrix provides more detail and yet looks simple 

<br>

Top N Filter -- Had implemented a drop-down slicer using a DAX measure which let you choose the N number of top countries/products/customers to show on the first page,
nearly at the end of report i realized "why only 5/10/15/20?, wouldn't it be better if i just show all of the countries/products/customers?" and ended up removing the Top N filter as well



<br>
<br>
<br>

**Limitations:** <br>
On the sales analysis page, the XoX Growth % trend line chart will only work if you select the same date granularity level in the drop-down called "Growth Parameter" placed in the top-left corner and the date buttons located in top-right corner of the sales analysis page. the date buttons placed in the top-right corner controls its X-axis while drop-down "Growth Paramter" controls its Y-axis.

if there's a mismatch in the axises' granularities, the XoX Growth % trend line visual will go blank to avoid showing misleading information




