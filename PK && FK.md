## PRIMARY KEY AND FOREIGN KEY
***Primary Key***
A *primary key* is a column or a group of columns that uniquely identifies each row in a table. You must define a primary key for each table and ensure that the primary key columns contain unique values. The primary key columns cannot contain NULL values and if a column is defined with the *PRIMARY KE*Y constraint, it's automatically defined as *NOT NULL*.
If the primary key consists of one column, you can define it as follows:

    CREATE TABLE table_name (
    pk_column data_type PRIMARY KEY
    );
If the primary key consists of multiple columns, you can define it as follows:

    CREATE TABLE table_name (
    pk_column1 data_type,
    pk_column2 data_type,
    ...
    PRIMARY KEY (pk_column1, pk_column2, ...)
    );

The following statement creates a new table named candidates with the id column as the primary key:

    CREATE TABLE candidates (
    id INT PRIMARY KEY,
    fullname VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(20) NOT NULL,
    );
The following statement creates a new table named employees with the id and email columns as the primary key:

    CREATE TABLE employees (
    id INT,
    email VARCHAR(255),
    fullname VARCHAR(255) NOT NULL,
    PRIMARY KEY (id, email)
    );

 ***SQL Server Foreign Key***
A *foreign key* is a column or a group of columns in a table that reference the primary key of another table. The table **containing the foreign key is called the child table**, and the table **containing the candidate key is called the referenced or parent table**.
To create a foreign key, you use the *FOREIGN KEY* constraint as follows:

    CREATE TABLE child_table (
    ...
    FOREIGN KEY (fk_columns) REFERENCES parent_table(pk_columns)
    );
The *foreign key* allows you to enforce the referential integrity constraints such as update and delete behaviors. For example, you can define the foreign key constraint that if a row in the parent table is deleted, the corresponding rows in the child table will be automatically deleted. This is called the cascade delete referential action.

    FOREIGN KEY(fk_columns) REFERENCES parent_table(pk_columns)
    ON DELETE CASCADE
    ON UPDATE CASCADE

There are more referential actions that you can use to define the foreign key constraint. The following  illustrates the referential actions:
*Referential Action Description*

 - [ ] CASCADE Delete or update the row from the parent table and automatically delete or update the matching rows in the child table. Both ON DELETE CASCADE and ON UPDATE CASCADE are supported. Between two tables, do not define several ON UPDATE CASCADE clauses that act on the same column in the parent table or in the child table.
 - [ ] SET NULL Set the column in the child table to NULL when the corresponding row in the parent table is deleted or updated. Both ON DELETE SET NULL and ON UPDATE SET NULL clauses are supported.
 - [ ] RESTRICT Rejects the delete or update operation for the parent table. Specifying RESTRICT (or NO ACTION) is the same as omitting the ON DELETE or ON UPDATE clause.
 - [ ] NO ACTION Specifying NO ACTION means that if the corresponding row in the parent table is deleted or updated, the action is rejected. NO ACTION is the same as RESTRICT.

***SQL Server Foreign Key Example***
Let’s take a look at the following example of creating a foreign key constraint for the employees table:
The following statement creates tables named departments and employees:

    CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL
    );

    CREATE TABLE employees (
    id INT PRIMARY KEY,
    email VARCHAR(255),
    fullname VARCHAR(255) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(id)
    );

In this example, the *department_id column in the employees table is the foreign key that references to the id column in the departments table*.
