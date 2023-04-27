# SQL

Simple query showing states ordered by total sales from the highest to the lowest

SELECT state, ROUND(SUM(sales), 2) AS total_sales
FROM [Superstoree].[dbo].[Order]
GROUP BY state
ORDER BY total_sales DESC;
