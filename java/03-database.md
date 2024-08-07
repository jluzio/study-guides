# SQL
SQL stands for Structured Query Language  
SQL lets you access and manipulate databases  
SQL became a standard of the American National Standards Institute (ANSI) in 1986, and of the International Organization for Standardization (ISO) in 1987

Although SQL is an ANSI/ISO standard, there are different versions of the SQL language.

    SELECT - extracts data from a database
    UPDATE - updates data in a database
    DELETE - deletes data from a database
    INSERT INTO - inserts new data into a database
    CREATE DATABASE - creates a new database
    ALTER DATABASE - modifies a database
    CREATE TABLE - creates a new table
    ALTER TABLE - modifies a table
    DROP TABLE - deletes a table
    CREATE INDEX - creates an index (search key)
    DROP INDEX - deletes an index

## Examples

```sql
SELECT column1, column2, ...
FROM table_name;

SELECT DISTINCT column1, column2, ...
FROM table_name;

SELECT column1, column2, ...
FROM table_name
WHERE condition;

SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;

SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;

SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;

SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;

INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

SELECT column_names
FROM table_name
WHERE column_name IS NULL;

SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;

UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

DELETE FROM table_name WHERE condition;

SELECT TOP number|percent column_name(s)
FROM table_name
WHERE condition;

SELECT MIN(column_name)
FROM table_name
WHERE condition;

SELECT COUNT(column_name)
FROM table_name
WHERE condition;

SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;

SELECT * FROM Customers
WHERE City LIKE 'ber%';

SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);

SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;

SELECT column_name AS alias_name
FROM table_name;

SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;

SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;

SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;

SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;

SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;

SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);

SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);

SELECT column_name(s)
FROM table_name
WHERE column_name operator ANY
  (SELECT column_name
  FROM table_name
  WHERE condition);

SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;

INSERT INTO table2
SELECT * FROM table1
WHERE condition;

CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;

SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
FROM Products;

SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products;

-- statement
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
-> then ->
EXEC procedure_name;

```


## Joins
### INNER JOIN
The INNER JOIN keyword selects all rows from both the tables as long as the condition is satisfied. This keyword will create the result-set by combining all rows from both the tables where the condition satisfies i.e value of the common field will be the same. 

### LEFT JOIN
This join returns all the rows of the table on the left side of the join and matches rows for the table on the right side of the join. For the rows for which there is no matching row on the right side, the result-set will contain null. LEFT JOIN is also known as LEFT OUTER JOIN.

### RIGHT JOIN
RIGHT JOIN is similar to LEFT JOIN. This join returns all the rows of the table on the right side of the join and matching rows for the table on the left side of the join. For the rows for which there is no matching row on the left side, the result-set will contain null. RIGHT JOIN is also known as RIGHT OUTER JOIN.

### FULL JOIN
FULL JOIN creates the result-set by combining results of both LEFT JOIN and RIGHT JOIN. The result-set will contain all the rows from both tables. For the rows for which there is no matching, the result-set will contain NULL values.


## Other topics

### function vs procedure
- Functions return a value and can be used in a SQL statement or function, can be used in select statement.
- Procedures can have output parameters, but can only be used by EXECUTE, so it can't be used in a select statement for example.


### truncate table
Deletes all records, but doesn't drop table. (may delete rollback history?) (may reset sequences?).


### concurrency
- transactions (use a isolation level that fits: read uncommitted, read committed, etc)
- optimistic locking (version/timestamp field)
- pessimistic locking
- row-level locking
- partitioning (multiple tables, distributed and handled seperatelly)
- application logic
  - queueing to serialize access to critical parts of the code


### NoSQL vs SQL
NoSQL is preferred over SQL in many cases because it offers more flexibility and scalability.
The primary benefit of using a NoSQL system is that it provides developers with the ability to store and access data quickly and easily, without the overhead of a traditional relational database.


### Pagination
Example for Postgres.
https://readyset.io/blog/optimizing-sql-pagination-in-postgres

#### Offset and Limit Pagination
The single most important concept to understand when it comes to pagination in Postgres databases is the use of LIMIT and OFFSET clauses.

LIMIT specifies the maximum number of rows to be returned by a query, while OFFSET specifies the number of rows to skip before returning rows from the query result set.

Here's a simple example:
~~~sql
SELECT * FROM users ORDER BY id LIMIT 10 OFFSET 0;
~~~

Beyond getting consistently slower, or rather, because it gets consistently slower, this pagination technique can lead to consistent results with concurrent updates. The results may be inconsistent or missing if the underlying data is modified (e.g., rows inserted, updated, or deleted) between consecutive paginated queries.

Consider the following scenario:
~~~sql
Query 1: SELECT * FROM users ORDER BY id LIMIT 10 OFFSET 0;
Query 2: SELECT * FROM users ORDER BY id LIMIT 10 OFFSET 10;
~~~

If a new row is inserted or an existing row is deleted between these two queries, the second query may return unexpected results. Rows might be duplicated or skipped entirely.

This approach can also be inefficient with large result sets. When using LIMIT and OFFSET for pagination, the database still needs to generate the entire result set, even if only a small portion is returned to the application. This can be inefficient, especially for queries with complex joins or large result sets.

#### Cursor-based pagination
Cursor-based pagination relies on using a unique identifier or a timestamp of the last retrieved record as a reference point for fetching the next page of results. Instead of using OFFSET, you keep track of the previous retrieved record and use its identifier or timestamp in the WHERE clause to fetch the next set of records.

~~~sql
-- Fetch the first page
SELECT * FROM users WHERE id > 0 ORDER BY id LIMIT 10;

-- Fetch the next page
SELECT * FROM users WHERE id > <last_id_from_previous_page> ORDER BY id LIMIT 10;
~~~

Cursor-based pagination is more efficient than offset-based pagination because it avoids the need to scan and discard rows. Instead, it directly jumps to the next set of records based on the cursor value. This approach remains efficient even for large offsets because the database can quickly use an index on the cursor column to locate the starting point.

It also produces stable results. Cursor-based pagination provides stable results even if new records are inserted or deleted between page requests. Each page contains the expected set of records based on the cursor value.

Using cursor-based pagination, you should also see reduced database load. By avoiding the need to scan and discard records, cursor-based pagination reduces the database load and resource consumption compared to offset-based pagination.

There are considerations when implementing cursor-based pagination:
- Cursor stability: The cursor column must be unique and immutable. If the cursor value changes between page requests (e.g., due to updates), it can lead to inconsistent results.
- Sorting requirements: Cursor-based pagination relies on a specific sorting order to determine the next set of records. Ensure the query includes an appropriate ORDER BY clause based on the cursor column.
- Application-side tracking: The application needs to keep track of the cursor value for each page and use it to construct the subsequent queries. This adds some complexity to the application code.
- Deleted records: If records are deleted between page requests, cursor-based pagination may result in gaps in the paginated results. The page size may be less than the expected number of records.

#### Keyset pagination
Keyset pagination takes cursor-based pagination a step further by using a combination of columns to identify each record uniquely. Typically, the columns used for keyset pagination include the primary key and a timestamp or a monotonically increasing value.

~~~sql
-- Fetch the first page
SELECT * FROM users ORDER BY id, created_at LIMIT 10;

-- Fetch the next page
SELECT * FROM users
WHERE (id, created_at) > (<last_id_from_previous_page>, <last_timestamp_from_previous_page>)
ORDER BY id, created_at
LIMIT 10;
~~~

Here, we use the combination of id and created_at columns as the keyset. For the first page, we fetch the records ordered by id and created_at and limit the result to 10 rows. For subsequent pages, we use the id and created_at values of the last retrieved record from the previous page as the starting point and fetch the next set of records.

Keyset pagination ensures stable and consistent results even if new records are inserted, or existing records are modified between page requests. It guarantees that each record is uniquely identified and avoids the problem of skipped or duplicated records that can occur with offset-based pagination. However, we can’t jump to a specific page–we only have the option of going to the next page of results.

#### Materialized Views
Materialized views are a robust caching mechanism in Postgres. They allow you to store the result of a complex query as a separate table. Materialized views are particularly useful for caching paginated results of queries that involve expensive joins, aggregations, or complex filtering.

To create a materialized view for a paginated query:
~~~sql
CREATE MATERIALIZED VIEW paginated_users AS
SELECT * FROM users ORDER BY id LIMIT 1000;
~~~

This materialized view caches the first 1000 rows of the users table, ordered by the id column. Subsequent pagination queries can retrieve data from this materialized view instead of querying the main table.

To refresh the materialized view with the latest data:

~~~sql
REFRESH MATERIALIZED VIEW paginated_users;
~~~

#### Extensions (if aplicable)
Example for Readyset in Postgres.

Readyset is a caching engine that integrates seamlessly with Postgres. It sits between your application and the database as a distributed caching layer. Readyset automatically caches the results of paginated queries and keeps the cached data up to date with the underlying database.

Readyset offers several benefits for cache-aware pagination:
- Automatic caching: Readyset caches the results of paginated queries without requiring changes to your application code.
- Incremental updates: Readyset efficiently updates the cached data as the underlying database changes, ensuring data consistency.
- Seamless integration: Readyset is wire-compatible with Postgres, so you only need to switch out your connection string to start using Readyset in your application—no code changes required.


#### Notes
- Indexes: consider use indexes for the paging params and query params.


#### "Advanced Techniques"
1. Window Functions
Use window functions to provide more advanced pagination capabilities, such as total row count alongside the paginated results.
SELECT * FROM (
  SELECT
    data_table.*,
    ROW_NUMBER() OVER (ORDER BY timestamp DESC) as row_num
  FROM data_table
) AS subquery
WHERE row_num BETWEEN :start AND :end;

Memory and Performance Considerations:
- Window functions can be resource-intensive but are useful for cases where you need additional metadata about the results.
- Ensure proper indexing and consider database-specific optimizations to handle window functions efficiently.

2. Caching
Implement caching mechanisms to store frequently accessed pages, reducing the need to repeatedly query the database for the same data.

~~~js
import redis

cache = redis.Redis(host='localhost', port=6379)

def fetch_page(page_number, page_size):
    cache_key = f"page_{page_number}"
    cached_page = cache.get(cache_key)
    if cached_page:
        return json.loads(cached_page)

    # Calculate offset for LIMIT and OFFSET pagination
    offset = (page_number - 1) * page_size
    query = f"SELECT * FROM data_table ORDER BY timestamp DESC LIMIT {page_size} OFFSET {offset}"
    result = execute_query(query)

    # Cache the result
    cache.set(cache_key, json.dumps(result), ex=60)  # Cache for 60 seconds
    return result
~~~

Memory and Performance Considerations:
- Caching reduces the load on the database and improves response times for frequently accessed pages.
- Cache expiration policies should be designed based on the data update frequency to ensure data freshness.
