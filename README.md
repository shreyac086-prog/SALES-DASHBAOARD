 Sales Analytics Dashboard — Excel + SQL + Power BI

## Project Overview

This project presents an end-to-end Sales Analytics Dashboard built using Excel, SQL, and Power BI.
The dashboard provides a comprehensive and interactive view of key business metrics, including:

Total Sales
Total Cost
Profit
ROI
Units Sold
Category, Region & Channel Performance
Customer Ratings
Inventory Status

The goal is to support data-driven decision-making through a clean, modern, and dynamic reporting system.

## Dashboard Preview 
[click here to view dashboard image](https://raw.githubusercontent.com/shreyac086-prog/SALES-DASHBAOARD/refs/heads/main/image/SALES%20DB.jpg)


Files Included

SALES DASHBOARD.pbix — Power BI Dashboard
README.md — Documentation

## How to Use

Download the .pbix file
Open it in Power BI Desktop
Explore KPIs, trends, slicers, and interactive buttons

## Data Extraction

The raw dataset (Excel) included:

Product details
Sales transactions
Regions & channels
Inventory
Customer ratings

## Data Cleaning & SQL Transformation

SQL was used to clean, standardize, and merge multiple tables before loading into Power BI.

SQL tasks performed:
Created a Calendar table
merged multiple  tables using joins 
Removed duplicates
sorting and filtering 
removed null values, blank spaces etc
Ensured analysis-ready, high-quality data

SQL Snippets:

![SQL 1](https://github.com/user-attachments/assets/a7e5ef87-3f22-4ecb-b098-6d6d102a6701)


![SQL2](https://github.com/user-attachments/assets/88ef4ee2-df02-4bde-bc78-bd6db4a3431a)



##  Data Modeling (Power BI)

After cleaning in SQL, the refined dataset was imported into Power BI.
A single main fact table was prepared
Relationships established for seamless filtering
Ensured the model supported drill-downs, bookmarks, and navigation

##  DAX Calculations

The dashboard includes 20+ measures powering KPIs, YoY comparisons, dynamic ranges, and indicators.

![kpi ](https://github.com/user-attachments/assets/9fd4eb4b-d433-4c5f-be4c-90b8bc709618)


⚙️ Key DAX Examples:


3-Month Cost
cost 3 month =
CALCULATE([total cost],
    DATESINPERIOD(calender[cal_date], MAX(calender[cal_date]), -3, MONTH))

3-Month Cost Last Year
cost 3 month ly =
CALCULATE([total cost],
    SAMEPERIODLASTYEAR(
        DATESINPERIOD(calender[cal_date], MAX(calender[cal_date]), -3, MONTH)
    ))

Indicator Symbol
COST 3 indicator =
SWITCH(
    TRUE(),
    [cost 3 %] > 0, "▲ " & FORMAT([cost 3 %], "0%"),
    [cost 3 %] < 0, "▼ " & FORMAT([cost 3 %], "0%"),
    "▬ " & FORMAT([cost 3 %], "0%")
)

Indicator Color
cost 3 Indicator Color =
SWITCH(
    TRUE(),
    [cost 3 %] > 0, "#006400",
    [cost 3 %] < 0, "#8B0000",
    "#3A7CA5"
)


## Filters, Parameters & Interactivity

🔹 Top N Selector


![top n calculator](https://github.com/user-attachments/assets/ac002e5e-9d49-4a4a-935d-eb51b1b1ee92)


Allows users to view Top/Bottom Customers based on a dynamic numeric input.

DAX:

CONDITION =
VAR N = Parameter[Parameter Value]
VAR SelectedMode = SELECTEDVALUE('TOP/BOTTTOM'[TYPE])

VAR IsTop = SelectedMode = "TOP" && [CUSTOMER RANK TOP] <= N
VAR IsBottom = SelectedMode = "BOTTOM" && [CUSTOMER RANK BOTTOM] <= N

RETURN IF(IsTop || IsBottom, 1, 0)


🔹 Dynamic Period Filters



![filter panel ](https://github.com/user-attachments/assets/d170386b-eb51-41a6-b682-19ba52a1c8bc)


Buttons for:
3M
6M
9M
YTD
This Month
This Year

DAX:
Total Sales Selected =
VAR p = SELECTEDVALUE(PeriodSelector[Period])
RETURN
SWITCH(
    TRUE(),
    p = "this month", [price mtd],
    p = "this year", [PRICE YTD],
    p = "previous yr month", [price mtd],
    p = "3 months", [unit price 3 months],
    p = "6 months", [unit price 6 months],
    p = "9 months", [unit price 9 months],
    [tol unit price]
)
🔹 Metric Selector
Switches between:
Total Sales
Total Quantity measure

DAX:
METRIX PARAMETER = {
    ("tol unit price", NAMEOF('_measures UNIT'[tol unit price]), 0),
    ("total quantity", NAMEOF('_measures UNIT'[total quantity]), 1)
}

##🎨 UI/UX & Dashboard Design

Clean and modern theme
Custom PowerPoint-designed background
Button-based navigation
Pop-up filter panel
Donut charts, bar charts, KPI cards
Trend comparisons with YoY & MoM highlights
Inventory & customer feedback visuals

Background example:

<img width="1075" height="890" alt="bg" src="https://github.com/user-attachments/assets/b1078966-1ae9-4f98-965f-393d5e285443" />






