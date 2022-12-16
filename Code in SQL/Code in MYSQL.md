
--Users table
CREATE TABLE Users (
  user_id int NOT NULL AUTO_INCREMENT,
  first_name varchar(255) NOT NULL,
  last_name varchar(255) NOT NULL,
  email varchar(255) NOT NULL,
  password varchar(255) NOT NULL,
  PRIMARY KEY (user_id)
);

--Products table
CREATE TABLE Products (
  product_id int NOT NULL AUTO_INCREMENT,
  name varchar(255) NOT NULL,
  price double NOT NULL,
  category_id int NOT NULL,
  PRIMARY KEY (product_id),
  FOREIGN KEY (category_id) REFERENCES Categories(category_id)
);

--Categories table
CREATE TABLE Categories (
  category_id int NOT NULL AUTO_INCREMENT,
  name varchar(255) NOT NULL,
  PRIMARY KEY (category_id)
);


-- Add new Item
INSERT INTO Products (name, price, category_id)
VALUES ('Product Name', 24.99, 1);

-- Update Products
UPDATE Products 
SET name = 'New Product Name', price = 29.99
WHERE product_id = 4;

-- Delete Products
DELETE FROM Products
WHERE product_id = 4;

-- Create Categories
INSERT INTO Categories (name)
VALUES ('Category Name');

-- Update Categories
UPDATE Categories
SET name = 'New Category Name'
WHERE category_id = 3;

-- Delete Categories
DELETE FROM Categories
WHERE category_id = 3;

-- List Products
SELECT * FROM Products;

-- List Categories
SELECT * FROM Categories;
