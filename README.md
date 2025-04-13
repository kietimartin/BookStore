# BookStore Database System - README

## Overview
This MySQL database system is designed for managing operations of a bookstore, including inventory, customers, orders, and shipping. The database follows relational design principles with proper normalization and relationships between entities.

## Database Schema

### Core Tables
- **Books & Authors**: `book`, `author`, `book_author`, `book_language`, `publisher`
- **Customers**: `customer`, `address`, `customer_address`, `country`, `address_status`
- **Orders**: `cust_order`, `order_line`, `order_history`, `order_status`, `shipping_method`

### Entity Relationship Diagram
![ER Diagram](er_diagram.png) *(Note: Include your Draw.io generated diagram here)*

## Installation Instructions

### Prerequisites
- MySQL Server (8.0+ recommended)
- MySQL Workbench or command line client
- Basic SQL knowledge

### Setup Steps
1. Clone this repository or copy the SQL scripts<br>
2. Connect to your MySQL server:<br>
   cmd/bash<br>
   mysql -u root -p<br>
Create the database:<br>

sql<br>
CREATE DATABASE bookstore;<br>
USE bookstore;<br>
Execute the schema script:

sql<br>

SOURCE /path/to/schema.sql;<br>
(Optional) Load sample data:<br>

sql<br>

SOURCE /path/to/sample_data.sql;<br>
User Accounts<br>
Username	Password	Privileges<br>
bookstore_admin	secure_password	Full database access<br>
bookstore_manager	manager_pass	Read/write all tables<br>
bookstore_staff	staff_pass	Limited read/write access<br>
bookstore_report	report_pass	Read-only for reporting<br>
To create users:<br>

sql<br>

SOURCE /path/to/user_management.sql;<br>
Common Queries<br>
Inventory Management<br>
sql<br>

-- Check low stock items<br>
SELECT title, stock_quantity FROM book WHERE stock_quantity < 5;<br>

-- Add new inventory<br>
UPDATE book SET stock_quantity = stock_quantity + 10 WHERE book_id = 101;<br>
Customer Operations<br>
sql<br>

-- Find customer orders<br>
SELECT o.order_id, o.order_date, COUNT(ol.line_id) AS items<br>
FROM cust_order o<br>
JOIN order_line ol ON o.order_id = ol.order_id<br>
WHERE o.customer_id = 42<br>
GROUP BY o.order_id;<br>
Order Processing<br>
sql<br>

-- Update order status<br>
INSERT INTO order_history (order_id, status_id)<br>
VALUES (1001, 3); -- 3 = Shipped<br>

-- Calculate daily sales<br>
SELECT DATE(order_date) AS day, SUM(price*quantity) AS total<br>
FROM cust_order o<br>
JOIN order_line ol ON o.order_id = ol.order_id<br>
GROUP BY day;<br>
Best Practices<br>
Backup Regularly:<br>

cmd/bash<br>

mysqldump -u root -p bookstore > bookstore_backup.sql<br>
Indexing: Consider adding indexes on frequently queried columns:<br>

sql<br>

CREATE INDEX idx_book_title ON book(title);<br>
CREATE INDEX idx_customer_email ON customer(email);<br>
Security:<br>

Rotate passwords quarterly

Limit admin access to essential personnel

Audit user privileges regularly<br>

Troubleshooting<br>
Issue: Foreign key constraint failures<br>
Solution: Ensure referenced data exists before inserting:

sql<br>

-- Check if publisher exists first<br>
SELECT publisher_id FROM publisher WHERE publisher_name = 'Penguin Books';<br>
Issue: Performance problems with large datasets<br>
Solution: Add appropriate indexes and optimize queries with EXPLAIN:<br>

sql<br>

EXPLAIN SELECT * FROM book WHERE title LIKE '%Harry%';

Support<br>
For assistance, please contact:

Database Administrator: admin@bookstore.com

Technical Support: support@bookstore.com

Note: This documentation assumes MySQL 8.0+. Some syntax may need adjustment for earlier versions.
