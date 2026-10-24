CREATE TABLE food (
    f_id INT PRIMARY KEY,
    f_name VARCHAR(100) NOT NULL,
    f_cost INT NOT NULL,
    f_type VARCHAR(50) NOT NULL
);

INSERT INTO food (f_id, f_name, f_cost, f_type) VALUES
(1, 'Sushi', 20, 'Japanese'),
(2, 'Tandoori Chicken', 15, 'Indian'),
(3, 'Beef Stroganoff', 18, 'Russian'),
(4, 'Paella', 25, 'Spanish'),
(5, 'Moussaka', 16, 'Greek'),
(6, 'Plain Rice', 1, 'Indian'),
(7, 'Bread', 1, 'Bakery'),
(8, 'Soup', 1, 'Continental'),
(9, 'Salad', 1, 'Healthy'),
(10, 'Tea', 1, 'Beverage');

SELECT f_name, f_cost, f_type
FROM food
WHERE f_cost > (
    SELECT AVG(f_cost)
    FROM food
)
ORDER BY f_id;