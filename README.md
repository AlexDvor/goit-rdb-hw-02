# Database Normalization Project (1NF → 2NF → 3NF)

## 📌 Project Overview

This project demonstrates the step-by-step normalization of a database
schema starting from an unnormalized table and transforming it into:

-   First Normal Form (1NF)
-   Second Normal Form (2NF)
-   Third Normal Form (3NF)

The example scenario models a simple order management system containing:

-   Customers
-   Orders
-   Products
-   Order Details

The goal was to eliminate redundancy, remove partial dependencies, and
remove transitive dependencies to achieve a properly structured
relational database.

------------------------------------------------------------------------

# 🔹 Initial Unnormalized Table

The original table stored:

-   Order number
-   Product names and quantities (stored together in one field)
-   Customer address
-   Order date
-   Customer name

Problem: - Multiple values were stored in a single column. - Data
redundancy existed. - No proper separation of entities.

------------------------------------------------------------------------

# ✅ Step 1 -- First Normal Form (1NF)

Rule: Each column must contain atomic (single) values.

What was done: - Split product list into separate rows. - Ensured each
cell contains only one value. - Each product in an order became a
separate row.

Result: One large table where: - Each row represents one product in one
order. - Data duplication still exists.

------------------------------------------------------------------------

# ✅ Step 2 -- Second Normal Form (2NF)

Rule: No partial dependency on a composite primary key.

Problem identified: - Order details depend on both order_id and
product_name. - Customer information depends only on order_id.

Solution: The table was split into:

### Orders

-   order_id (PK)
-   customer_name
-   customer_address
-   order_date

### Order_Details

-   order_id (PK, FK)
-   product_name (PK)
-   quantity

Composite primary key: PRIMARY KEY (order_id, product_name)

Result: - Removed partial dependencies. - Structured order and order
details separately.

------------------------------------------------------------------------

# ✅ Step 3 -- Third Normal Form (3NF)

Rule: No transitive dependencies.

Problem identified: customer_address depends on customer_name, which
depends on order_id.

Solution: Separated entities into four tables:

### Customers

-   customer_id (PK)
-   customer_name
-   customer_address

### Orders

-   order_id (PK)
-   order_date
-   customer_id (FK)

### Products

-   product_id (PK)
-   product_name

### Order_Details

-   order_id (PK, FK)
-   product_id (PK, FK)
-   quantity

Composite key: PRIMARY KEY (order_id, product_id)

Result: - Removed transitive dependencies. - Created proper relational
structure. - Established correct foreign key relationships.

------------------------------------------------------------------------

# 🔗 Relationships

Customers (1) → (N) Orders\
Orders (1) → (N) Order_Details\
Products (1) → (N) Order_Details

Many-to-many relationship between Orders and Products is resolved
through the Order_Details table.

------------------------------------------------------------------------

# 🛠 Technologies Used

-   MySQL 8.0
-   MySQL Workbench 8.0.46
-   EER Diagram modeling
-   SQL table design

------------------------------------------------------------------------

# 🎯 Final Outcome

The final schema follows:

-   Proper primary keys
-   Foreign key constraints
-   No redundant data
-   No partial dependencies
-   No transitive dependencies

The database structure is now fully normalized up to Third Normal Form
(3NF).

------------------------------------------------------------------------

# 👨‍💻 Author

Database normalization practice project.
