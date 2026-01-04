# Power-BI-Reports
Hi, This is the repository for all of my power bi reports
and this README.md is a detailed documentation of them


I document my Power-BI-Reports in the order:

-- About the Report

-- Data Source 

-- The use of SQL

-- List of Power BI features Used

-- Report Navigation

-- Purpose of Visuals

-- Visuals I decided to exclude

-- Limitations



<br>
<br>
<br>


**<h1>Sales VS Target Performance Report</h1>**
**About The Report:**

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
after i touched it:











