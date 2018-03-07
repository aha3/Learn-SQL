# Working with Multiple Tables
In this lesson, we'll learn the SQL commands that will help us work with data that is stored in multiple tables.

## Introduction

In order to efficiently store data, we often spread related information across multiple tables.
For instance, imagine that we're running a magazine company where users can have different types of subscriptions to different products. Different subscriptions might have many different properties. Each customer would also have lots of associated information.
We could have one table with all of the following information:

•	order_id

•	customer_id

•	customer_first_name

•	customer_last_name

•	customer_address

•	subscription_id

•	subscription_description

•	subscription_length

•	subscription_monthly_price

•	purchase_date

However, a lot of this information would be **repeated**. 
If the same customer has multiple subscriptions, that customer's name and address will be reported multiple times. 
If the same subscription type is ordered by multiple customers, then the subscription price and subscription description will be repeated. 
This will **make our table big and unmanageable**.

So instead, we can split our data into three tables:

•	orders would contain just the information necessary to describe what was ordered:

o	order_id

o	customer_id

o	subscription_id

o	purchase_date


•	subscriptions would contain the information to describe each type of subscription:

o	subscription_id

o	subscription_description

o	subscription_monthly_price

o	subscription_length

•	customers would contain the information for each customer:

o	customer_id

o	customer_name

o	customer_address

### Instructions
1.
Examine these tables by pasting the following code into the editor:
```sql
SELECT * FROM orders; 
SELECT * FROM subscriptions; 
SELECT * FROM customers;
```

## Combining Tables Manually

Let's return to our magazine company. Suppose we have the three tables described in the previous exercise. 
The tables are shown in the far right panel.
If we just look at the orders table, we can't really tell what's happened in each order. However, if we refer to the other tables, we can get a more complete picture.

Let's examine the order with an order_id of 2. It was purchased by customer 2. To find out the customer's name, we look at the customers table and look for the item with a customer_id value of 2. We can see that Customer 2's name is Jane Doe and that she lives at 456 Park Ave.

Doing this kind of matching is called **joining** two Tables.

### Instructions
1.
Using the tables displayed, what is the description of the magazine ordered in order 1?
Type your answer on line 1 of the code editor. Be sure to capitalize it the same as in the table.

## Combining Tables with SQL

Combining tables manually is **time-consuming**. Luckily, SQL gives us an easy sequence for this: it's called a `JOIN`.

If we want to combine orders and customers, we would type:
```sql
SELECT * 
FROM orders 
JOIN customers 
ON orders.customer_id = customers.customer_id
```

Let's break down this command:
1.	The first line **selects all columns** from our combined table. If we only want to select certain columns, we can specify which ones we want.
2.	The second line **specifies the first table** that we want to look in, orders
3.	The third line uses `JOIN` to say that we want to **combine information from orders with customers**.
4.	The fourth line tells us **how to combine the two tables**. We want to match customer_id from orders with customer_id from customers.

Because column names are often repeated across multiple tables we use the syntax `table_name.column_name` **to be sure that our requests for columns are unambiguous**. In our example, we use this syntax in the `ON` statement, but we will also use it in the `SELECT` or any other statement where we refer to column names.

For example, if we only wanted to select the order_id from orders and the customer_name from customers, we could use the following query:
```sql
SELECT orders.order_id, customers.customer_name 
FROM orders 
JOIN customers 
ON orders.customer_id = customers.customer_id
```
### Instructions
1.
Join orders and subscriptions and select all columns. Make sure to join on subscription_id.

```sql
SELECT *
FROM orders
JOIN subscriptions
	ON orders.subscription_id = subscriptions.subscription_id;
  ```
2.
Add a second query after your first one that only selects rows from the join where description is equal to 'Fashion Magazine'.

```sql
SELECT *
FROM orders
JOIN subscriptions
	ON orders.subscription_id = subscriptions.subscription_id
WHERE subscriptions.description = 'Fashion Magazine';
```

## Inner Joins

Let's revisit how we joined `orders` and `customers`. For every possible value of `customer_id` in `orders`, there was a corresponding row of customers with the same `customer_id`.

What if that wasn't true?

For instance, imagine that our `customers` table was out of date, and was missing any information on customer 11. If that customer had an order in `orders`, what would happen when we joined the tables?

When we perform a simple `JOIN` (often called an **inner join**) our result only includes **rows that match our `ON` condition**.

Consider the following GIF, which illustrates an inner join of two tables on `table1.c2 = table2.c2`:

![inner-join](https://user-images.githubusercontent.com/33429899/37095305-cc245ade-2215-11e8-8ac1-b4ed36b4d7e3.gif)

The first and last rows have matching values of `c2`. The middle rows do not match. The final result has all values from the first and last rows **but does not include the non-matching middle row.**

1.
Suppose we are working for The Codecademy Times, a newspaper with two types of subscriptions: a print newspaper or a set of online articles.

Some users subscribe to just the newspaper, some subscribe to just the online edition, and some subscribe to both.

The table `newspaper` contains information about the newspaper subscribers. Count the number of subscribers who get a print newspaper.
```sql
SELECT COUNT(id)
FROM newspaper;
```
2.
The table `online` contains information about the online subscribers. Count the number of subscribers who get an online newspaper.
```sql
SELECT COUNT(id)
FROM online;
```

3.
Join `newspaper` and `online` on `id` (the unique ID of the subscriber). 
How many rows are in this table?
```sql
SELECT COUNT(*)
FROM newspaper;

SELECT COUNT(*)
FROM online;

SELECT COUNT(*)
FROM newspaper
JOIN online
	ON newspaper.id = online.id;
```

## Left Joins
What if we want to combine two tables and **keep some of the un-matched rows**?

SQL lets us do this through a command called `LEFT JOIN`. A **left join** will **keep all rows from the first table**, regardless of whether there is a matching row in the second table.

Consider the following animation:

![left-join](https://user-images.githubusercontent.com/33429899/37095619-b9001500-2216-11e8-9467-ccd323f1f59b.gif)

The first and last rows have matching values of `c2`. The middle rows do not match. The final result will **keep all rows of the first table but will omit the un-matched row from the second table**.

This animation represents a table operation produced by the following command:
```sql
SELECT * 
FROM table1 
LEFT JOIN table2 
ON table1.c2 = table2.c2
```

1.	The first line **selects all columns from both tables**.
2.	The second line **selects table1 (the "left" table)**.
3.	The third line **performs a LEFT JOIN** on table2 **(the "right" table)**.
4.	The fourth line tells SQL **how to perform the join** (by looking for matching values in column `c2`.

### Instructions
1.
Let's return to our newspaper and online subscribers. Suppose we want to know how many users subscribe to the print news paper, but not to the online. Start by performing a left join of newspaper and online and selecting all columns.
```sql
SELECT *
FROM newspaper
LEFT JOIN online
ON newspaper.id = online.id;
```
2.
In order to find which users do not subscribe to the online edition, we need to add a WHERE clause. Create a new query that adds the following WHEREclause:
```sql
WHERE online.id IS NULL
```
This will select rows where there was no corresponding row from the online table.
```sql
SELECT *
FROM newspaper
LEFT JOIN online
ON newspaper.id = online.id;
```

## Primary Key vs Foreign Key

Let's return to our example of the magazine subscriptions. 
Recall that we had three tables: orders, customers and subscriptions.

Each of these tables has a column that uniquely identifies each row of that table:

•	order_id for orders

•	subscription_id for subscriptions

•	customer_id for customers

These special columns are called **primary keys**. Primary keys have a few requirements:

•	**None of the values can be NULL**

•	Each value **must be unique** (i.e., you can't have two customers with the same customer_id in the customers table)

•	A table **can not have more than one primary key column**

Let's reexamine the orders table:

order_id	customer_id	subscription_id	purchase date

1		2		3		2017-01-01

2		2		2		2017-01-01

3		3		1		2017-01-01

```sql
SELECT *
FROM newspaper
LEFT JOIN online
ON newspaper.id = online.id
WHERE online.id IS NULL;
```

