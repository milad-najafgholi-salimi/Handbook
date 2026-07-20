### What is a Primary Key?

A **primary key** is a constraint that uniquely identifies each row in a table. It ensures:

- **Uniqueness**: No duplicate values
    
- **Not NULL**: Every row must have a value
    
- Each table can have only **one** primary key

### Syntax:
**During table creation:**
```
CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100)
);
```

**Adding to existing table:**
```
ALTER TABLE table_name ADD PRIMARY KEY (column_name);
```

**Dropping a Primary Key:**
```
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```
### Single vs Composite Keys

**Single-column primary key:**
```
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(100)
);
```

**Composite (multiple columns):**
```
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
-- Combination of both columns must be unique
```
