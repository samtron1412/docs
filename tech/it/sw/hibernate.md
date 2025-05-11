# Overview

- https://www.tutorialspoint.com/hibernate/hibernate_quick_guide.htm
- https://www.geeksforgeeks.org/hibernate-architecture/
- https://www.baeldung.com/hibernate-one-to-many
- Inheritance Mapping
    + https://www.baeldung.com/hibernate-inheritance

# Hibernate Query Language (HQL) / Java Persistence Query Language (JPQL) vs. Native SQL Queries

- `createQuery()` (HQL/JPQL) object-oriented query languages
    + Working with objects rather than columns
- `createSQLQuery()` native SQL queries
    + more performant

- Both are safe if using parameterized queries (`:parameterName` or
  `?1`) against SQL injection.

# Troubleshooting

## composite keys cannot contain null

- Hibernate will maps records in database to null objects in memory if
  the record contains `null` values in any of they composite key
  columns.
    + No exceptions are thrown for this!
- https://stackoverflow.com/questions/70909/hibernate-mapping-a-composite-key-with-null-values
