# timbercrest-sql-analysis
SQL project analyzing sales and product performance for TimberCrest Furnishings


# 🪑 TimberCrest Furnishings SQL Sales Analysis

This SQL project analyzes the sales performance, product data, and customer trends for **TimberCrest Furnishings**, a U.S.-based company supplying office furniture, equipment, and maintenance products across multiple cities and states.

## 🧩 Business Context
TimberCrest aims to monitor performance across product categories, identify top-performing locations and customers, and improve inventory and sales strategies. With a growing product base and a wide range of clients, data insights are essential for making informed, strategic decisions.

## 🎯 Project Objectives
- Understand which products and categories generate the highest sales.
- Analyze customer property locations and order behavior.
- Identify underperforming categories and potential growth areas.
- Examine year-over-year order trends and pricing insights.

## 🛠️ SQL Techniques Used
- Data retrieval and exploration using `SELECT`, `DISTINCT`, `WHERE`, `ORDER BY`, and `LIMIT`.
- Aggregation with `SUM()`, `AVG()`, `COUNT()`, and `GROUP BY`.
- String pattern matching with `LIKE` and `ILIKE`.
- Date functions using `EXTRACT(YEAR FROM OrderDate)` for time-based analysis.
- Filtering and conditional logic using `IN`.

## 📈 Key Insights Uncovered
- Identified the cities and states with active TimberCrest properties.
- Analyzed product diversity across categories and their pricing structure.
- Revealed the most and least expensive products.
- Tracked total product quantities ordered across years and properties.
- Flagged underperforming product categories and high-demand items.

## 📂 Files
- `timbercrest_sales_analysis.sql` — All SQL queries used for this project.

## 🧠 Skills Demonstrated
- Data exploration and business-focused analysis
- SQL querying and reporting
- Sales performance monitoring
- Inventory and customer segmentation.


-- 1. Show all details about orders, products and properties.
SELECT *
FROM "orders";

SELECT *
FROM "products";

SELECT *
FROM "propertyinfo";

-- 2. In what Cities and States are TimberCrest Properties Located.
SELECT DISTINCT "PropertyCity", "PropertyState"
FROM propertyinfo;

-- 3. What are the different product categories TimberCrest has in store?
SELECT DISTINCT "ProductCategory"
FROM products;

-- 4. What are the numbers of products in each product category?
SELECT DISTINCT "ProductCategory", COUNT(*) AS "NumberOfProducts"
FROM products
GROUP BY "ProductCategory";

-- 5. What is the total quantity of products ordered?
SELECT SUM("Quantity") AS "TotalQuantityOrdered"
FROM orders;

-- 6. What are the five most expensive products?
SELECT "ProductName", "Price"
FROM products
ORDER BY "Price" DESC
LIMIT 5;

-- 7. What is the average price of products in each category?
SELECT DISTINCT "ProductCategory", AVG("Price") AS AveragePrice
FROM products
GROUP BY "ProductCategory"
ORDER BY AveragePrice DESC;

-- 8. What products have names starting with “T”?
SELECT "ProductName"
FROM products
WHERE "ProductName" LIKE 'T%';

-- 9. Lists all products with names containing paper.
SELECT "ProductName"
FROM products
WHERE "ProductName" ILIKE '%paper%';

-- 10. Extract the name and category of products whose prices are above $200
SELECT "ProductName", "ProductCategory", "Price"
FROM products
WHERE "Price" > 200;

-- 11. What is the total quantity of products ordered in 2015 and 2016 respectively?
SELECT EXTRACT(YEAR FROM "OrderDate") AS "Year", SUM("Quantity") AS "QuantityOrdered"
FROM orders
WHERE EXTRACT(YEAR FROM "OrderDate") IN (2015, 2016)
GROUP BY EXTRACT(YEAR FROM "OrderDate");

-- 12. Which orders were made by property 1, 10, and 20?
SELECT *
FROM orders
WHERE "PropertyID" IN (1, 10, 20);

-- 13. What is the least expensive product?
select "ProductName", "Price" from products
order by "Price" 
limit 5;

## 📌 Next Steps
This SQL analysis can be extended with Tableau or Power BI to build interactive dashboards for dynamic business insights.
