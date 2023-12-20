

## ***SQL JOINS***

Let's have two tables, hr.candidates and hr.employees and call the candidates table as the left table and the employees table as the right table. The left table is the one that is listed first in the FROM clause. The right table is the one that is listed second in the FROM clause.
*Join is an SQL clause used to query and access data from two or more tables based on the logical relationships between the tables.*
***Types of SQL Joins***

 - Inner Join 
 - Left Outer Join 
 - Right Outer Join 
 - Full Outer Join 
 - Cross Join

## ***SQL Server Inner Join***

Inner join produces a dataset that includes rows from the left table, matching rows from the right table. The syntax for the inner join is as follows:

    SELECT column_list
    FROM left_table
    INNER JOIN right_table ON join_predicate;

The *join predicate* defines the logical relationship between the tables. The join predicate can be any expression that evaluates to true or false. If the join predicate evaluates to true, the inner join returns a row that contains columns from both tables specified in the **SELECT** clause.
*SQL Server Inner Join Example*

    SELECT
	    c.id candidate_id,
	    c.fullname candidate_name,
	    e.id employee_id,
	    e.fullname employee_name
    FROM
	    hr.candidates c
	    INNER JOIN hr.employees e
    ON e.fullname = c.fullname;

In this example, we joined the candidates table with the employees table using the inner join clause. The join predicate is *e.fullname = c.fullname*. It means that the inner join *returns a row if the fullname column in the employees table is equal to the fullname column in the candidates table*.

*SQL Server Inner Join Multiple Tables*
You can join more than two tables using the inner join clause. The following statement joins the candidates, employees, and departments tables.

    SELECT
	    c.id candidate_id,
	    c.fullname candidate_name,
	    e.id employee_id,
	    e.fullname employee_name,
	    d.name department_name
    FROM
	    hr.candidates c
	    INNER JOIN hr.employees e
	    ON e.fullname = c.fullname
	    INNER JOIN hr.departments d
    ON d.id = e.department_id;
In this example, we joined the candidates table with the employees table first. Then, we joined the result set with the departments table.

## ***SQL Server Left Join / Left Outer Join***

Left join returns *all the rows from the left table and matching rows from the right ta*ble. If a row in the left table does not have any matching row in the right table, the columns of the right table will have nulls.

*SQL Server Left Join Syntax*

    SELECT column_list
    FROM left_table
    LEFT JOIN right_table ON join_predicate;

SQL Server Left Join Example

    SELECT
	    c.id candidate_id,
	    c.fullname candidate_name,
	    e.id employee_id,
	    e.fullname employee_name
    FROM
	    hr.candidates c
	    LEFT JOIN hr.employees e
    ON e.fullname = c.fullname;
In this example, we joined the candidates table with the employees table using the left join clause. The join predicate is *e.fullname = c.fullname*. It means that the left join returns a row if the fullname column in the employees table is equal to the fullname column in the candidates table.
You can also add a where clause to get the rows that are available in the left table only.

    SELECT
	    c.id candidate_id,
	    c.fullname candidate_name,
	    e.id employee_id,
	    e.fullname employee_name
    FROM
	    hr.candidates c
	    LEFT JOIN hr.employees e
	    ON e.fullname = c.fullname
    WHERE
	    e.id IS NULL;
SYNTAX: 

    SELECT column_list FROM left_table LEFT JOIN right_table ON join_predicate WHERE condition;

## ***SQL Server Right Join / Right Outer Join***

Right join returns *all the rows from the right table and matching rows from the left table*. If a row in the right table does not have any matching row in the left table, the columns of the left table will have nulls. The right join is the reverse of the left join.

*SQL Server Right Join Syntax*

    SELECT column_list
    FROM left_table
    RIGHT JOIN right_table ON join_predicate;
    SQL Server Right Join Example

    SELECT
	    c.id candidate_id,
	    c.fullname candidate_name,
	    e.id employee_id,
	    e.fullname employee_name
    FROM
	    hr.candidates c
	    RIGHT JOIN hr.employees e
    ON e.fullname = c.fullname;
In this example, we joined the candidates table with the employees table using the right join clause. The join predicate is *e.fullname = c.fullname*. It means that the right join returns a row if the fullname column in the employees table is equal to the fullname column in the candidates table.
You can also add a where clause to get the rows that are available in the right table only.

    SELECT
	    c.id candidate_id,
	    c.fullname candidate_name,
	    e.id employee_id,
	    e.fullname employee_name
    FROM
	    hr.candidates c
	    RIGHT JOIN hr.employees e
    ON e.fullname = c.fullname
    WHERE
	    c.id IS NULL;

SYNTAX: 

    SELECT column_list FROM left_table RIGHT JOIN right_table ON join_predicate WHERE condition;

## ***SQL Server Full Outer Join***

The full outer join returns *all rows from both tables*. If a row in the left table does not have any matching row in the right table, the columns of the right table will have nulls. If a row in the right table does not have any matching row in the left table, the columns of the left table will have nulls.
*SQL Full Outer Join is a combination of Left Outer Join and Right Outer Join.*
*SQL Server Full Outer Join Syntax*

    SELECT column_list
    FROM left_table
    FULL OUTER JOIN right_table ON join_predicate;
The outer keyword is optional. You can use the full join instead of the full outer join.

    SELECT column_list FROM left_table FULL JOIN right_table ON join_predicate;

