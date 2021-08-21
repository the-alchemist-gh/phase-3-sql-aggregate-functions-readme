# Aggregate Functions

## Learning Goals

- Define aggregate functions and when to use them
- Use the following aggregate functions in SQL queries: `average`, `sum`,
  `count`, `minimum`, `maximum`

## Introduction

We'll cover basic aggregate functions and how to write SQL queries that utilize them.

[Fork and clone this lesson](https://github.com/learn-co-curriculum/phase-3-sql-aggregate-functions-readme/fork) to code along.

## Operating on Data

Imagine writing an application for a restaurant owner to track her customers and
transactions, or an app that an e-commerce company uses to store users,
transactions and shopping behaviors. Think about creating a social networking
application whose administrators want to keep track of the number of times users
log on to identify who their most frequent users are.

It's easy to see that storing or persisting information in an application or
program is about more than just keeping track of static data. We can imagine any
number of situations in which we want to operate on or analyze the data we
store. Our restaurant owner will want to discover who her biggest spenders are
or what they make on average over a busy weekend. Our e-commerce company wants
to know who their most frequent buyers are and how much they spend on average on
a given item, and so on.

We can do so using the aggregate functions that SQL makes available to us. With
these functions we can sum and average column data, request minimum and maximum
values, and more. SQL also includes keywords that allow us to group aggregated
data by various categories and narrow our search criteria based on various
conditions.

## Using Aggregate Functions

Aggregate functions perform a calculation on specified values, queried from a
database table. We will cover the following aggregators here:

- `AVG`
- `SUM`
- `COUNT`
- `MIN`
- `MAX`

We'll craft queries that select a desired set of values from a table and then
aggregate that data using the above aggregators, in addition to clauses that
will group and/or order the returned data based on various conditions.

For this walk-through, we'll be utilizing a database of pets once more.

For the rest of this code along, you can run the SQL commands one of two ways,
depending on your preference.

You can either open the database using the `sqlite3` CLI, and run the SQL
commands from the terminal:

```sh
sqlite3 pets_database.db
```

Or you can open the `pets_database.db` file in DB Browser for SQLite, and run
the SQL commands from the "Execute SQL" tab.

## Using Aggregators

### Code Along 1: `AVG()`

The average, `AVG()`, function returns the average value of a column. Here's how
it works:

```sql
SELECT AVG(column_name) FROM table_name;
```

Let's write a query to grab the average net worth of our very lucrative cats.

```sql
SELECT AVG(net_worth) FROM cats;
```

This should return:

```txt
AVG(net_worth)
---------------
1050700.0
```

That return value is a little ugly, however. Let's use the `AS` keyword to
rename the column. This is called "aliasing the return value".

```sql
SELECT AVG(net_worth) AS average_net_worth FROM cats;
```

This should return:

```txt
average_net_worth
--------------------
1050700.0
```

### Code Along 2: `SUM()`

The sum, `SUM()`, function returns the sum of all of the values in a particular
column.

Here's how it works:

```sql
SELECT SUM(column_name) FROM table_name;
```

Let's try it out by calculating the sum of the net worths of all of our cats:

```sql
SELECT SUM(net_worth) FROM cats;
```

This should return:

```txt
SUM(net_worth)
--------------------
4202800
```

### Code Along 3: `MIN()` and `MAX()`

The minimum and maximum aggregator functions return the minimum and maximum
values from a specified column respectively.

Here's how it works:

```sql
SELECT MIN(column_name) FROM table_name;
SELECT MAX(column_name) FROM table_name;
```

Let's try it out:

```sql
SELECT MIN(net_worth) FROM cats;
```

This should return:

```txt
MIN(net_worth)
--------------------
21000
```

### Code Along 4: `COUNT()`

The count function returns the number of rows that meet a certain condition.

Here's how it works:

```sql
SELECT COUNT(column_name) FROM table_name;
```

We can use the `COUNT()` function to calculate the total number of rows in a
table that are not `NULL`. `NULL` means empty. All of our cats have a `name` so
we can call `COUNT` on the name column like this:

```sql
SELECT COUNT(name) FROM cats;
```

This should return:

```txt
COUNT(name)
--------------------
4
```

We have a total of four cats in our Cats table with a name. If we really didn't
care about a specific column and we just wanted the total number of rows in our
database we can call `COUNT(*)`. `*` means everything. Sometimes it's called the
"wildcard." This `COUNT(*)` will count the rows where at least one column has
data in it.

We can also use `COUNT()` to count the total number of rows in a table that meet
a certain condition. Let's use this aggregator to count the number of cats whose
net worth is greater than one million:

```sql
SELECT COUNT(*) FROM cats WHERE net_worth > 1000000;
```

This should return:

```txt
COUNT(*)
--------------------
1
```

Because only Lil' Bub is _that_ rich.
