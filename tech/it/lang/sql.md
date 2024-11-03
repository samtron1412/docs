# Overview

- Structured Query Language (SQL) is a domain-specific language used in
  programming and designed for managing data held in a relational
  database management system (RDBMS)
- https://en.wikipedia.org/wiki/SQL

# Styles

- https://www.sqlstyle.guide/
- https://docs.telemetry.mozilla.org/concepts/sql_style.html
- https://oracle.readthedocs.io/en/latest/sql/basics/style-guide.html
- https://about.gitlab.com/handbook/business-technology/data-team/platform/sql-style-guide/
- https://gist.github.com/mattmc3/38a85e6a4ca1093816c08d4815fbebfb
- https://github.com/mattm/sql-style-guide

Check style

- SQLfluff: https://github.com/sqlfluff/sqlfluff
- SQL lint: https://github.com/joereynolds/sql-lint
- https://www.jetbrains.com/help/idea/configure-the-sql-code-style.html

# CTE vs Temporary Table vs Table Variables

- https://www.mssqltips.com/sqlservertip/5118/sql-server-cte-vs-temp-table-vs-table-variable-performance-test/
- https://stackoverflow.com/questions/690465/which-are-more-performant-cte-or-temporary-tables
    + It depends on each query: for some CTE is more performant, but for
      others temporary tables are more performant.

## Common Table Expression (CTE) - WITH clause - Organize complex queries

- https://modern-sql.com/feature/with
- https://learnsql.com/blog/what-is-with-clause-sql/

```
WITH query_name1 AS (
     SELECT ...
     )
   , query_name2 AS (
     SELECT ...
       FROM query_name1
        ...
     )
SELECT ...
```

# Unit tests

- https://dataform.co/blog/unit-tests
- https://www.sqlshack.com/sql-unit-testing-best-practices/

# Joins

- https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join
- LEFT [OUTER] JOIN vs INNER JOIN
    + LEFT JOIN == LEFT OUTER JOIN
    + INNER JOIN results contain rows that have pair on both sides
    + The result of LEFT JOIN shall be the same as the result of INNER
      JOIN + we’ll have rows, from the “left” table, without a pair in
      the “right” table. (values that don't exist in the right table are
      set to NULL)
    + You’ll use INNER JOIN when you want to return only records having
      pair on both sides, and you’ll use LEFT JOIN when you need all
      records from the “left” table, no matter if they have pair in the
      “right” table or not.
- CROSS JOIN
    + If you’ll need all records from both tables, no matter if they
      have pair.

## Inner Join

```
SELECT table1.column1,table1.column2,table2.column1,....
FROM table1
INNER JOIN table2
ON table1.matching_column = table2.matching_column;
```

- Select all columns from the first tables

```
SELECT nutrients.*, measures.colX
FROM nutrients
LEFT JOIN measures ON nutrients.name=measures.name
```

# RANK vs. DENSE_RANK vs. ROW_NUMBER

- https://stackoverflow.com/questions/7747327/sql-rank-versus-row-number
- https://stackoverflow.com/questions/64420584/when-to-choose-rank-over-dense-rank-or-row-number

# Best practices

- Don't `SELECT *` and aggregate or join or order by
    + Even if you LIMIT your results, the other statements will force
      all rows to be considered.
- Use WHERE clauses reduce the total number of rows considered
- Constrain/filter the dataset by date, region id, etc.
- Don't use WITH statements if they can be avoided. Use TEMP tables
  instead
- Use a CASE expression to perform complex aggregations
- Add predicates to your Join tables

# NoSQL

- https://www.youtube.com/watch?v=ruz-vK8IesE

# Tips and tricks

## Double Quotes vs. Single Quotes

- https://stackoverflow.com/questions/1992314/what-is-the-difference-between-single-and-double-quotes-in-sql

```
[S]ingle quotes are for [S]trings Literals (date literals are also strings);
[D]ouble quotes are for [D]atabase Identifiers (table names, column names);
```

## 1=1 condition

- https://pushmetrics.io/blog/why-use-where-1-1-in-sql-queries-exploring-the-surprising-benefits-of-a-seemingly-redundant-clause
- Serve as stating point in dynamic SQL query generation
- Allow us to commenting out conditions as needed
- Template queries.
- Readability: focus on other conditions

```
SELECT *
FROM employees
WHERE 1=1
-- AND department_id = 3
-- AND salary > 50000;
```

## Select the max date

- https://stackoverflow.com/questions/16550703/sql-get-the-last-date-time-record

```
select filename ,
       status   ,
       max_date = max( dates )
from some_table t
group by filename , status
having status = '<your-desired-status-here>'
```

```
SELECT * FROM table
WHERE Dates IN (SELECT max(Dates) FROM table);
```

```
SELECT TOP 1 * FROM foo ORDER BY Dates DESC
Will return one result with the latest date.

SELECT * FROM foo WHERE foo.Dates = (SELECT MAX(Dates) FROM foo)
Will return all results that have the same maximum date, to the milissecond.
```
