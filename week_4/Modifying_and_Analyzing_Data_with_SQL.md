# Week 4: Modifying and Analyzing Data for SQL

## Working with Text Strings

- concatenate

  ```sqlite
  SELECT CompanyName, ContactName, CompanyName || ' ('|| ContactName||')'
  FROM Customers
  ```

- trim - removes trailing whitespace

  - `TRIM`, `RTRIM` `LTRIM`

  ```sqlite
  SELECT TRIM(" Text  ") AS TrimmedString
  ```

- substring

  ```sqlite
  SELECT string
  , SUBSTR(string, start_pos, num_char) -- 1-based index, includes start-pos
  FROM data
  ```

- change case

  ```sqlite
  SELECT
  UPPER(column_name)
  , LOWER(column_name)
  FROM data
  ```

## Date and Time Strings

- Unique for DBMS
- DATE: YYYY-MM-DD
- DATETIME: YYYY-MM-DD HH:MI:SS
- TIMESTAMP: YYYY-MM-DD HH:MI:SS
- Functions:
  - DATE(timestring, modifiers), TIME(), DATETIME(), JULIANDAY(), STRFTIME()

- Modifiers:
  - NNN days, NNN hours, start of month, etc

## Date and Time String Examples

- Example

  ```sqlite
  SELECT Birthdate
  ,STRFTIME('%Y', Birthdate) AS Year
  ,STRFTIME('%m', Birthdate) AS Month
  ,STRFTIME('%d', Birthdate) AS Day
  FROM data
  ```

- Current Time

  ```sqlite
  SELECT STRFTIME('%H %M %S %s', 'now')
  -- compute age from above example
  SELECT DATE(('now') - Birthdate) AS Age
  ```

## Case Statement

- like if, then, else

  ```sqlite
  SELECT
  CASE input
  WHEN condition THEN result
  ELSE result
  END column_name_result
  ```

- result of when can also be a fill for another column

## Views

- views are stored queries

- add or remove columns without changing database

- use it to encapsulate queries

  ```sqlite
  CREATE [TEMP] VIEW [IF NOT EXISTS]
  view_name(column_name_list) AS
  select_statement;
  ```

- Example

  ```sqlite
  CREATE VIEW my_view
  AS
  SELECT
  column
  FROM a
  
  SELECT *
  FROM my_view
  
  DROP VIEW my_view;
  ```

## Data Governance and Profiling

- data profiling - descriptive statistics, number of rows, table size, when was table last updated
  - column data profiling - data type, distinct values, number of rows with null, descriptive statistics
- governance - depends on company, understand read and write permissions, clean up environments

## SQL For Data Science

- data understanding
  - Null, string, dates and times, understanding where data joins
- business understanding
  - what is the goal?, unspoken need
- profiling
  - data quality, format issues
- SELECT first and then other commands
  - data model
  - joins and calculations
  - start simple and build on to it
- Test
  - test along the way
  - number of values that joins are returning
- Format and Comment
  - clean code, easy to read
- Review when re-running old queries
  - has data changed, has business rules changed, date indicators changed?, etc

**Note**: Use this [website](https://sqlzoo.net/) for interview prep.