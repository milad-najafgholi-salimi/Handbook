A **unique constraint** ensures that all values in a column (or combination of columns) are **distinct** across the entire table. Unlike primary keys:

- Allows **one NULL** value (or multiple NULLs in PostgreSQL)
    
- Can have **multiple** unique constraints per table
    
- Can be added to existing columns

### Syntax:
**During table creation:**
```
CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE,           -- Column-level
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(20)
);

-- OR with explicit constraint name
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    sku VARCHAR(20) CONSTRAINT unique_sku UNIQUE,
    name VARCHAR(100)
);
```

**Adding to existing table:**
```
-- Simple syntax
ALTER TABLE users ADD UNIQUE (email);

-- With custom constraint name (recommended)
ALTER TABLE users ADD CONSTRAINT uk_users_email UNIQUE (email);

-- Multiple columns (composite unique)
ALTER TABLE users ADD CONSTRAINT uk_users_name_birth UNIQUE (first_name, last_name, birth_date);
```

### Composite Unique Constraints

**Two or more columns together must be unique:**
```
-- Example: Same user can't order same product twice
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    user_id INT,
    product_id INT,
    order_date DATE,
    UNIQUE (user_id, product_id)  -- Combination must be unique
);

-- Or with explicit name
ALTER TABLE orders 
ADD CONSTRAINT uk_orders_user_product UNIQUE (user_id, product_id);
```

**What this means:**
```
-- Allowed (different combinations)
INSERT INTO orders VALUES (1, 1, '2026-01-01');  -- User 1, Product A
INSERT INTO orders VALUES (1, 2, '2026-01-02');  -- User 1, Product B
INSERT INTO orders VALUES (2, 1, '2026-01-03');  -- User 2, Product A

-- NOT allowed (duplicate combination)
INSERT INTO orders VALUES (1, 1, '2026-01-04');  -- ERROR! User 1, Product A exists
```

### NULL Behavior in Unique Constraints

**PostgreSQL treats NULLs as distinct:**
```
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);

-- These are ALL allowed (multiple NULLs)
INSERT INTO users (email) VALUES (NULL);  -- Allowed
INSERT INTO users (email) VALUES (NULL);  -- Allowed
INSERT INTO users (email) VALUES (NULL);  -- Allowed

-- Only one non-NULL value allowed
INSERT INTO users (email) VALUES ('john@test.com');  -- Allowed
INSERT INTO users (email) VALUES ('john@test.com');  -- ERROR! Duplicate
```
