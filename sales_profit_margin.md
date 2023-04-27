# SQL

This SQL query selects the year, total sales, total profit, and margin percentage for each year.
The YEAR function extracts the year from the order date column. The total sales and total profit are rounded to 2 decimal places using the ROUND function. 
The margin percentage is calculated by dividing the total profit by the total sales, multiplying by 100, and concatenating the percentage symbol using the 
CONCAT function.

The results are grouped by the year using the GROUP BY clause and are sorted in ascending order by the year using the ORDER BY clause.


SELECT YEAR(order_date) AS year,
       ROUND(SUM(sales), 2) AS total_sales,
       ROUND(SUM(profit), 2) AS total_profit,
       CONCAT(ROUND(SUM(profit) / SUM(sales) * 100, 2), '%') AS margin_percentage
FROM [Superstoree].[dbo].[Order]
GROUP BY YEAR(order_date)
ORDER BY YEAR(order_date) ASC;
