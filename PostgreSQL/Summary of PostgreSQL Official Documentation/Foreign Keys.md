## What is a Foreign Key?

A **Foreign Key** is a column (or set of columns) in one table that references the **Primary Key** of another table. It creates a link between two tables, establishing a **relationship**.

Think of it like this:

- **Primary Key** = "I am unique. I identify this row."
    
- **Foreign Key** = "I point to a row in another table. I must exist there."

---
### A Real-World Example

Let's say you have an customers database:
```
-- The "parent" table
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE
);

-- The "child" table with a foreign key
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INTEGER REFERENCES customers(customer_id),
    order_date TIMESTAMP DEFAULT NOW(),
    total DECIMAL(10,2)
);
```

---
## Why Use Foreign Keys? (The "Referential Integrity" Benefit)

Foreign keys enforce **data consistency** automatically. PostgreSQL prevents two common problems:

### 1. **Orphaned Records**

Without a foreign key, you could delete a customer but keep their orders → "orphaned" data.
```
-- With FK: This would FAIL if customer has orders
DELETE FROM customers WHERE customer_id = 1;
-- ERROR: update or delete on table "customers" violates foreign key constraint
```
### 2. **Invalid References**

Without a FK, you could insert an order for customer_id 999 that doesn't exist.
```
-- With FK: This FAILS
INSERT INTO orders (customer_id, total) VALUES (999, 100.50);
-- ERROR: insert or update on table "orders" violates foreign key constraint
```
