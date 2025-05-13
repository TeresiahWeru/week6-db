# week6-db

SQL Joins and Database Relationships
In relational databases, relationships between tables are established to avoid data redundancy and maintain data integrity.  SQL JOIN clauses are used to query data from multiple tables based on these relationships.

Database Relationships
One-to-One: Each record in one table is related to one, and only one, record in another table.

Example: A users table and a profiles table, where each user has one profile, and each profile belongs to one user.

One-to-Many: One record in a table is related to many records in another table.

Example: A customers table and an orders table, where a customer can have multiple orders, but each order belongs to only one customer.

Many-to-Many: Many records in one table are related to many records in another table.  This is typically implemented using a junction table.

Example: A students table and a courses table, where a student can enroll in many courses, and a course can have many students.  A junction table like enrollments would store the student_id and course_id.

SQL JOINs
SQL JOIN clauses are used to combine rows from two or more tables based on a related column between them.

1.  INNER JOIN

Returns only the rows that have matching values in both tables.

SELECT orders.order_id, customers.customer_name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.customer_id;

2.  LEFT JOIN (or LEFT OUTER JOIN)

Returns all rows from the left table, and the matching rows from the right table.  If there's no match in the right table, NULL values are returned for the right table's columns.

SELECT customers.customer_name, orders.order_id
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id;

3.  RIGHT JOIN (or RIGHT OUTER JOIN)

Returns all rows from the right table, and the matching rows from the left table.  If there's no match in the left table, NULL values are returned for the left table's columns.

SELECT orders.order_id, customers.customer_name
FROM orders
RIGHT JOIN customers ON orders.customer_id = customers.customer_id;

4.  FULL OUTER JOIN

Returns all rows from both tables.  If there are no matching rows, NULL values are returned for the columns of the table that doesn't have a match.

SELECT customers.customer_name, orders.order_id
FROM customers
FULL OUTER JOIN orders ON customers.customer_id = orders.customer_id;

5.  CROSS JOIN

Returns the Cartesian product of the rows from both tables.  Every row from the first table is combined with every row from the second table.  It does not require a join condition.

Use with caution, as it can produce very large result sets.

SELECT customers.customer_name, products.product_name
FROM customers
CROSS JOIN products;

Join Conditions
The ON clause specifies the relationship between the tables.  It indicates which columns should be used to match rows.

The most common type of join condition is an equality condition, where the values in the specified columns must be equal (e.g., orders.customer_id = customers.customer_id).

Aliases
Table aliases can be used to shorten table names in a query, making it more readable, especially when joining multiple tables.

SELECT c.customer_name, o.order_id
FROM customers AS c
INNER JOIN orders AS o ON c.customer_id = o.customer_id;
