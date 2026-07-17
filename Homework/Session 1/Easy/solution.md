SELECT i.product_id, i.product_name
FROM inventory_current_stock i
LEFT JOIN sales_transactions s
    ON i.product_id = s.product_id
WHERE s.product_id IS NULL;