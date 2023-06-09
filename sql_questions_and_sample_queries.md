Here's an example schema for creating the tables needed to run the SQL queries:

```
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50),
    city VARCHAR(50)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    fulfillment_date DATE,
    status VARCHAR(20),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE salespeople (
    salesperson_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE sales (
    sale_id INT PRIMARY KEY,
    salesperson_id INT,
    customer_id INT,
    product VARCHAR(50),
    revenue DECIMAL(10, 2),
    sales INT,
    date DATE,
    FOREIGN KEY (salesperson_id) REFERENCES salespeople(salesperson_id),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

```

Here's an example set of sample data that can be inserted into the tables:

```
INSERT INTO customers (customer_id, name, city)
VALUES
    (1, 'Alice', 'New York'),
    (2, 'Bob', 'San Francisco'),
    (3, 'Charlie', 'Chicago'),
    (4, 'Dave', 'Los Angeles'),
    (5, 'Eve', 'Boston');

INSERT INTO orders (order_id, customer_id, order_date, fulfillment_date, status)
VALUES
    (1, 1, '2022-03-01', '2022-03-05', 'fulfilled'),
    (2, 1, '2022-04-01', '2022-04-05', 'fulfilled'),
    (3, 2, '2022-05-01', '2022-05-05', 'fulfilled'),
    (4, 3, '2022-06-01', NULL, 'pending'),
    (5, 4, '2022-07-01', '2022-07-05', 'fulfilled'),
    (6, 5, '2022-08-01', NULL, 'pending'),
    (7, 2, '2022-09-01', '2022-09-05', 'fulfilled'),
    (8, 3, '2022-10-01', '2022-10-05', 'fulfilled'),
    (9, 4, '2022-11-01', '2022-11-05', 'fulfilled'),
    (10, 5, '2022-12-01', NULL, 'pending');

INSERT INTO salespeople (salesperson_id, name)
VALUES
    (1, 'Frank'),
    (2, 'Gina'),
    (3, 'Henry'),
    (4, 'Isabella'),
    (5, 'Jack');

INSERT INTO sales (sale_id, salesperson_id, customer_id, product, revenue, sales, date)
VALUES
    (1, 1, 1, 'Product A', 1000.00, 10, '2022-03-01'),
    (2, 1, 1, 'Product A', 1500.00, 15, '2022-04-01'),
    (3, 2, 2, 'Product B', 2000.00, 10, '2022-05-01'),
    (4, 3, 3, 'Product C', 3000.00, 5, '2022-06-01'),
    (5, 4, 4, 'Product D', 4000.00, 10, '2022-07-01'),
    (6, 5, 5, 'Product E', 5000.00, 5, '2022-08-01'),
    (7, 2, 2, 'Product B', 1000.00, 5, '2022-09-01'),
    (8, 3, 3, 'Product C', 2000.00, 10, '2022-10-01'),
    (9, 4, 4, 'Product D', 3000.00, 5, '2022-11-01'),
    (10, 5, 5, 'Product E', 4000.00, 10, '2022-12-01');

```

After creating the tables and inserting the sample data, the SQL queries can be run against the tables.

# SQL Questions for Data Engineering Interview

Here are 50 medium to hard SQL questions and example queries for each:

1. What is the total revenue generated by product X in the last quarter?

```
SELECT SUM(revenue)
FROM sales
WHERE product = 'X'
AND date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What was the highest revenue earned by a salesperson in the last year?

```
SELECT MAX(revenue)
FROM sales
WHERE date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the average revenue per sale in the last month?

```
SELECT AVG(revenue/sales)
FROM sales
WHERE date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. How many orders were placed in the last quarter?

```
SELECT COUNT(*)
FROM orders
WHERE date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What was the average time it took to fulfill an order in the last year?

```
SELECT AVG(DATEDIFF(fulfillment_date, order_date))
FROM orders
WHERE order_date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What percentage of customers have made a repeat purchase in the last year?

```
SELECT (COUNT(DISTINCT customer_id)
        / COUNT(DISTINCT CASE WHEN order_date BETWEEN '2022-01-01' AND '2022-12-31' THEN customer_id END))
        * 100
FROM orders;

```

1. What is the total value of sales made in the last month?

```
SELECT SUM(revenue)
FROM sales
WHERE date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. How many orders were placed by repeat customers in the last quarter?

```
SELECT COUNT(*)
FROM orders
WHERE customer_id IN (
        SELECT customer_id
        FROM orders
        WHERE order_date BETWEEN '2022-10-01' AND '2022-12-31'
        GROUP BY customer_id
        HAVING COUNT(DISTINCT order_id) > 1
    )
AND order_date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What was the total revenue earned from product X in the last year?

```
SELECT SUM(revenue)
FROM sales
WHERE product = 'X'
AND date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What was the most popular product sold in the last quarter?

```
SELECT product
FROM sales
WHERE date BETWEEN '2022-10-01' AND '2022-12-31'
GROUP BY product
ORDER BY COUNT(*) DESC
LIMIT 1;

```

1. What is the average order value for customers who have made a purchase in the last month?

```
SELECT AVG(revenue)
FROM sales
WHERE customer_id IN (
        SELECT DISTINCT customer_id
        FROM sales
        WHERE date BETWEEN '2023-03-01' AND '2023-03-31'
    );

```

1. How many orders were canceled in the last year?

```
SELECT COUNT(*)
FROM orders
WHERE status = 'canceled'
AND order_date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the total revenue earned by salesperson X in the last quarter?

```
SELECT SUM(revenue)
FROM sales
WHERE salesperson = 'X'
AND date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What is the average revenue per customer in the last month?

```
SELECT AVG(revenue)
FROM (
        SELECT customer_id, SUM(revenue) AS revenue
        FROM sales
        WHERE date BETWEEN '2023-03-01' AND '2023-03-31'
        GROUP BY customer_id
    ) AS customer_revenue;

```

1. What percentage of orders were placed by new customers in the last year?

```
SELECT (COUNT(DISTINCT CASE WHEN order_date BETWEEN '2022-01-01' AND '2022-12-31' THEN customer_id END)
        - COUNT(DISTINCT CASE WHEN order_date < '2022-01-01' THEN customer_id END))
        / COUNT(DISTINCT CASE WHEN order_date BETWEEN '2022-01-01' AND '2022-12-31' THEN customer_id END)
        * 100
FROM orders;

```

1. What was the highest revenue earned by a salesperson in the last quarter?

```
SELECT MAX(revenue)
FROM sales
WHERE date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. How many orders were placed by customers in city X in the last month?

```
SELECT COUNT(*)
FROM orders
WHERE customer_id IN (
        SELECT customer_id
        FROM customers
        WHERE city = 'X'
    )
AND order_date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. What was the average time it took to fulfill an order in the last month?

```
SELECT AVG(DATEDIFF(fulfillment_date, order_date))
FROM orders
WHERE order_date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. What is the total revenue earned from product X in the last quarter?

```
SELECT SUM(revenue)
FROM sales
WHERE product = 'X'
AND date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What is the average revenue per sale in the last year?

```
SELECT AVG(revenue/sales)
FROM sales
WHERE date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the total revenue earned from customers who made a purchase in the last month?

```
SELECT SUM(revenue)
FROM sales
WHERE customer_id IN (
        SELECT DISTINCT customer_id
        FROM sales
        WHERE date BETWEEN '2023-03-01' AND '2023-03-31'
    );

```

1. How many orders were placed by customers who have made a repeat purchase in the last quarter?

```
SELECT COUNT(*)
FROM orders
WHERE customer_id IN (
        SELECT customer_id
        FROM orders
        WHERE order_date BETWEEN '2022-10-01' AND '2022-12-31'
        GROUP BY customer_id
        HAVING COUNT(DISTINCT order_id) > 1
    )
AND order_date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What is the average order value for customers who live in city X?

```
SELECT AVG(revenue)
FROM sales
WHERE customer_id IN (
        SELECT customer_id
        FROM customers
        WHERE city = 'X'
    );

```

1. What is the total revenue earned from salesperson X in the last year?

```
SELECT SUM(revenue)
FROM sales
WHERE salesperson = 'X'
AND date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What was the most popular product sold in the last year?

```
SELECT product
FROM sales
WHERE date BETWEEN '2022-01-01' AND '2022-12-31'
GROUP BY product
ORDER BY COUNT(*) DESC
LIMIT 1;

```

1. How many orders were placed by new customers in the last quarter?

```
SELECT COUNT(DISTINCT CASE WHEN order_date BETWEEN '2022-10-01' AND '2022-12-31'
                            AND DATEDIFF(order_date, (SELECT MIN(order_date) FROM orders)) > 365
                        THEN customer_id END)
FROM orders;

```

1. What is the average revenue per customer in the last year?

```
SELECT AVG(revenue)
FROM (
        SELECT customer_id, SUM(revenue) AS revenue
        FROM sales
        WHERE date BETWEEN '2022-01-01' AND '2022-12-31'
        GROUP BY customer_id
    ) AS customer_revenue;

```

1. What percentage of customers have made a repeat purchase in the last month?

```
SELECT (COUNT(DISTINCT customer_id)
        / COUNT(DISTINCT CASE WHEN date BETWEEN '2023-03-01' AND '2023-03-31' THEN customer_id END))
        * 100
FROM sales;

```

1. What is the average time it took to fulfill an order in the last year?

```
SELECT AVG(DATEDIFF(fulfillment_date, order_date))
FROM orders
WHERE order_date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. How many orders were canceled in the last quarter?

```
SELECT COUNT(*)
FROM orders
WHERE status = 'canceled'
AND order_date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What is the total revenue earned from salesperson X in the last month?

```
SELECT SUM(revenue)
FROM sales
WHERE salesperson = 'X'
AND date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. What was the highest revenue earned by a salesperson in the last year?

```
SELECT MAX(revenue)
FROM sales
WHERE date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. How many orders were placed by customers in city X in the last quarter?

```
SELECT COUNT(*)
FROM orders
WHERE customer_id IN (
        SELECT customer_id
        FROM customers
        WHERE city = 'X'
    )
AND order_date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What was the average revenue per sale in the last month?

```
SELECT AVG(revenue/sales)
FROM sales
WHERE date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. What is the total revenue earned from customers who have made a repeat purchase in the last year?

```
SELECT SUM(revenue)
FROM sales
WHERE customer_id IN (
        SELECT customer_id
        FROM orders
        WHERE order_date BETWEEN '2022-01-01' AND '2022-12-31'
        GROUP BY customer_id
        HAVING COUNT(DISTINCT order_id) > 1
    );

```

1. What was the highest revenue earned by a salesperson in the last quarter?

```
SELECT MAX(revenue)
FROM sales
WHERE date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. How many orders were placed by customers who have made a repeat purchase in the last month?

```
SELECT COUNT(*)
FROM orders
WHERE customer_id IN (
        SELECT customer_id
        FROM orders
        WHERE order_date BETWEEN '2023-03-01' AND '2023-03-31'
        GROUP BY customer_id
        HAVING COUNT(DISTINCT order_id) > 1
    );

```

1. What is the total revenue earned from product X in the last year?

```
SELECT SUM(revenue)
FROM sales
WHERE product = 'X'
AND date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. How many orders were placed in the last year?

```
SELECT COUNT(*)
FROM orders
WHERE date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the average order value for customers who have made a purchase in the last quarter?

```
SELECT AVG(revenue)
FROM sales
WHERE customer_id IN (
        SELECT DISTINCT customer_id
        FROM sales
        WHERE date BETWEEN '2022-10-01' AND '2022-12-31'
    );

```

1. What is the total revenue earned by salesperson X in the last year?

```
SELECT SUM(revenue)
FROM sales
WHERE salesperson = 'X'
AND date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What was the most popular product sold in the last month?

```
SELECT product
FROM sales
WHERE date BETWEEN '2023-03-01' AND '2023-03-31'
GROUP BY product
ORDER BY COUNT(*) DESC
LIMIT 1;

```

1. How many orders were placed by new customers in the last year?

```
SELECT COUNT(DISTINCT CASE WHEN order_date BETWEEN '2022-01-01' AND '2022-12-31'
                            AND DATEDIFF(order_date, (SELECT MIN(order_date) FROM orders)) > 365
                        THEN customer_id END)
FROM orders;

```

1. What is the average revenue per customer in the last quarter?

```
SELECT AVG(revenue)
FROM (
        SELECT customer_id, SUM(revenue) AS revenue
        FROM sales
        WHERE date BETWEEN '2022-10-01' AND '2022-12-31'
        GROUP BY customer_id
    ) AS customer_revenue;

```

1. What percentage of customers have made a repeat purchase in the last year?

```
SELECT (COUNT(DISTINCT customer_id)
        / COUNT(DISTINCT CASE WHEN date BETWEEN '2022-01-01' AND '2022-12-31' THEN customer_id END))
        * 100
FROM sales;

```

Here are 10 sample questions that can be solved using MySQL join operations on the tables above:

1. What is the total revenue earned by salesperson X in the last month?

```
SELECT SUM(s.revenue)
FROM sales s
JOIN salespeople sp ON s.salesperson_id = sp.salesperson_id
WHERE sp.name = 'X'
AND s.date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. What is the total revenue earned by customers in city X in the last quarter?

```
SELECT SUM(s.revenue)
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
WHERE c.city = 'X'
AND s.date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What is the total revenue earned from product X sold by salesperson Y in the last year?

```
SELECT SUM(s.revenue)
FROM sales s
JOIN salespeople sp ON s.salesperson_id = sp.salesperson_id
WHERE s.product = 'X'
AND sp.name = 'Y'
AND s.date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the average revenue per sale for product X in the last quarter?

```
SELECT AVG(s.revenue/s.sales)
FROM sales s
WHERE s.product = 'X'
AND s.date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What is the total revenue earned by salesperson X from customers in city Y in the last year?

```
SELECT SUM(s.revenue)
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
JOIN salespeople sp ON s.salesperson_id = sp.salesperson_id
WHERE sp.name = 'X'
AND c.city = 'Y'
AND s.date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the average revenue per sale for salesperson X in the last month?

```
SELECT AVG(s.revenue/s.sales)
FROM sales s
JOIN salespeople sp ON s.salesperson_id = sp.salesperson_id
WHERE sp.name = 'X'
AND s.date BETWEEN '2023-03-01' AND '2023-03-31';

```

1. What is the total revenue earned from product X sold to customers in city Y in the last year?

```
SELECT SUM(s.revenue)
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
WHERE s.product = 'X'
AND c.city = 'Y'
AND s.date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the average order value for customers who made a purchase from salesperson X in the last quarter?

```
SELECT AVG(s.revenue)
FROM sales s
JOIN salespeople sp ON s.salesperson_id = sp.salesperson_id
WHERE sp.name = 'X'
AND s.date BETWEEN '2022-10-01' AND '2022-12-31';

```

1. What is the total revenue earned from product X sold to customers in city Y by salesperson Z in the last year?

```
SELECT SUM(s.revenue)
FROM sales s
JOIN customers c ON s.customer_id = c.customer_id
JOIN salespeople sp ON s.salesperson_id = sp.salesperson_id
WHERE s.product = 'X'
AND c.city = 'Y'
AND sp.name = 'Z'
AND s.date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the total revenue earned by salesperson X from repeat customers in the last quarter?

```
SELECT SUM(s.revenue)
FROM sales s
JOIN salespeople sp ON s.salesperson_id = sp.salesperson_id
WHERE sp.name = 'X'
AND s.customer_id IN (
        SELECT customer_id
        FROM orders
        WHERE order_date BETWEEN '2022-10-01' AND '2022-12-31'
        GROUP BY customer_id
        HAVING COUNT(DISTINCT order_id) > 1
    )
AND s.date BETWEEN '2022-10-01' AND '2022-12-31';

```

Here are 5 sample questions that require MySQL ranking and partitioning:

1. What are the top 10 customers by total revenue in the last year?

```
SELECT customer_id, SUM(revenue) AS total_revenue
FROM sales
WHERE date BETWEEN '2022-01-01' AND '2022-12-31'
GROUP BY customer_id
ORDER BY total_revenue DESC
LIMIT 10;

```

1. What are the top 5 salespeople by total sales in the last quarter?

```
SELECT salesperson_id, SUM(sales) AS total_sales
FROM sales
WHERE date BETWEEN '2022-10-01' AND '2022-12-31'
GROUP BY salesperson_id
ORDER BY total_sales DESC
LIMIT 5;

```

1. What is the rank of each customer by total revenue in the last year?

```
SELECT customer_id, SUM(revenue) AS total_revenue, RANK() OVER (ORDER BY SUM(revenue) DESC) AS revenue_rank
FROM sales
WHERE date BETWEEN '2022-01-01' AND '2022-12-31'
GROUP BY customer_id
ORDER BY total_revenue DESC;

```

1. What is the running total of revenue by product in the last year?

```
SELECT product, date, revenue, SUM(revenue) OVER (PARTITION BY product ORDER BY date) AS running_total
FROM sales
WHERE date BETWEEN '2022-01-01' AND '2022-12-31';

```

1. What is the rank of each salesperson by total sales in the last year, grouped by their region?

```
SELECT region, salesperson_id, SUM(sales) AS total_sales, RANK() OVER (PARTITION BY region ORDER BY SUM(sales) DESC) AS sales_rank
FROM salespeople
JOIN sales ON sales.salesperson_id = salespeople.salesperson_id
WHERE date BETWEEN '2022-01-01' AND '2022-12-31'
GROUP BY region, salesperson_id
ORDER BY region, total_sales DESC;

```