# Customer and Order Analytics

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

## Stages

1. **Data Acquisition**: 
   - Gather data from the BIT_DB SQLite database, including tables such as `AprSales`, `FebSales`, `JanSales`, `MarSales`, `MaySales`, and `customers`.

2. **Data Exploration**:
   - Inspect the data to understand its structure and content.
   - Identify key attributes and any potential data quality issues.

3. **Data Cleaning**:
   - Remove duplicates, handle missing values, and correct any inconsistencies in the data.
   - Ensure data types are appropriate for analysis.

4. **Data Transformation**:
   - Transform raw data into a suitable format for analysis.
   - Create new features if necessary to enhance analysis.

5. **Data Analysis**:
   - Perform SQL queries to analyze customer and order data.
   - Generate insights and identify trends, patterns, and anomalies.

6. **Visualization and Reporting**:
   - Visualize the results using charts and graphs to present findings clearly.
   - Compile a report summarizing the analysis and key insights.

7. **Conclusion and Recommendations**:
   - Summarize the key findings of the analysis.
   - Provide actionable recommendations based on the insights obtained.

## Design
### Dashboard Components Required
To effectively visualize and analyze the customer and order data, the following dashboard components are required:
- **Sales Overview**: Total sales, sales by month, and sales by product category.
- **Customer Demographics**: Breakdown of customers by age, gender, location, and other relevant demographics.
- **Order Details**: Number of orders, average order value, and order frequency.
- **Product Performance**: Sales performance of individual products, including top-selling and low-performing products.
- **Location Analysis**: Sales performance by location, highlighting high-performing and underperforming regions.

### Mockup
Below is a mockup of the Tableau dashboard that was created to visualize the data insights. (Here you will insert images of your Tableau dashboard mockups)

### Tools Used
The following tools were used in the design and development of this project:
- **SQLite**: For data storage and querying.
- **Tableau**: For data visualization and dashboard creation.
- **Excel**: For additional data manipulation and analysis.

## Development
### Data Exploration Steps
- **Inspect Data**: Understand the structure, content, and types of data available in the BIT_DB SQLite database.
- **Identify Key Attributes**: Determine important attributes for analysis such as `orderID`, `Product`, `Quantity`, `price`, `orderdate`, and `location`.

### Data Exploration Notes
- Data contains customer orders, product details, sales dates, and sales locations.
- Initial exploration reveals missing values and potential duplicates that need to be addressed.

### Data Cleaning
1. **Remove Duplicates**: Ensure each order is unique.
   - Utilize Excel’s Remove Duplicates feature to eliminate duplicate entries based on the `order_id` column.
2. **Handle Missing Values**: Fill or exclude missing values where necessary.
   - **Filter Out Blank Rows**:
     - Select the data range and apply filters.
     - Click on the filter drop-down arrow in the `order_id` column header.
     - Uncheck (Blanks) to filter out blank rows.
     - Select and delete the filtered rows.
   - **Filter Out Null Values**:
     - Click on the filter drop-down arrow in the `order_id` column header.
     - Uncheck (null) to filter out null values.
     - Select and delete the filtered rows.
   - **Filter Out Specific Unwanted Values ("Order ID")**:
     - Click on the filter drop-down arrow in the `order_id` column header.
     - Uncheck "Order ID" to exclude these placeholder values.
     - Select and delete the filtered rows.
3. **Correct Data Types**: Ensure all data types are appropriate for the analysis (e.g., dates are in datetime format).
   - Use Excel’s Format Cells feature to set the appropriate data types for each column (e.g., setting `acctnum` to Number).
   - Example of errors found in data in photo below:
     
  ![Example of Data](https://github.com/josephsackett/SQL-Projects/blob/main/Images/Dataerror.png?raw=true)
     

### Transform the Data
1. **Create New Features**: Derived new attributes such as total revenue per product (`quantity * price`).
   - Add a column to calculate `total_revenue` by multiplying `quantity` and `price`.
2. **Aggregate Data**: Summarize data to higher levels (e.g., total sales per month, sales by product category).
   - Used pivot tables and summary functions in Excel to calculate total sales per month or by product category.

## Testing
### Row Count Check
- Verify that the number of rows in the dataset matches the expected count after data cleaning.
- Use SQL or Excel functions to count the rows and ensure no data loss during cleaning and transformation.

  ![Example of Data](https://github.com/josephsackett/SQL-Projects/blob/main/SQLrowcount.png?raw=true)

### Column Count Check
- Ensure all necessary columns are present in the dataset.
- Check for any unexpected or missing columns after data processing.
- To perform a column count check in SQL, you generally want to ensure that all required columns exist and are correctly named in 
  your tables. Here’s an alternative SQL approach for verifying columns using SQL queries:

  ![Example of Data](https://github.com/josephsackett/SQL-Projects/blob/main/Images/SQLcolumncheck.png?raw=true)

### Duplicate Check
- Confirm that all duplicate entries have been removed.
- Use SQL queries or Excel functions to identify any remaining duplicates.

### Missing Values Check
- Check for any remaining missing values in critical columns.
- Ensure that all missing values have been handled appropriately during the data cleaning process.

## Analysis
### Sales Analysis

#1. How many orders were placed in January? 

 ![Example of Data](https://github.com/josephsackett/Customer-and-Order-Analystics/blob/main/Images/TotalJanSales.png?raw=true)

#2. How many of those orders were for an iPhone? 

 ![Example of Data](https://github.com/josephsackett/Customer-and-Order-Analystics/blob/main/Images/JanIphoneorders.png?raw=true)

#3. Select the customer account numbers for all the orders that were placed in February. 

 ![Example of Data](https://github.com/josephsackett/Customer-and-Order-Analystics/blob/main/Images/AcctOrderFeb.png?raw=true)

#4. Which product was the cheapest one sold in January, and what was the price?
 - Showed two ways to tackle this question.

![Example of Data](https://github.com/josephsackett/Customer-and-Order-Analystics/blob/main/Images/CheapestItemJan.png?raw=true)

#5. What is the total revenue for each product sold in January?
 - Revenue can be calculated using the number of products sold and the price of the products

![Example of Data](https://github.com/josephsackett/Customer-and-Order-Analystics/blob/main/Images/TotalRevEachPrJan.png?raw=true)

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
