# SQL-Projects

## Table of Contents
1. [Objective](#objective)
2. [User Story](#user-story)
3. [Data Source](#data-source)
4. [Stages](#stages)
5. [Design](#design)
    - [Dashboard components required](#dashboard-components-required)
    - [Mockup](#mockup)
    - [Tools Used](#tools-used)
6. [Development](#development)
    - [Data Exploration Steps](#data-exploration-steps)
        - [Data exploration notes](#data-exploration-notes)
    - [Data Cleaning](#data-cleaning)
    - [Transform the Data](#transform-the-data)
7. [Testing](#testing)
    - [Row Count Check](#row-count-check)
    - [Column Count Check](#column-count-check)
    - [Duplicate Check](#duplicate-check)
    - [Missing Values Check](#missing-values-check)
8. [Analysis](#analysis)
    - [Sales Analysis](#sales-analysis)

## Objective
The objective of this project is to analyze customer and order data to identify trends, patterns, and insights that can inform business decisions. This includes examining customer demographics, purchase behaviors, order frequencies, and product preferences to improve customer satisfaction, optimize inventory management, and enhance overall business performance.


## User Story
As a business analyst, I want to analyze customer and order data to gain insights into purchasing patterns and customer behavior. This will allow me to identify trends, optimize inventory, and improve marketing strategies, ultimately enhancing customer satisfaction and increasing sales.

## Data Source
### Description
The data for this project is sourced from the BIT_DB SQLite database. It includes several tables containing sales data across different months and customer information. The key tables used in this analysis are:
- `AprSales`: Contains columns such as `orderID`, `Product`, `Quantity`, `price`, `orderdate`, and `location`.
- `customers`: Contains columns such as `order_id` and `acctnum`.
- `FebSales`, `JanSales`, `MarSales`, `MaySales`: Each of these tables contains similar columns to `AprSales`.

#In this SQL, I'm querying a database with multiple tables in it to quantify statistics about customer and order data. 

#1. How many orders were placed in January? 
SELECT COUNT(orderid)
FROM BIT_DB.JanSales
WHERE length(orderid) = 6 
AND orderid <> 'Order ID'

#2. How many of those orders were for an iPhone? 
SELECT COUNT(orderid)
FROM BIT_DB.JanSales
WHERE Product='iPhone'
AND length(orderid) = 6 
AND orderid <> 'Order ID'

#3. Select the customer account numbers for all the orders that were placed in February. 
SELECT distinct acctnum
FROM BIT_DB.customers cust

INNER JOIN BIT_DB.FebSales Feb
ON cust.order_id=FEB.orderid
WHERE length(orderid) = 6 
AND orderid <> 'Order ID'

#4. Which product was the cheapest one sold in January, and what was the price? 
SELECT distinct Product, price
FROM BIT_DB.JanSales
WHERE  price in (SELECT min(price) FROM BIT_DB.JanSales)
#OR 
SELECT distinct product, price FROM BIT_DB.JanSales 
ORDER BY price ASC LIMIT 1

#5. What is the total revenue for each product sold in January?
SELECT sum(quantity)*price as revenue
,product
FROM BIT_DB.JanSales
GROUP BY product

#6. Which products were sold in February at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue?
select 
sum(Quantity), 
product, 
sum(quantity)*price as revenue
FROM BIT_DB.FebSales 
WHERE location = '548 Lincoln St, Seattle, WA 98101'
GROUP BY product

#7. How many customers ordered more than 2 products at a time, and what was the average amount spent for those customers? 
select 
count(distinct cust.acctnum), 
avg(quantity*price)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid=cust.order_id
WHERE Feb.Quantity>2
AND length(orderid) = 6 
AND orderid <> 'Order ID'

#8. List all the products sold in Los Angeles in February, and include how many of each were sold.
#Note: 'like' searches the column you give it for the values you type in after like. '%' tells the SQL code that you are searching for a value that can match anything.
SELECT Product, SUM(quantity)
FROM BIT_DB.FebSales
WHERE location like '%Los Angeles%'
GROUP BY Product;

#9. Which locations in New York received at least 3 orders in January, and how many orders did they each receive?
SELECT distinct location, count(orderID)
FROM BIT_DB.JanSales
WHERE location LIKE '%NY%'
AND length(orderid) = 6 
AND orderid <> 'Order ID'
GROUP BY location
HAVING count(orderID)>2;

#10. How many of each type of headphone was sold in February?
SELECT sum(Quantity) as quantity,
Product
FROM BIT_DB.FebSales 
WHERE Product like '%Headphones%'
GROUP BY Product;

#11. What was the average amount spent per account in February?
SELECT avg(quantity*price)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid=cust.order_id
WHERE length(orderid) = 6 
AND orderid <> 'Order ID';

#12. What was the average quantity of products purchased per account in February? 
SELECT SUM(quantity)/count(cust.acctnum)
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid=cust.order_id
WHERE length(orderid) = 6 
AND orderid <> 'Order ID';

#13. Which product brought in the most revenue in January and how much revenue did it bring in total? 
SELECT product, 
sum(quantity*price)
FROM BIT_DB.JanSales 
GROUP BY product
ORDER BY sum(quantity*price) desc 
LIMIT 1;
# In this question, I'm using GROUP BY product. 
# The price of each individual product doesn't change. 
