# SQL


This SQL query selects the customer ID and the total sales for each customer from the "Order" table in the "Superstoree" database.
Rounded to 2 decimals, having sum of the sales over 10000


SELECT customer_id, ROUND(SUM(sales), 2) AS total_sales
FROM [Superstoree].[dbo].[Order]
GROUP BY customer_id
HAVING SUM(sales) > 10000
ORDER BY total_sales DESC;
