# Week 1: Selecting and Retrieving Data with SQL

## What is SQL?

- Structured Query Language
- non-procedural, descriptive
- read, update, and write data
- DBA: manages database, permissions, manage/create table
- Data Scientist: end use of database
- main use: retrieve data

## Data Models, Part 1: Thinking About Your Data

- Think before you do
- What problems you need to do with the data?
- database: container of tables
- table: data organized in columns and rows

## Data Models, Part 2: The Evolution of Data Models

- data modelling: organizes and structures information into many tables
- relational data model: write data, simple connections and structured, retrieve/update data, easy queries 
- NoSQL: unstructured data

## Data Models, Part 3: Relational v. Transactional Models

- relational: shows relationships for easy queries
- transactional: operational, hard to access
- entity: noun, thing
- attribute: adjective, characteristic
- relationship: association between entities:
  - one to many
  - many to many
  - one to one
- ER Diagrams - visual way to show relationships
- primary key - unique id
- foreign key - one or more column that can be used as unique id
- ER Diagram notation
  - Chen notation
    - 1-m, m-n, 1-1
  - crow's fit
    - train tracks for 1 and crow's foot for many
  - uml
    - 1, *

## Retrieving Data with SELECT

- one column

    ```sqlite
    SELECT column
    FROM Data;
    ```

- multiple columns
  
    ```sqlite
    SELECT column
    		, column1
    		, column2
    FROM Data;
    ```
 - all columns

	```sqlite
    SELECT *
    FROM Data;
   ```
   
- sample data (head - first 5 rows)

    ```sqlite
    SELECT *
    FROM Data
    LIMIT 5;
    ```

## Creating Tables

- write data to a database
- used for data scrapers, model predictions, etc
- Data Types:
  - **NULL**. The value is a NULL value.
  - **INTEGER**. The value is a signed integer, stored in 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value. (also used for booleans)
  - **REAL**. The value is a floating point value, stored as an 8-byte IEEE floating point number.
  - **TEXT**. The value is a text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE).
  - **BLOB**. The value is a blob of data, stored exactly as it was input.

### Create table

```sqlite
CREATE TABLE Name
(
Column1		char(10)		PRIMARY KEY,
Column2		char(250)		NOT NULL,
Column3		decimal(0,2)	NULL,
Column4		Varchar (750)	NULL
);
```

### Adding data

```sqlite
INSERT INTO Name
	(Column1
     ,Column2
     ,Column3
     ,Column4
    )
 VALUES
 	('12345'
     ,'words'
     ,'100.00'
     ,NULL
    )
```

## Creating Temporary Tables

- temporary, simpler than creating full table
- `AS` renames a table (alias)

*Note*: This code is heavily dependent on specific database system

```sqlite
CREATE TEMPORARY TABLE Temp AS
(
    SELECT *
    FROM Data
    WHERE column = 'condition'
)
```

## Adding Comments to SQL

```sqlite
-- This is a single-line comment

/*
	This is a multi-line comment
*/
```

## Additional Reading

- Star vs Snow Flake
  - Star: fact table has all dimensions (stored as their id), each id leads to another table with measures/more info about each dimension, denormalized, less joins
  - snow flake: star design but normalized, less redundancy, more joins