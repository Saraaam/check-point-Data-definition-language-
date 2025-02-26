# check-point-Data-definition-language

Step 1: Create Tables

-- Creating the CUSTOMER table
CREATE TABLE CUSTOMER (
    CustomerID NUMBER PRIMARY KEY,
    Name VARCHAR2(100) NOT NULL,
    Email VARCHAR2(100) UNIQUE,
    Phone VARCHAR2(20),
    Address VARCHAR2(255)
);

-- Creating the PRODUCT table
CREATE TABLE PRODUCT (
    ProductID NUMBER PRIMARY KEY,
    Name VARCHAR2(100) NOT NULL,
    Price NUMBER(10,2) CHECK (Price > 0),
    StockQuantity NUMBER CHECK (StockQuantity >= 0)
);

-- Creating the ORDERS table
CREATE TABLE ORDERS (
    OrderID NUMBER PRIMARY KEY,
    CustomerID NUMBER,
    FOREIGN KEY (CustomerID) REFERENCES CUSTOMER(CustomerID)
);

-- Creating the ORDER_DETAILS table
CREATE TABLE ORDER_DETAILS (
    OrderDetailID NUMBER PRIMARY KEY,
    OrderID NUMBER,
    ProductID NUMBER,
    Quantity NUMBER CHECK (Quantity > 0),
    FOREIGN KEY (OrderID) REFERENCES ORDERS(OrderID),
    FOREIGN KEY (ProductID) REFERENCES PRODUCT(ProductID)
);

Step 2: Add Required Columns

-- Adding the Category column to the PRODUCT table
ALTER TABLE PRODUCT ADD Category VARCHAR2(20);

-- Adding the OrderDate column to the ORDERS table with default SYSDATE
ALTER TABLE ORDERS ADD OrderDate DATE DEFAULT SYSDATE;
