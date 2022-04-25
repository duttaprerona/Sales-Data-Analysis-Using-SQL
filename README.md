# Sales-Data-Analysis-Using-SQL
The purpose of this project is to analyse sales data of Atliq hardware to gain meaningful insights. I have used MySQL to write the queries. I have used the **Sales** database which contains five columns namely customers,date,markets, products and transactions.

###### Checking all customer records
SELECT *
FROM sales.customers;

###### Checking the total number of customers
SELECT count(*)
FROM sales.customers;

###### Show transactions for Bengaluru market (market code for bengaluru is Mark006)
SELECT *
FROM sales.markets
WHERE markets_code= 'Mark006';

###### Finding distinct product codes that were sold in Bengaluru
SELECT distinct product_code 
FROM sales.transactions 
where market_code='Mark006';

###### Checking transactions where currency is US dollars
SELECT * from sales.transactions where currency="USD";

--------------------------------------------------------
###### Transactions for the year 2020 joined by date table
SELECT sales.transactions.*, sales.date.*
FROM sales.transactions INNER JOIN sales.date
ON sales.transactions.order_date = sales.date.date
WHERE year = '2020';
---------------------------------------------------------
###### Total Revenue for the year 2020
SELECT SUM(sales.transactions.sales_amount)
FROM sales.transactions 
INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date
WHERE year='2020' AND sales.transactions.currency= 'INR';

###### Total Revenue for the month of January and year 2020
SELECT SUM(sales.transactions.sales_amount)
FROM sales.transactions 
INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date
WHERE year='2020' AND month_name = 'January' AND sales.transactions.currency= 'INR';

###### Total Revenue for Bengaluru in year 2020
SELECT SUM(transactions.sales_amount) 
FROM sales.transactions 
INNER JOIN sales.date ON sales.transactions.order_date = sales.date.date 
WHERE sales.date.year=2020 and sales.transactions.market_code="Mark006";
