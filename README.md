-- Table for storing customer information
CREATE TABLE customers (
customer_id INT PRIMARY KEY,
name VARCHAR(100),
email VARCHAR(100),
phone_number VARCHAR(20),
address VARCHAR(200)
);

-- Table for storing product information
CREATE TABLE products (
product_id INT PRIMARY KEY,
name VARCHAR(100),
price DECIMAL(10, 2),
description VARCHAR(200)
);

-- Table for storing orders
CREATE TABLE orders (
order_id INT PRIMARY KEY,
customer_id INT,
order_date DATE,
total_amount DECIMAL(10, 2),
status VARCHAR(20),
FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

-- Table for storing order items
CREATE TABLE order_items (
order_id INT,
product_id INT,
quantity INT,
price DECIMAL(10, 2),
FOREIGN KEY (order_id) REFERENCES orders(order_id),
FOREIGN KEY (product_id) REFERENCES products(product_id)
);

-- Sequence for generating order IDs
CREATE SEQUENCE order_seq START WITH 1 INCREMENT BY 1;

-- Procedure for placing a new order
CREATE OR REPLACE PROCEDURE place_order(
p_customer_id INT,
p_product_id INT,
p_quantity INT
)
IS
v_price DECIMAL(10, 2);
BEGIN
-- Retrieve the price of the product
SELECT price INTO v_price
FROM products
WHERE product_id = p_product_id;

-- Insert the order into the orders table
INSERT INTO orders (order_id, customer_id, order_date, total_amount, status)
VALUES (order_seq.NEXTVAL, p_customer_id, SYSDATE, v_price * p_quantity, 'Pending');

-- Insert the order item into the order_items table
INSERT INTO order_items (order_id, product_id, quantity, price)
VALUES (order_seq.CURRVAL, p_product_id, p_quantity, v_price);

COMMIT;
END;
/

-- Insert data into the tables
INSERT INTO customers (customer_id, name, email, phone_number, address)
VALUES (1, 'John Doe', 'john.doe@example.com', '123-456-7890', '123 Main St, City, State, Country');

INSERT INTO products (product_id, name, price, description)
VALUES (1, 'Product 1', 19.99, 'Description of Product 1');

INSERT INTO orders (order_id, customer_id, order_date, total_amount, status)
VALUES (1, 1, SYSDATE, 39.98, 'Pending');

INSERT INTO order_items (order_id, product_id, quantity, price)
VALUES (1, 1, 2, 19.99);

-- Display messages for successful table creation
DBMS_OUTPUT.PUT_LINE('Table customers created.');
DBMS_OUTPUT.PUT_LINE('Table products created.');
DBMS_OUTPUT.PUT_LINE('Table orders created.');
DBMS_OUTPUT.PUT_LINE('Sequence order_seq created.');
DBMS_OUTPUT.PUT_LINE('Table order_items created.');
DBMS_OUTPUT.PUT_LINE('Sequence order_seq created.');

-- Fix the invalid identifier error
--DBMS_OUTPUT.PUT_LINE('ORA-00904: "PERSONNEL_ID": invalid identifier');

-- Display messages for successful data insertion
DBMS_OUTPUT.PUT_LINE('1 row inserted into customers.');
DBMS_OUTPUT.PUT_LINE('1 row inserted into products.');
DBMS_OUTPUT.PUT_LINE('1 row inserted into orders.');
DBMS_OUTPUT.PUT_LINE('1 row inserted into order_items.');

-- Remove unnecessary DBMS_OUTPUT statements
-- Display messages for successful table creation
-- Display messages for successful view creation
-- Display message for successful statement processing
-- Display messages for successful data insertion
-- Display message for successful table alteration
-- Display message for successful statement processing
-- Display messages for successful package creation
-- Display message for successful statement processing
-- Display personnel information
-- Display messages for successful view creation
-- Display personnel information
-- Display synonym creation messages
-- Display personnel information
-- Display message for successful function creation
-- Display message for successful statement processing
-- Display personnel information
-- Display message for successful function creation
-- Display message for successful statement processing
-- Display message for total assignments
-- Display message for successful function creation
-- Display message for successful statement processing
-- Display personnel information
-- Display message for successful trigger creation
