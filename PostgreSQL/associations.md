# PostgreSQL Associations

## General

- Modeling Associations
  - authors and articles
  - owners and cars
  - owners and pets
  - parent and children
  - albums and artists
  - projects and contributors
  - classes and objects
  
- Types of Associations
  - One-to-many
    - One author and multiple articles
  - Many-to-many
    - Many albums and many artists

- Determine Associations
  - Can X have multiple Y's?
  - Can Y have multiple Y's?
  - What kind of info is needed to determine the association

### Examples

- Authors and Articles
  - Can 1 author have many articles?
    - Yes
  - Can 1 article have many authors?
    - Yes
    
- Groups and Members
  - Can 1 group have many members?
    - Yes
  - Can 1 member belong to many groups?
    - Yes

- More Examples
  - People and legs
    - 1 person has 2 legs
    - 2 legs belong to 1 person
  - People and homes
    - 1 person can have multiple homes
    - 1 home can have multiple people
  - Company and employees
    - 1 company can have many employees
    - 1 employee (usually) only works at 1 company
  - Team and players
    - 1 team has multiple players
    - Players can only belong to 1 team
  - Facebook groups and members
    - 1 facebook group can have multiple members
    - 1 member can belong to multiple groups

## Representing One-to-Many

- **Foreign Key**
  - Key used to link two tables together
    - A **foreign key** is a field(s) that references the primary key in another table.
    - The table containing the candidate key is the referenced or **parent table**.
    - The table that inherits the foreign key from the parent table is the **child table**.
  - e.g.
  ```sql
  CREATE TABLE author (
    id SERIAL PRIMARY KEY,
    name VARCHAR
  );
  
  CREATE TABLE article (
    id SERIAL PRIMARY KEY,
    title VARCHAR,
    author_id INTEGER REFERENCES author (id)
  );
  ```
  
### Joins

- [Venn Diagram illustration](https://i.stack.imgur.com/qje6o.png)

- **Inner Join**
  - Keyword that selects records with matching values from two specified tables.
    - Everything that intersects in a venn diagram.
  - Syntax
    ```sql
    SELECT attribute
    FROM table1
    INNER JOIN table2 ON table1.attribute = table2.attribute;
    ```
    - Explicitly joins table1 to table2 on the specified condition
  - e.g.
    ```sql
    SELECT * FROM article INNER JOIN author 
    ON article.author_id = author.id;
    
    -- OR
    
    SELECT * FROM article, author
    WHERE article.author_id = author.id;
    ```

- **Outer Join**
  - Keyword that returns all rows from both selected tables which satisfy the join condition along with rows that do not satisfy the condition.
    - Everything that doesn't intersect in a venn diagram.
  - e.g.
    ```sql
    SELECT * FROM article
      LEFT OUTER JOIN author
        ON article.author_id = author.id;
    ```
    ```sql
    SELECT * FROM article
      RIGHT OUTER JOIN author
        ON article.author_id = author.id;
    ```
    ```sql
    SELECT * FROM article
      FULL OUTER JOIN author
    ```
    
- Representing Many-to-Many
  - Add an associative table in the middle, and it will link to each side as a many-to-one association.
  - e.g.
    ```sql
    CREATE TABLE team (
      id SERIAL PRIMARY KEY,
      name VARCHAR
    );
    CREATE TABLE member (
      id SERIAL PRIMARY KEY,
      name VARCHAR
    );
    CREATE TABLE team_member (
      id SERIAL PRIMARY KEY,
      team_id INTEGER REFERENCES team (id),
      member_id INTEGER REFERENCES member (id)
    );
    ```
  - Querying Many-to-Many
    ```sql
    SELECT * FROM member
    JOIN team_member ON team_member.member_id = member.id
    JOIN team ON team_member.team_id = team.id;
    ```
