SELECT
CASE
    WHEN price > 18 THEN 'High'
    WHEN price BETWEEN 10 AND 18 THEN 'Medium'
    WHEN price < 10 THEN 'Low'
    ELSE 'NA'
    END AS Pay_Category,
COUNT(*) as Dish_count
FROM Orders
GROUP BY 1;

