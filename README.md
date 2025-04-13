# BookStore Database System - README

## Overview
The BookStore database system is designed for managing operations of a bookstore, including inventory, customers, orders, and shipping.<br>
The database follows relational design principles with proper normalization and relationships between entities.<br>

## Database Schema

### Core Tables
- **Books & Authors**: `book`, `author`, `book_author`, `book_language`, `publisher`
- **Customers**: `customer`, `address`, `customer_address`, `country`, `address_status`
- **Orders**: `cust_order`, `order_line`, `order_history`, `order_status`, `shipping_method`

### Entity Relationship Diagram
![ER Diagram]((https://drive.google.com/file/d/1w9I_kbbW14mDqNyoLZSSOEwg10ZrJUbf/view?usp=sharing))

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



Support<br>
For assistance, please contact:

Database Administrator: admin@bookstore.com

Technical Support: support@bookstore.com

Note: This documentation assumes MySQL 8.0+. Some syntax may need adjustment for earlier versions.
