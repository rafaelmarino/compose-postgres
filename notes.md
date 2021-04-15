# Notes on Postgres

## Sorting

Based on UTF-8, PostgreSQL sorts characters in this
order:
1. Punctuation marks, including quotes, parentheses, and math
operators
2. Numbers 0 to 9
3. Additional punctuation, including the question mark
4. Capital letters from A to Z
5. More punctuation, including brackets and underscore
6. Lowercase letters a to z
7. Additional punctuation, special characters, and the extended
alphabet

## Pattern Matching

1) The LIKE operator, which is part of the ANSI SQL standard, is case sensitive
2) The ILIKE operator, which is a PostgreSQL-only implementation, is case insensitive
3) Percent sign ( `%` ) A wildcard matching one or more characters
4) Underscore ( `_`) A wildcard matching just one character

## Indexing Watchout

Even though a column with a serial type auto-increments each time a row is
added, some scenarios will create gaps in the sequence of numbers in the
column. If a row is deleted, for example, the value in that row is never
replaced. Or, if a row insert is aborted, the sequence for the column will still
be incremented.

## Primary Key

A **primary key** is a column or collection of columns whose values uniquely identify each row in a table. A valid primary key column enforces certain constraints:

1. The column or collection of columns must have a unique value for each row.
2. The column or collection of columns can’t have missing values.

NOTE: Primary key values only need to be unique within a table.

## Foreign Key

A **foreign key** is a column or collection of columns that constitute primary keys in another table. A foreign key constraint requires a value entered in a column to already exist in the  primary key of the table it references.
Unlike a primary key, a foreign key column can be empty, and it can contain duplicate values.

## Constraints

The `UNIQUE` constraint guarantees that values in a column, or a combination of values in more than one column, are unique.

## Joins

When you join tables in a query, the database connects rows in both
tables where the columns you specified for the join have matching values.
The query results then include columns from both tables if you requested
them as part of the query. You also can use columns from the joined
tables to filter results using a `WHERE` clause.

### (Inner) Join

We use `JOIN`, or `INNER JOIN`, when we want to return rows that have a match
in the columns we used for the join. Only rows that match in both tables are kept. Watchout for this join as there may be unintended loss of data. 

### Left Join and Right Join

In contrast to `JOIN`, the `LEFT JOIN` and `RIGHT JOIN` keywords each return all
rows from one table (left table if `LEFT JOIN`; right table if `RIGHT JOIN`) and display blank rows from the other table if no matching values are found in the joined columns.

### Full Outer Join

When you want to see all rows from both tables in a join, regardless of
whether any match, use the `FULL OUTER JOIN` option. A full outer join is admittedly less useful and used less often than inner and left or right joins. Still, you can use it for a couple of tasks: to merge two data sources that partially overlap or to visualize the degree to which the tables share matching values.

### Cross Join

In a `CROSS JOIN` query, the result (also known as a Cartesian product) lines up
each row in the left table with each row in the right table to present all
possible combinations of rows. Because the join doesn’t need to find matches between key fields, there’s no need to provide the clause using the `ON` keyword.

## NULLs

In SQL, `NULL` is a special value that represents a condition in which
there’s no data present or where the data is unknown because it wasn’t
included. A `NULL` is distinctively different from a `0` or `""`. A `NULL` represents absence of evidence---and not evidence of absence.

## Relationships

### One-to-One Relationship

There is only one match for an id in each of the two tables. In addition, there are no duplicate id values in either table: only one row in the left table exists with an id of 1, and only one row in the right table has an id of 1. Eg. Each State contains one Governor. 

### One-to-Many Relationship

A key value in the first table will have multiple matching values in the second table’s joined column. Eg. Each State contains multiple Counties.

### Many-to-Many Relationship

Multiple rows in the first table will have multiple matching rows in the second table. Eg. Students and classes: a student can register for many classes, and a class can include many students.

## Constraints

We can add constraints in two ways: as a column constraint or as a table
constraint. A column constraint only applies to that column. It’s declared
with the column name and data type in the `CREATE TABLE` statement, and it
gets checked whenever a change is made to the column. With a table
constraint, we can supply criteria that apply to one or more columns. We
declare it in the `CREATE TABLE` statement immediately after defining all the
table columns, and it gets checked whenever a change is made to a row in
the table.