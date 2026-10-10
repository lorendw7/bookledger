# Lesson 02: SQL foundations

## Goal

Understand databases, tables, rows, columns, and constraints; then write the initial catalog scripts yourself. This lesson describes tasks and hints without supplying a complete BookLedger schema.

## Client and server

MySQL is the database server. Workbench and the `mysql` command-line client send SQL to it. Saving a `.sql` file in VS Code does not execute it. Follow [Getting started](../getting-started.md) and record the actual server version.

## Data structure

A database groups related tables. A table has named columns and records called rows. For example, a book record needs a title, price, and stock quantity. A column's data type defines the kinds of values it can store.

Generic diagnostics:

```sql
SELECT 1;
SELECT VERSION();
SELECT DATABASE();
```

`SELECT` requests results. A semicolon terminates a statement. `NULL` represents an absent/unknown value; it is different from zero and an empty string.

## Maintainer task: database

Write a script that creates the learning database when absent, explicitly selects `utf8mb4`, selects the database for the current connection, and displays its name. Explain rerun behavior. Hints: `CREATE DATABASE`, `IF NOT EXISTS`, `CHARACTER SET`, `USE`, and `DATABASE()`.

If your local database already exists, inspect it first. `IF NOT EXISTS` does not update an existing object's definition. The repository restart is not a database reset.

## Maintainer task: catalog

Design the first catalog table using [the proposal](../database-design.md) and [requirements](../requirements.md). Explain each choice rather than copying an unexplained schema.

- Use a primary key to identify a record. Automatic numbering and primary-key uniqueness have different responsibilities.
- Store money using an exact decimal type, documenting total digits, fractional digits, and currency.
- Store stock quantities as integers, and decide which constraint rejects negative values.
- Distinguish `NOT NULL`, meaningful text, defaults, and value checks.
- Introduce ISBN uniqueness and author metadata before declaring the catalog requirements complete.
- Select InnoDB for future transactions.

MySQL 8.0.16 and later enforce supported `CHECK` constraints. The observed 8.0.45 server supports them; verify actual rejection cases. `DECIMAL(p, s)` counts total digits with `p` and fractional digits with `s`. See the official references below.

## Maintainer task: queries

Create a separate synthetic-data script and query exercise file. Demonstrate insertion, selection, filtering, sorting, aggregation, an update, and deletion of a disposable fixture. Record whether rerunning a seed script duplicates data. State prerequisites and cleanup.

## Evidence

- Inspect the actual table definition, not only the source file.
- Show expected rows and observed results.
- Attempt an invalid record and document its rejection.
- Explain why duplicate titles need not mean duplicate editions.
- Explain why `NOT NULL` alone cannot prevent a negative number.

Save the evidence in [the progress log](../progress.md).

## Official references

- [Creating and selecting a database](https://dev.mysql.com/doc/refman/8.0/en/creating-database.html)
- [Creating a table](https://dev.mysql.com/doc/refman/8.0/en/creating-tables.html)
- [Exact decimal types](https://dev.mysql.com/doc/refman/8.0/en/fixed-point-types.html)
- [Automatic numbering](https://dev.mysql.com/doc/refman/8.0/en/example-auto-increment.html)
- [CHECK constraints](https://dev.mysql.com/doc/refman/8.0/en/create-table-check-constraints.html)
