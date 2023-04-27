# SQL

This SQL query selects the category, subcategory, total sales, and subcategory rank for each subcategor.
The total sales are rounded to 2 decimal places using the ROUND function. 
The subcategory rank is calculated using the RANK function, which assigns a rank to each subcategory within its respective category based on its total sales.

The subquery selects the category, subcategory, total sales, and subcategory rank for each subcategory, and the outer query filters the results to only 
include subcategories with a rank of 1, 2, or 3. The results are sorted first by category in ascending order and then by subcategory rank.


SELECT category, subcategory, TotalSales, sub_category_rank
FROM (
  SELECT s.category, s.subcategory, ROUND(SUM(s.sales) ,2) AS TotalSales, 
	RANK() OVER (PARTITION BY s.category ORDER BY SUM(s.sales) DESC) AS sub_category_rank 
	FROM [Superstoree].[dbo].[Order] s
	GROUP BY s.category, s.subcategory 
) subquery
WHERE sub_category_rank <= 3
ORDER BY category, sub_category_rank;
