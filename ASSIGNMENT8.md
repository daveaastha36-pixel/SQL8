1.
Create two tables in your SQL database: Users (user_id, username, city) and Orders (order_id, user_id, product, amount). Insert at least 3 users and 5 orders, making sure some users have no orders.

***SOLUTION***
-- Users table
CREATE TABLE Users (
    user_id INT PRIMARY KEY,
    username VARCHAR(50),
    city VARCHAR(50)
);

-- Orders table
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    product VARCHAR(100),
    amount DECIMAL(10,2)
);

-- Insert users
INSERT INTO Users (user_id, username, city) VALUES
(1, 'Amit', 'Ahmedabad'),
(2, 'Priya', 'Surat'),
(3, 'Rahul', 'Vadodara');

-- Insert orders
INSERT INTO Orders (order_id, user_id, product, amount) VALUES
(101, 1, 'Pizza', 350.00),
(102, 1, 'Burger', 200.00),
(103, 2, 'Pasta', 280.00),
(104, 2, 'Sandwich', 150.00),
(105, 4, 'Cold Coffee', 120.00);

2.
Write an SQL query using INNER JOIN to list all usernames and their ordered products, showing only users who have placed at least one order.

***SOLUTION***
SELECT u.username,
       o.product
FROM Users u
INNER JOIN Orders o
ON u.user_id = o.user_id;


3.
Write an SQL query using LEFT JOIN to display all usernames along with their ordered products. For users who haven't placed any orders, show NULL for the product.

***SOLUTION***
SELECT u.username,
       o.product
FROM Users u
LEFT JOIN Orders o
ON u.user_id = o.user_id;

4.
Write an SQL query using RIGHT JOIN to show all orders and the corresponding username for each order. If an order has a user_id that doesn't exist in the Users table, display NULL for the username.<br><br><em><strong>Hint:</strong> Try deleting one user and keeping their order to test this case.</em>

***SOLUTION***
SELECT u.username,
       o.order_id,
       o.product,
       o.amount
FROM Users u
RIGHT JOIN Orders o
ON u.user_id = o.user_id;

5.
Suppose you want to analyze food delivery data like Zomato. Create a CustomerSegments table (segment_id, segment_name), and link it to Users with a foreign key. Write an SQL query to show each username, their segment name, and total order amount (use JOINs as needed).

***SOLUTION***
CREATE TABLE CustomerSegments (
    segment_id INT PRIMARY KEY,
    segment_name VARCHAR(50)
);

ALTER TABLE Users
ADD segment_id INT,
ADD CONSTRAINT fk_segment
FOREIGN KEY (segment_id)
REFERENCES CustomerSegments(segment_id);

-- Sample segments
INSERT INTO CustomerSegments VALUES
(1, 'Regular'),
(2, 'Premium'),
(3, 'VIP');

-- Assign segments to users
UPDATE Users SET segment_id = 1 WHERE user_id = 1;
UPDATE Users SET segment_id = 2 WHERE user_id = 2;
UPDATE Users SET segment_id = 3 WHERE user_id = 3;


