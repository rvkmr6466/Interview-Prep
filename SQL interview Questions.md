# SQL interview questions

## Q. What are procedures and functions in SQL?
In SQL, both stored procedures and functions are reusable blocks of code used to perform specific tasks, but they differ in their purpose and behavior. Procedures are primarily used for data manipulation and can be called to execute a set of SQL statements, potentially changing the database. Functions, on the other hand, are designed for calculations and always return a single value, making them suitable for operations like data transformation or retrieving computed values.  
Key Differences:  

* Purpose:  
  * Procedures: Primarily for data manipulation (e.g., inserting, updating, deleting data).
  * Functions: Primarily for calculations and returning a single value.

* Return Value:  
	* Procedures: Can return multiple values, a single value, or no value at all. They can modify the database data.  
	* Functions: Always return a single value.

* Usage:
	* Procedures: Can be called directly or indirectly through other procedures or SQL statements.  
	* Functions: Can be used within SQL statements, including SELECT, INSERT, UPDATE, and DELETE.  

* Data Modification:
	* Procedures: Can modify data in the database (e.g., using DML statements like INSERT, UPDATE, DELETE).
	* Functions: Generally, they cannot modify data in the database.  

* Example:
	* Procedure: A procedure might be used to update product inventory levels when a sale occurs.  
	* Function: A function might be used to calculate the total cost of items in a shopping cart.

---
## Q. What are views and temporary tables in SQL?
In database management, both views and temporary tables offer ways to present and work with data without storing it physically in the main database tables, but they differ in their persistence and usage. Views are virtual representations of data, reflecting the latest underlying data changes, while temporary tables store a copy of data within a specific session and are deleted when that session ends. [1, 2]  

* **Views**:
  * _Virtual Representations_: Views are not actual data storage; they are like virtual tables based on SQL queries.
  * _Dynamic Updates_: When a view is accessed, the data is retrieved from the underlying tables, ensuring it reflects the latest changes.
  * _Abstraction_: Views can hide complex table structures or data transformations, providing a simplified interface for users or applications.
  * _Security_: Views can be used to restrict access to specific columns or rows, improving security.
  * _Reusability_: Views can be used multiple times in different queries or stored procedures, saving time and effort.
  * _Persistence_: Views persist until they are explicitly dropped or the database is altered. [1, 3]  

* **Temporary Tables**:
  * _Data Storage_: Temporary tables physically store data, similar to regular tables, but within a temporary storage area (often the tempdb database).
  * _Session-Based_: Temporary tables are created and exist only for the duration of the database session in which they were created.
  * _Data Copy_: A temporary table holds a copy of the data, and it is not synchronized with the underlying tables.
  * _Multi-Step Operations_: Temporary tables are often used to store intermediate results in multi-step queries or procedures, improving efficiency and reducing the need to repeatedly execute complex queries.
  * _Performance_: Temporary tables can improve performance by avoiding repeated execution of complex queries or by allowing the use of indexes on the temporary data.
  * _Explicit Management_: Temporary tables can be created, altered, and dropped explicitly, providing greater control.

**Key Differences:** 

| Feature | View | Temporary Table  |
| --- | --- | --- |
| Data Storage | Virtual (not physically stored) | Physically stored (in tempdb)  |
| Persistence | Persists across sessions | Limited to the current session  |
| Data Synchronization | Reflects latest data in underlying tables | Does not synchronize with underlying tables  |
| Use Cases | Abstraction, reusability, security | Intermediate data storage, performance  |

---
## Q. How do you optimize SQL queries?
To optimize SQL queries, focus on efficient indexing, minimizing data retrieval, and optimizing join operations. Avoid `SELECT *` and use `UNION ALL` instead of `UNION` for better performance. Also, consider database-specific features like partitioning and stored procedures.

* **Elaboration:**
 * _Indexing_: Create indexes on columns frequently used in `WHERE`, `JOIN`, `ORDER BY`, and `GROUP BY` clauses. Indexes act like an index in a book, allowing the database to quickly locate specific data.
 * _Data Retrieval_: Avoid fetching unnecessary data by specifying only the required columns in the `SELECT` statement and limiting the amount of data retrieved. This reduces network traffic and improves query speed.
 * _Join Optimization_: Choose appropriate join types (e.g., `INNER JOIN` instead of `OUTER JOIN` when possible) and optimize the order of joins to minimize the number of tables involved in a single query.
 * _Subqueries_: Minimize the use of subqueries as they can impact performance. Consider using `JOIN` or `EXISTS` instead of `IN` for subqueries.
 * _Database-Specific Features_: Utilize database-specific features like partitioning (splitting data into smaller, more manageable chunks) and stored procedures (pre-compiled SQL code that can be executed more efficiently).
 * _Other Techniques_: Use `UNION ALL` instead of `UNION` when you don't need to remove duplicate rows. Optimize `WHERE` clauses by avoiding functions in predicates and using the `LIKE` operator with wildcards at the end of a string.
 * _Monitoring_: Regularly monitor query performance to identify bottlenecks and optimize queries accordingly.

---
## Q. Second Highest Salary in SQL  
```sql
SELECT salary FROM employees ORDER BY salary DESC LIMIT 1 OFFSET 1;
```

---
## Q. 
