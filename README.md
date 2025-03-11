# Bike Store Database Project

## Project Overview
This project involves setting up and analyzing a **Bike Store Database** using **PostgreSQL**. The database includes tables related to stores, products, customers, orders, and staff. It is designed to help users practice SQL queries for data analysis and management.

## Database Schema
The database consists of the following tables:

1. **brands** - Contains bike brand information.
2. **category** - Stores product categories.
3. **customers** - Stores customer details.
4. **order_items** - Contains products ordered in each order.
5. **orders** - Stores order details.
6. **products** - Contains bike product information.
7. **staffs** - Stores employee details.
8. **stocks** - Keeps track of product quantities in different stores.
9. **stores** - Stores information about physical bike stores.

## SQL Queries for Practice
Here are some SQL queries you can practice on this dataset:

### 1. Get Products That Have Never Been Sold
```sql
SELECT p.product_name
FROM products p
LEFT JOIN order_items oi ON p.product_id = oi.product_id
WHERE oi.product_id IS NULL;
```

### 2. Find the Total Sales Per Store
```sql
SELECT s.store_name, SUM(oi.quantity * oi.list_price) AS total_sales
FROM stores s
JOIN orders o ON s.store_id = o.store_id
JOIN order_items oi ON o.order_id = oi.order_id
GROUP BY s.store_name
ORDER BY total_sales DESC;
```

### 3. Get the Top 5 Best-Selling Products
```sql
SELECT p.product_name, SUM(oi.quantity) AS total_sold
FROM products p
JOIN order_items oi ON p.product_id = oi.product_id
GROUP BY p.product_name
ORDER BY total_sold DESC
LIMIT 5;
```

### 4. Find Customers Who Have Placed More Than 5 Orders
```sql
SELECT c.customer_id, c.first_name, c.last_name, COUNT(o.order_id) AS total_orders
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name
HAVING COUNT(o.order_id) > 5;
```

### 5. Get Staff Members Who Have Managed Orders
```sql
SELECT s.staff_id, s.first_name, s.last_name, COUNT(o.order_id) AS managed_orders
FROM staffs s
JOIN orders o ON s.staff_id = o.staff_id
GROUP BY s.staff_id, s.first_name, s.last_name
ORDER BY managed_orders DESC;
```

## How to Use This Project
1. Clone this repository:
   ```sh
   git clone https://github.com/your-username/bike-store-database.git
   ```
2. Import the SQL file into **PostgreSQL**.
3. Run the queries in a PostgreSQL client like **pgAdmin** or **DBeaver**.
4. Modify and explore additional queries for practice.

## Technologies Used
- **PostgreSQL** for database management.
- **SQL** for querying the data.
- **GitHub** for version control.

## Author
[Your Name]

## License
This project is open-source under the [MIT License](LICENSE).

