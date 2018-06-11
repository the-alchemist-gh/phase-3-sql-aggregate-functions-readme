# SQL Aggregate Functions

## Overview

We'll cover basic aggregate functions and how to write SQL queries that utilize them.

## Objectives

1. Define aggregate functions and when to use them
2. Use the following aggregrate functions in SQL queries: `average`, `sum`, `count`, `minimum`, `maximum`

## Operating on Data

Imagine writing an application for a restaurant owner to track her customers and transactions, or an app that an e-commerce company uses to store users, transactions and shopping behaviors. Think about creating a social networking application whose administrators want to keep track of the number of times a user logs on and identify who their most frequent users are. It's easy to see that storing or persisting information in an application or program is about more than just keeping track of static data. We can imagine any number of situations in which we want to operate on or analyze the data we store. Our restaurant owner will want to discover who her biggest spenders are or what they make on average over a busy weekend. Our e-commerce company wants to know who their most frequent buyers are and how much they spend on average on a given item, and so on. 

We can do so using the aggregate functions that SQL makes available to us. With these functions we can sum and average column data, request minimum and maximum values, and more. SQL also makes available to use keywords that allow us to group aggregated data by various categories and narrow our search criteria based on various conditions. 

## Aggregate Functions

Aggregate functions perform a calculation on specified values, queried from a database table. We will cover the following aggregators here: 

* `AVG`
* `SUM`
* `COUNT`
* `MIN`
* `MAX`

We'll craft queries that select a desired set of values from a table and then aggregate that data using the above aggregators, in addition to clauses that will group and or order the returned data based on various conditions. 

For this walk-through, we'll be utilizing a database of pets and owners. 

## Setting up the Database

Some cats are very famous and, accordingly, very wealthy. Our pets database will have a cats table in which each cat has a name, age, breed, and net worth. 

**Creating the Database:**

Create the database in your terminal with the following: 

```bash
sqlite3 pets_database.db 
```

**Creating the table:**

In the `sqlite3>` prompt in your terminal:

```sql
CREATE TABLE cats (
  name TEXT,
  age INTEGER,
  breed TEXT, 
  net_worth INTEGER
);
```

**Inserting the values:**

```sql
INSERT INTO cats (name, age, breed, net_worth) VALUES ("Maru", 3, "Scottish Fold", 1000000);
INSERT INTO cats (name, age, breed, net_worth) VALUES ("Hana", 1, "Tabby", 21000);
INSERT INTO cats (name, age, breed, net_worth) VALUES ("Grumpy Cat", 4, "Persian", 181800);
INSERT INTO cats (name, age, breed, net_worth) VALUES ("Lil' Bub", 2, "Tortoiseshell", 3000000);
```

**Confirming our Data**

```sql
SELECT * FROM cats;
```

should return:

```
name             age         breed          net_worth 
---------------  ----------  -------------  ----------
Maru             3           Scottish Fold  1000000   
Hana             1           Tabby          21000    
Grumpy Cat       4           Persian        181800    
Lil' Bub         2           Tortoiseshell  3000000  
```

## Using Aggregators

### Code Along I: `AVG()`

The average, `AVG()`, function returns the average value of a column. Here's how it works: 

```sql
SELECT AVG(column_name) FROM table_name;
```

Let's write a query to grab the average net worth of our very lucrative cats. 

```sql
SELECT AVG(net_worth) FROM cats;
```

This should return: 

```
AVG(net_worth) 
---------------
1050700.0
```

That return value is a little ugly, however. Let's use the `AS` keyword to rename the column. This is called "aliasing the return value".

```sql
SELECT AVG(net_worth) AS average_net_worth FROM cats;
```

This should return: 

```
average_net_worth   
--------------------
1050700.0 
```

### Code Along II: `SUM()`

The sum, `SUM()`, function returns the sum of all of the values in a particular column. 

Here's how it works:

```sql
SELECT SUM(column_name) FROM table_name;
```

Let's try it out by calculating the sum of the net worths of all of our cats:

```sql
SELECT SUM(net_worth) FROM cats;
```

This should return: 

```
SUM(net_worth)      
--------------------
4202800   
```

### Code Along II: `MIN()` and `MAX()`

The minimum and maximum aggregator functions return the minimum and maximum values from a specified column respectively. 

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

```
MIN(net_worth)      
--------------------
21000   
```

### Code Along III: `COUNT()`

The count function returns the number of rows that meet a certain condition. 

Here's how it works:

```sql
SELECT COUNT(column_name) FROM table_name;
```

We can use the `COUNT()` function to calculate the total number of rows in a table that are not `NULL`. `NULL` means empty. All of our cats have a `name` so we can call `COUNT` on the name column like this:

```sql
SELECT COUNT(name) FROM cats;
```

This should return:

```
COUNT(name)            
--------------------
4
```

We have a total of four cats in our Cats table with a name. If we really didn't care about a specific column and we just wanted the total number of rows in our database we can call `COUNT(*)`. `*` means everything. Sometimes it's called the "wildcard." This `COUNT(*)` will count the rows where at least one column has data in it. 

We can also use `COUNT()` to count the total number of rows in a table that meet a certain criteria. Let's use this aggregator to count the number of cats whose net worth is greater than one million:

```sql
SELECT COUNT(*) FROM cats WHERE net_worth > 1000000;
```

This should return:

```
COUNT(*)            
--------------------
1    
```

Because only Lil' Bub is *that* rich. 

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/sql-aggregate-functions-readme'>SQL Aggregate Functions</a> on Learn.co and start learning to code for free.</p>
