# SQL

This SQL query selects the year, product name, and total sales for each product.
The results are filtered to only include the top three best-selling products for each year between 2013 and 2015. 
The total sales are calculated using the SUM function and are grouped by year and product name. 
The ROW_NUMBER function is used to assign a sales rank to each product within each year.

The subquery (s) selects the year, product name, total sales, and sales rank for each product. 
Query filters the results to only include products with a sales ranks of 1, 2, or 3. 
The results are sorted first by year in ascending order and then by total sales in descending order.



SELECT 
    s.Year, s.product_name, s.total_sales
FROM 
    (
        SELECT YEAR(order_date) AS Year, product_name, SUM(Sales) AS total_sales, 
        ROW_NUMBER() OVER(PARTITION BY YEAR(order_date) ORDER BY SUM(Sales) DESC) AS sales_rank
        FROM [Superstoree].[dbo].[Order]
        WHERE YEAR(order_date) IN (2013, 2014, 2015)
        GROUP BY YEAR(order_date), product_name 
    ) s
WHERE s.sales_rank <= 3
ORDER BY s.Year, s.total_sales DESC;
