# Filtering, Sorting, and Calculating Data with SQL

## Basic Filtering with SQL

- reduces amount of data analyzing by adding conditions

  - increases query performance, reduced strain on client application

- Use `WHERE` for conditional

    ```sqlite
    SELECT column
    FROM Data
    WHERE column operator value;
    ```

  - operators:

    - `=`: equal

        ```sqlite
        SELECT column
        FROM Data
        WHERE column == '10';
        ```

    - `<>`: not equal

    - `>`

    - `<`

    - `>=`

    - `<=`

    - `BETWEEN`: range of values

        ```sqlite
        SELECT column
        FROM Data
        WHERE column BETWEEN 5 AND 15;
        ```

    - `IS NULL`

        ```sqlite
        SELECT column
        FROM Data
        WHERE column IS NULL;
        ```

    
## Advanced Filtering

- `IN`: range of conditions in list

    ```sqlite
    SELECT column
    FROM Data
    WHERE column IN (5,6,10,12);
    ```

- `OR`: uses short circuit evaluation, `IN` is faster than `OR`

    ```sqlite
    SELECT column
    FROM Data
    WHERE column = 9 OR column = 5;

    ```

- `AND`

  ```sqlite
  SELECT column, column2
  FROM Data
  -- use paranthesis for order of operations (ignore short circuit evaluation here)
  WHERE (column = 9 OR column = 5)
  AND column2 = 3;
  ```

- `NOT`: exclude items

  ```sqlite
  SELECT column, column2
  FROM Data
  -- use paranthesis for order of operations (ignore short circuit evaluation here)
  WHERE NOT column = 'A';
  ```

  

## Wildcards

- `LIKE` and wildcards(%, _) can be used for strings, etc
  - '%Pizza': anything ending with Pizza
  - 'A%T': anything that starts with A and ends with T
  - will not match null
  - '_pizza': single character before pizza
  - '[]': set of characters in a location
-  wildcards are slow

## Sorting with `ORDER BY`

- Default is essentially random order

- `ORDER BY`: last clause, can sort by column you did not select, takes in name of one or more column

  ```sqlite
  SELECT column
  FROM Data
  ORDER BY column;
  ```

  - column order

    ```sqlite
    SELECT column
    FROM Data
    ORDER BY 1;
    ```

- `DESC` (descending) and `ASC` (default is ascending)

## Math Operations

- `+`, `-`, `/`,`*`

  ```sqlite
  SELECT
  column1
  ,column2
  ,column1 * column2 AS calcColumn
  FROM Data;
  ```

- Order of operations: PEMDAS

## Aggregate Functions

- Used for summarizing and analyzing data

- `SUM ()`, `AVG ()`, `MIN ()`, `MAX ()`, `COUNT` ()

  ```sqlite
  SELECT AVG(column1) AS avg_1
  FROM Data;
  ```

  ```sqlite
  -- include nulls in count
  SELECT COUNT (*) AS total
  FROM Data;
  
  -- only count non-null values in one column
  SELECT COUNT(column) AS small_total
  FROM Data;
  ```

- use alias because it will return blank column name as default

- Combine operations and aggregate functions for analysis

  ```sqlite
  SELECT SUM(column1*column2) AS sum_product
  FROM Data
  WHERE ID = 2;
  ```

- `DISTINCT`: can't use on `COUNT(*)`, avoids duplicates, default is ALL instead of DISTINCT

  ```sqlite
  SELECT COUNT(DISTINCT ID) AS size
  FROM Data
  ```

  

## Grouping Data

- `GROUP BY` and `HAVING`: aggregate on a particular value, NULLs are grouped together

- `GROUP BY`

  ```sqlite
  -- total of column 2 value in each unique vaule of column 1
  SELECT
  column1
  ,COUNT(column2) as total_2
  FROM Data
  GROUP BY column1
  ```

- `HAVING`: WHERE does not work for groups bc it filters on rows, WHERE filters before data is grouped, HAVING filters after data is grouped

  ```sqlite
  SELECT
  CustomerID
  ,COUNT (*) AS orders
  FROM Orders
  GROUP BY CustomerID
  HAVING COUNT (*) >= 2;
  ```

## Putting it All Together

- be careful and do smaller queries with testing
- do filtering in SQL to lower load on client side (R, Python)
- Order of clauses:
  - `SELECT`	
  - `FROM`
  - `WHERE` (optional)
  - `GROUP BY` (optional)
  - `HAVING` (optional)
  - `ORDER BY` (optional)

## Supplemental Reading

- `SQLDF` package for SQL in R
- `python-sql` package for SQL in Python

