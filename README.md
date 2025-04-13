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
1. Clone this repository or copy the SQL scripts
2. Connect to your MySQL server:
   cmd/bash
   mysql -u root -p
Create the database:

sql
CREATE DATABASE bookstore;
USE bookstore;
Execute the schema script:

sql

SOURCE /path/to/schema.sql;
(Optional) Load sample data:

sql

SOURCE /path/to/sample_data.sql;
User Accounts
Username	Password	Privileges
bookstore_admin	secure_password	Full database access
bookstore_manager	manager_pass	Read/write all tables
bookstore_staff	staff_pass	Limited read/write access
bookstore_report	report_pass	Read-only for reporting
To create users:

sql

SOURCE /path/to/user_management.sql;
Common Queries
Inventory Management
sql

-- Check low stock items
SELECT title, stock_quantity FROM book WHERE stock_quantity < 5;

-- Add new inventory
UPDATE book SET stock_quantity = stock_quantity + 10 WHERE book_id = 101;
Customer Operations
sql

-- Find customer orders
SELECT o.order_id, o.order_date, COUNT(ol.line_id) AS items
FROM cust_order o
JOIN order_line ol ON o.order_id = ol.order_id
WHERE o.customer_id = 42
GROUP BY o.order_id;
Order Processing
sql

-- Update order status
INSERT INTO order_history (order_id, status_id)
VALUES (1001, 3); -- 3 = Shipped

-- Calculate daily sales
SELECT DATE(order_date) AS day, SUM(price*quantity) AS total
FROM cust_order o
JOIN order_line ol ON o.order_id = ol.order_id
GROUP BY day;
Best Practices
Backup Regularly:

cmd/bash

mysqldump -u root -p bookstore > bookstore_backup.sql
Indexing: Consider adding indexes on frequently queried columns:

sql

CREATE INDEX idx_book_title ON book(title);
CREATE INDEX idx_customer_email ON customer(email);
Security:

Rotate passwords quarterly

Limit admin access to essential personnel

Audit user privileges regularly

Troubleshooting
Issue: Foreign key constraint failures
Solution: Ensure referenced data exists before inserting:

sql

-- Check if publisher exists first
SELECT publisher_id FROM publisher WHERE publisher_name = 'Penguin Books';
Issue: Performance problems with large datasets
Solution: Add appropriate indexes and optimize queries with EXPLAIN:

sql

EXPLAIN SELECT * FROM book WHERE title LIKE '%Harry%';

Support
For assistance, please contact:

Database Administrator: admin@bookstore.com

Technical Support: support@bookstore.com

Note: This documentation assumes MySQL 8.0+. Some syntax may need adjustment for earlier versions.
