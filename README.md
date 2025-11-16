# PRIME_WEARS-SQL_PROJECT
Prime Wears SQL Analytics Project

**A Data Analysis Case Study using MySQL**


**📌 Project Overview**

Prime Wears is a mid-sized e-commerce fashion brand selling men’s wears, women’s wears, and accessories.
This SQL project analyzes 10,000+ transactional records across customers, orders, payments, and product catalogs to uncover insights that support sales optimization, customer understanding, and product strategy.

The analysis focuses on questions such as:

Which products generate the most or least revenue?

Which countries contribute the highest sales?

Who are the best-performing customers?

Which fashion categories perform best?


**📁 Dataset Structure**

The project uses five normalized CSV files:

Table Description

customers Customer demographics & locations
orders Order-level records
order_details Line-level details of each order
products Product catalog with categories & prices
payments Payment transactions per order


🗂 Entity–Relationship Diagram (ERD)

customers (customer_id PK)
    |
    | 1..*
    |
orders (order_id PK, customer_id FK)
    |
    | 1..*
    |
order_details (detail_id PK, order_id FK, product_id FK)
                    |
                    | *..1
                    |
               products (product_id PK)

payments (payment_id PK, order_id FK)


**🛠 SQL Setup**

**Create Tables**

CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(150),
    country VARCHAR(100),
    signup_date DATE
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(200),
    category VARCHAR(100),
    unit_price DECIMAL(10,2)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(12,2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE order_details (
    detail_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    unit_price DECIMAL(10,2),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

CREATE TABLE payments (
    payment_id INT PRIMARY KEY,
    order_id INT,
    payment_method VARCHAR(50),
    payment_date DATE,
    amount DECIMAL(12,2),
    FOREIGN KEY (order_id) REFERENCES orders(order_id)
);


---

📊 Key SQL Queries

Top-selling product

SELECT p.product_name,
       SUM(od.quantity * od.unit_price) AS total_sales
FROM order_details od
JOIN products p ON od.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sales DESC
LIMIT 1;

Least-selling product

SELECT p.product_name,
       SUM(od.quantity * od.unit_price) AS total_sales
FROM order_details od
JOIN products p ON od.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_sales ASC
LIMIT 1;

Top 5 countries by revenue

SELECT c.country,
       SUM(o.total_amount) AS total_revenue
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.country
ORDER BY total_revenue DESC
LIMIT 5;

Top 5 customers by spending

SELECT c.first_name,
       c.last_name,
       SUM(o.total_amount) AS total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id
ORDER BY total_spent DESC
LIMIT 5;

Best-selling category

SELECT p.category,
       SUM(od.quantity) AS units_sold
FROM order_details od
JOIN products p ON od.product_id = p.product_id
GROUP BY p.category
ORDER BY units_sold DESC;



**🧠 Insights & Findings**

1. Best-selling product → Trendy Wears

Consistently generates the highest revenue.

2. Least-selling product → Premium Cap

Lowest sales volume, indicating weak demand.

3. Top customer locations

USA leads

Followed by UK, Canada, Australia, and Germany
These five countries drive a large share of total revenue.


4. Top 5 customers

These key customers contribute massively to total revenue — strong opportunity for retention strategies.

5. Best-performing category → Women Wears

Highest units sold and strongest growth potential.




**💼 Business Recommendations**

✔ Focus marketing and inventory on Trendy Wears & Women Wears

Demand is consistently strong.

✔ Reposition or rebrand Premium Cap

Try bundles, discounts, or design updates.

✔ Target high-value markets

USA, UK, Canada, Australia, and Germany show the best conversions.

✔ Launch a customer loyalty program

Top spenders should be nurtured for repeat purchases.

✔ Expand women fashion lines

Their growth rate and revenue contribution are significantly higher.


---

🚀 How to Use This Project

1. Import the CSV data into MySQL Workbench


2. Run the CREATE TABLE script


3. Load each dataset into its table


4. Execute the analysis queries


5. Extend this into a BI dashboard (Power BI, Excel, or Table
6. 

**📁 Recommended Repository Structure**

Prime-Wears-SQL-Project/
│
├── datasets/
│   ├── customers.csv
│   ├── orders.csv
│   ├── order_details.csv
│   ├── products.csv
│   ├── payments.csv
│
├── sql_scripts/
│   ├── create_tables.sql
│   ├── analysis_queries.sql
│
└── README.md



👨‍💻 Author

Solomon Adeniran – PrimeSol Analytics
SQL • Excel • Power BI • Data Analytics
