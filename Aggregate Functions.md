# Aggregate Functions

## Introduction

We've learned how to write queries to retrieve information from the database. 
Now, we are going to learn how to perform calculations using SQL.
Calculations performed on multiple rows of a table are called aggregates.
In this lesson, we have given you a table named fake_appswhich is made up of data on fake mobile applications.
Here is a quick preview of some important aggregates that we will cover in the next five exercises:

•	`COUNT`: count the number of values
•	`SUM`: add up all of the values in a column
•	`MAX`/`MIN`: get the largest/smallest value
•	`AVG`: get the mean for all values in a column
•	`ROUND`: round the values in the column

Let's get started!

1.
Before getting started, take a look at the data in the fake_apps table.
In the code editor, type the following:
```
SELECT * FROM fake_apps;
What are the column names?
```
`
## Count
The fastest way to calculate how many rows are in a table is to use the `COUNT` function.
`COUNT` is a function that takes the name of a column as an argument and counts the number of non-empty values in that column.
```
SELECT COUNT(*) 
FROM table_name;
```

Here, we want to count every row, so we pass `*` **as an argument inside parenthesis**.

### Instructions
1.
Let's count how many apps are in the database.
In the code editor, run:
```
SELECT COUNT(*) 
FROM fake_apps;
```

## Sum

SQL makes it easy to add all values in a particular column using `SUM`.
`SUM` is a function that takes the name of a column as an argument and returns the sum of all the values in that column.
What is the total number of downloads for all of the apps combined?
```
SELECT SUM(downloads) 
FROM fake_apps;
```
This adds all values in the downloads column.

### Instructions
1.
Let's find out the answer!
In the code editor, type:
```
SELECT SUM(downloads) 
FROM fake_apps;
```

## Max / Min

The `MAX` and `MIN` functions return the highest and lowest values **in a column**, respectively.
How many downloads does the most popular app have?
```
SELECT MAX(downloads) 
FROM fake_apps;
```

The most popular app has **31,090** downloads!
`MAX` takes the name of a column as an argument and returns the **largest value in that column**. 
Here, we returned the largest value in the downloads column.
`MIN` works the same way but it does the exact opposite; it **returns the smallest value**.

### Instructions
1.
What is the least number of times an app has been downloaded?
In the code editor, type:
```
SELECT MIN(downloads) FROM fake_apps;
```
## Average

SQL uses the `AVG` function to quickly calculate the **average value of a particular column**.
The statement below returns the average number of downloads for an app in our database:
```
SELECT AVG(downloads) 
FROM fake_apps;
```
The `AVG` function works by taking a column name as an argument and **returns the average value for that column**.

1.
Calculate the average number of downloads for an app in the database.
In the code editor, type:
```
SELECT AVG(downloads) 
FROM fake_apps;
```

##Round

By default, SQL tries to be as precise as possible without rounding. We can make the result set easier to read using the `ROUND` function.
`ROUND` function takes two arguments inside the parenthesis:

•	a column name

•	an integer

It rounds the values in the column **to the number of decimal places specified by the integer**.
```
SELECT ROUND(price, 0) 
FROM fake_apps;
```
Here, we pass the column price and integer 0 as arguments. SQL rounds the values in the column to zero decimal places in the output.

### Instructions
1.
Let's return the name column and a rounded pricecolumn.
In the code editor, type:
```
SELECT name, ROUND(price, 0) 
FROM fake_apps;
```

2.
Delete the previous query.
In the last exercise, we were able to get the average price of an app (2.02365) using:
```
SELECT AVG(price) 
FROM fake_apps;
```

Write a new query that rounds this result to 2 decimal places.
```
SELECT ROUND(AVG(price), 2)
 FROM fake_apps;
```

