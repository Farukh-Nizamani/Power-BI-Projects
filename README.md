# Power-BI-Reports
Hi, This is the repository for all of my power bi reports
and this README.md is a detailed documentation of them


I document my Power-BI-Reports in the order:

-- About the Report

-- Data Source 

-- The use of SQL

-- Power BI features Used

-- Report Navigation

-- Choice/Purpose of Visuals

-- Visuals I decided to exclude

-- Limitations



<br>
<br>
<br>


**<h1>Sales VS Target Performance Report</h1>**
**About The Report:**

SIDE-NOTE: if want to know how to navigate this power bi report, scroll down to the **Report Navigation** paragraph

It consists of 4 pages in total (excluding tool-tip pages) out of which 2 pages will only be shown to the end-user when they drill-through the charts on the first and second page:
1) Summary
2) Sales Analysis
3) Product Performance (hidden)
4) Regional Performance (hidden)




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
I used the MySQL DBMS to clean, deduplicate, standardize, normalize and structure the dataset into a Star Schema with two Fact Tables (Sales and Target table) and 5 denormalized dim tables, having linked them to both the Fact tables using foreign keys. I also used Recursive CTEs to fill in the missing dates in the Date Table, and used CASE statements to change the data of Target Table so its not just a duplicate of Sales Table.


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
**Report Navitation:**<br>
To access the Product or Regional Performance pages, right-click a specific item on the Summary or Sales Analysis pages and select the drill-through option. This automatically filters the destination page by your selected product or region


<br>
Here's a little demonstration, let's say i want to know more detail about the country 'finland', i will right-click on it and select drill-through option


<img width="959" height="538" alt="image" src="https://github.com/user-attachments/assets/f0701a3b-8d0c-4797-8747-c96c52221394" />
<br>
<img width="962" height="544" alt="image" src="https://github.com/user-attachments/assets/331e9453-69c2-457a-8d06-43f1950c22a1" />
<br>
the destination page (we drill-through a country so its regional performance page) is now filtered by the country Finland










