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

# Unit tests

- https://dataform.co/blog/unit-tests
- https://www.sqlshack.com/sql-unit-testing-best-practices/

# Joins

- https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join
- Left Join vs Inner Join
    + INNER JOIN results contain rows that have pair on both sides
    + The result of LEFT JOIN shall be the same as the result of INNER
      JOIN + we’ll have rows, from the “left” table, without a pair in
      the “right” table. (values that don't exist in the right table are
      set to NULL)
    + You’ll use INNER JOIN when you want to return only records having
      pair on both sides, and you’ll use LEFT JOIN when you need all
      records from the “left” table, no matter if they have pair in the
      “right” table or not.
- Cross Join
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

# Tips and tricks

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
