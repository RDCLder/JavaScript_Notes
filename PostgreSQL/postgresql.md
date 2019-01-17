# PostgreSQL

## General

- [Documentation](https://www.postgresql.org/docs/current/index.html)

- Database
  - A collection of related data or information that is stored, modified, and transmittetd.
  - Modularized into tables that contain rows and tables
  - Tables consist of rows and columns which contain rectangles with values

- PostgreSQL 
  - An open-source, object-relational database management system (ORDBMS).
    - Can be used, modified, and distributed by anyone for any purpose.
  - Supports a large part of SQL standard and offers many modern features.
    - Complex queries
    - Foreign keys
    - Triggers
    - Updatable views
    - Transactional integrity
    - Multiversion concurrency control 
  - Can be easily extended
  
- Ways to run SQL
  - Use psql shell
    - Type ```psql``` in a terminal
    - [Cheatsheet 1](http://postgresguide.com/utilities/psql.html)
    - [Cheatsheet 2](https://www.postgresql.org/docs/current/index.html)
  - Use psql to run a sql file
    - Open databsase: ```psql dbName```
    - Apply SQL file to database: ```psql dbName -f file.sql```
  - Postico

---

## Syntax
 
### Common Statements
  
- **Create Database**
  - Syntax
    ```sql
    CREATE DATABASE dbName;
    ```
  - e.g.
    ```sql
    CREATE DATABASE novClass;
    ```
- **Create Table**
  - Syntax
    ```sql
    CREATE TABLE tableName (
      columnNames data types  
    );
    ```
  - e.g.
    ```sql
    CREATE TABLE student (
      id SERIAL NOT NULL PRIMARY KEY,
      name VARCHAR,
      github VARCHAR,
      points INTEGER,
      start_date DATE,
      graduated BOOLEAN
    );
    ```
- **Insert**
  - Syntax
    - Full values
      ```sql
      INSERT INTO tableName values (value1, value2, etc. valueN)
      ```
    - Partial values
      ```sql
      INSERT INTO tableName (keys) values (corresponding values)
      ```
  - e.g.
    - Full values
      ```sql
      INSERT INTO student VALUES (
        DEFAULT, 'Paul', 'pizzapanther', 6, '2017-04-17', FALSE
      );
      ```
    - Partial values
      ```sql
      INSERT INTO student (name, github) VALUES (
        'Paul', 'pizzapanther'
      );
      ```

- **Update**
  - Syntax
    ```sql
    UPDATE tableName SET attribute = value WHERE attribute = value
    ```
    - The first attribute is being changed while the second attribute after WHERE selects which columns by a specified attribute.
    - If no criteria is set, all entries with the attribute will be selected.
    - Multiple attributes can be selected.
  - e.g.
    ```sql
    -- Select student with id = 1
    UPDATE student SET points = 8 WHERE id = 1;
    ```
    ```sql
    -- Select all students
    UPDATE student SET points = 8;
    ```
    ```sql
    -- Multiple attribute updates
    UPDATE student SET points = 8, graduated = TRUE WHERE id = 1;
    ```

- **Delete**
  - Syntax
    ```sql
    DELETE FROM table where attribute = value
    ```
  - e.g.
    ```sql
    -- Delete student with matching id
    DELETE FROM student where id = 1
    ```
    ```sql
    -- Delete all entries from student table
    DELETE FROM student;
    ```

- **Select**
  - ```sql
    SELECT attribute FROM table;
    ```
    - Multiple attributes can be selected
    - * selects all attributes
  - e.g.
    ```sql
    -- Select multiple attributes
    SELECT name, website FROM student;
    
    SELECT id, name FROM student;
    
    SELECT * FROM student;
    ```

- **Where**
  - Used to select entries that have match the criteria
  - ```SELECT attribute FROM table WHERE attribute = value;
    - The attribute after WHERE sets the criteria
    - Multiple attributes can be set for the criteria
  - e.g.
    ```sql
    SELECT name FROM student where gender = 'F';
    
    SELECT * from student WHERE points > 7;
    ```
    ```sql
    -- and operator
    SELECT name FROM student WHERE gender = 'F' and points > 7;
    ```
    ```sql
    -- like operator for substring comparison
    SELECT * FROM student WHERE gihub_username like '%thompson%;
    ```
    ```sql
    -- ilike operator for case insensitivity
    SELECT * FROM student WHERE gihub_username ilike '%thompson%;
    ```
    ```sql
    SELECT * FROM student WHERE website is NULL;
    ```

- **ADD/DROP/MODIFY** Column
  - Add
    ```sql
    ALTER TABLE tableName ADD columnName datatype
    ```
  - Drop
    ```sql
    ALTER TABLE tableName DROP COLUMN columnName
    ```
  - Modify
    ```sql
    MODIFY COLUMN columnName datatype
    ```

### Syntax

- Default Values
  - Syntax
    ```sql
    CREATE TABLE student (
      attribute type default value
    );
    ```
  - e.g.
    ```sql
    CREATE TABLE student (
      id SERIAL NOT NULL PRIMARY KEY,
      name VARCHAR,
      github VARCHAR,
      points INTEGER DEFAULT 0,
      start_date DATE,
      graduated BOOLEAN DEFAULT FALSE
    );
    ```

- Constraints
  - Determes what types of values can be input
    - Placed after DEFAULT value
  - Common constraints
    - NOT NULL: Prevents a column value from being NULL
    - UNIQUE: Prevent rows from having the same value
    - CHECK: Number range checks and more
  - e.g.
    ```sql
    CREATE TABLE student (
      id SERIAL NOT NULL PRIMARY KEY,
      name varchar,
      github varchar UNIQUE NOT NULL,
      points integer DEFAULT 0 CHECK (points >= 0),
      start_date date NOT NULL,
      graduated boolean DEFAULT FALSE
    );
    ```
  
- Primary Keys
  - A column or columns that uniquely identify a row
    - Used for lookups (like keys in a dictionary)
    - In reality is simply the combination of the constraints: NOT NULL and UNIQUE
  - Placed after constraints
  - e.g.
    ```sql
    CREATE TABLE student (
      name varchar,
      github varchar UNIQUE NOT NULL,
      points integer DEFAULT 0 CHECK (points >= 0),
      start_date date NOT NULL,
      graduated boolean DEFAULT FALSE,
      PRIMARY KEY (name, github)
    );
    ```

- Serial IDs
  - Auto-incremeneting integers
    - Increments with eacn new entry
  - Commonly used with primary keys for searching

- Naming Convention
  - All uppercase for SQL statements
  - All lowercase for naming tables, columns, etc.
  - Ultimately case insensitive with a few exceptions

- Data Types
  - String Types
    - CHAR(n): fixed length string
    - VARCHAR(n): vary length string with limit
    - VARCHAR or text: no limit
  - Number Types
    - Integer
    - Numeric: precise decimal (good for currency)
    - Real: floating point
  - Other
    - Date
    - Timestamp
    - Boolean
    
- Syntax
  - Strings - use single quotes (double quotes are for column names)
  - Booleans - use TRUE or FALSE
  - Null - use NULL
  
- CRUD Operations
  - Create
  - Read
  - Update
  - Delete

---

## Data Aggregation

- Data aggregation is a process in which information is gathered and expressed in a summary form
  - Statistical analysis
  - Obtain more information about particular groups based on specific criteria (e.g. age, profession, income, etc.)
  
- **COUNT**
  - e.g.
    ```sql
    SELECT COUNT(*) FROM student;
    ```
    ```sql
    -- Students with Github
    SELECT COUNT(github) FROM student;
    ```
    
- **SUM**
  - e.g.
    ```sql
    SELECT SUM(points) FROM student;
    ```

- Common Functions
  - **AVG**
  - **MAX**
  - **MIN**

- **GROUP BY**
  - Displays the specified attributes' values grouped by a specified attribute
    - The attribute must be one of the selected attributes
  - e.g.
    ```sql
    SELECT start_date, sum(points) FROM GROUP BY start_date;
    ```
    ```sql
    -- more stats!
    SELECT start_date,
      SUM(points) AS total_points,
      AVG(points) AS average_points,
      COUNT(*) AS num_students
    FROM student GROUP BY start_date;
    ```

- **ORDER BY**
  - Orders 
  - e.g.
    ```sql
    SELECT * FROM student ORDER BY points;
    ```
    
- **LIMIT/OFFSET**
  - e.g.
  ```sql
  SELECT * FROM student ORDER BY points LIMIT 5;
  ```
  ```sql
  -- offset (pagination)
  SELECT * FROM student ORDER BY points LIMIT 5 OFFSET 5;
  ```
