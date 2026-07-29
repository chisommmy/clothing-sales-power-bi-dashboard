# clothing-sales-power-bi-dashboard
Clothing sales performance dashboard (Power BI)

A Power BI dashboard built from a clothing sales dataset, covering data cleaning, DAX measures, and dashboard design. Built as a portfolio project to practice moving from a raw, messy spreadsheet to a decision ready dashboard.

## What's in this repo

Clothing_Sales.pbit, the Power BI template file. Opening it in Power BI Desktop will prompt you to load the source data, since a template stores the data model, Power Query steps, and DAX measures, not the raw rows themselves.

Clothing_Sales_PowerBI_Dashboard.pdf, a static export of the finished dashboard page.

## Business questions this dashboard answers
*Which product category and brand generate the highest total sales?*
*Do returning customers spend more than new customers, and rate the store differently?*
*How is the order base split across High, Medium, and Low sales categories?*
*How does total sales vary by season and gender?*
*What's the overall profit margin, and what does the average discount and store rating look like across the business?*

## Data cleaning summary

The source file had several data quality issues that had to be resolved in Power Query before any of this was possible:

Five columns (Selling_Price, Discount_Percentage, Stock_Availability, Customer_Age, Store_Rating) used the literal text "NIL" instead of blank cells to represent missing values, roughly 5 percent of rows in each column. These were converted to true nulls, then the affected rows were removed.

The Brand column had an encoding error causing "Levi's" to display as "Leviâ€™s," corrected with a find and replace step.

Four columns (Selling_Price, Cost_Price, Total_Sales, Purchase_Frequency) contained a small number of negative values that don't make business sense (a shirt can't sell for negative money). These were corrected with an absolute value transform.

All columns were re-typed correctly once the "NIL" placeholder was removed, since Power BI had defaulted them to text.

## Key DAX measures

Total Sales = SUM('Clothing Sales'[Total_Sales])

Total Profit = SUMX('Clothing Sales', ('Clothing Sales'[Selling_Price] - 'Clothing Sales'[Cost_Price]) * 'Clothing Sales'[Quantity_Sold])

Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)

Returning Customer Sales = CALCULATE([Total Sales], 'Clothing Sales'[Customer_Type] = "Returning")

New Customer Sales = CALCULATE([Total Sales], 'Clothing Sales'[Customer_Type] = "New")

## Key findings

Total sales came to 3.87 billion naira across 414,000 units sold, with an average discount of 25 percent and an average store rating of 3.99 out of 5.

Sales were remarkably even across product categories, brands, and customer segments (new customer sales and returning customer sales landed within about 25 million naira of each other, on a 3.87 billion naira base). Rather than force an insight out of that, the write up treats this as a signal about the nature of the dataset itself, since a real market would typically show more skew than this. That distinction, between a genuine business insight and a flat, evenly distributed dataset, is discussed further in the full case study.

## Tools used

Power Query for cleaning, Power BI Desktop for modeling, DAX, and visualization.

## About

Built by Somi (@somispen_). Background in technical writing and content marketing, currently building analytics skills through hands on projects like this one.
