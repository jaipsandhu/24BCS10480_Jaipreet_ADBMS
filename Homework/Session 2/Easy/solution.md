WITH ranked_customers AS (
    SELECT customer_id,
           total_purchase_value,
           DENSE_RANK() OVER (ORDER BY total_purchase_value DESC) AS rank
    FROM customer_purchase
)
SELECT customer_id, total_purchase_value, rank
FROM ranked_customers
WHERE rank <= 5;