# Subqueries and Joins in SQL

## Using subqueries

- subqueries - queries in other queries, used for merging data between data, start with inner and connect with `WHERE`

  ```sqlite
  SELECT
  CustomerID
  ,CompanyName
  ,Region
  FROM Customers
  WHERE customerID in (SELECT CustomerID
                       FROM Orders
                       WHERE Frieght > 100 );
  ```

  

## Subquery Best Practices and Considerations

- nested subqueries have performance limitations

- subquery selects can only retrieve a single column

- best practices - use indentation

- [poorsql.com](poorsql.com) does auto-formatting

- Subqueries for calculations

  ```sqlite
  SELECT COUNT (*) AS orders
  FROM Orders
  WHERE customer_id = '123456';
  
  SELECT customer_name
  	,customer_state(
          SELECT COUNT(*) AS orders 
          FROM Orders 
          WHERE Orders.customer_id = Customer.customer_id) AS orders
  FROM customers
  ORDER BY Customer_name
  ```

- joins are sometimes more efficient

## Joining Tables: An Introduction

- data is often in multiple tables for easier manipulation and efficient storage
- join tables together with a key (unique id)
- joins are temporary for a query (not physical)

## Cartesian (Cross) Joins

- Cartesian join: each record from first table matches every record in the second table

- If first column has x rows and second table has y rows, then end result is x*y rows

- computationally taxing

- No actual matching, just multiplication

  ```sqlite
  SELECT product_name
  ,unit_price
  ,company_name
  FROM suppliers CROSS JOIN products;
  ```

## Inner Join

- used for matching values in both tables (middle part of Venn diagrams)

- Example

  ```sqlite
  -- specify which column with prequalifier
  SELECT suppliers.CompanyName
  ,ProductName
  ,UnitPrice
  FROM Suppliers INNER JOIN Products
  ON Suppliers.supplierID = Products.supplierID
  ```

- Shortcut for prequalifiers

  ```sqlite
  SELECT o.OrderID
  ,c.CompanyName
  ,e.LastName
  FROM (
      	(Orders o INNER JOIN Customers c 
           ON o.CustomerID = c.Customer ID) INNER JOIN Employees e 
        ON o. EmployeeID = e. EmployeeID );
  
  ```

## Aliases and Self Joins

- shorted name for table, specify alias in `FROM`

  ```sqlite
  SELECT vendor_name
  ,product_name
  ,product_price
  FROM Vendors AS v, Products AS p
  WHERE v.vendor_id = p.vendor_id;
  ```

- Self join

  ```sqlite
  SELECT A.CustomerName AS CustomerName1
  ,B.CustomerName as CustomerName2
  ,A.City
  FROM Customer A, Customers B
  WHERE A.CustomerID = B.CustomerID
  AND A.City = B.City
  Order BY A.City;
  ```

## Advanced Joins: Left, Right, and Full Outer Joins

- sqlite only has left joins, right and full outer are in other dbms

- left join is everything in left circle of Venn diagram (first table listed)

  ```sqlite
  -- include customers that do not have orders
  SELECT C.customerName, O.OrderID
  FROM Customers C
  LEFT JOIN Orders O ON C.CustomerID = O.CustomerID
  ORDER BY C.CustomerName;
  ```

- right join is everything in right circle of Venn diagram, can just switch order on left join

  ```sql
  SELECT Orders.OrderID,
  Employees.LastName,
  Employees.FirstName
  FROM Orders
  RIGHT JOIN Employees ON
  Orders. EmployeeID =
  Employees. EmployeeID
  ORDER BY Orders.OrderID;
  ```

- full outer join is for everything in Venn diagram

  ```sql
  SELECT Customers.CustomerName,
  Orders.OrderID
  FROM Customers
  FULL OUTER JOIN Orders ON
  Customers.CustomerID=
  Orders.CustomerID
  ORDER BY Customers.CustomerName;
  ```

## Unions

- not used much

- used to combine result-set of two or more SELECT statements

- stack tables on top of each other

  - must make sure columns, data types, etc are same in each table

- Syntax

  ```sqlite
  SELECT column_name(s) FROM
  tablel
  UNION
  SELECT column_name(s) FROM
  table2;
  ```
  
```sqlite
  SELECT City, Country FROM
  Customers
  WHERE Country='Germany'
  UNION
  SELECT City, Country FROM
  Suppliers
  WHERE Country='Germany'
  ORDER BY City;
  ```
