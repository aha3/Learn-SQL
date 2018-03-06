## SQL Queries

### Introduction

In this lesson, we will be learning different SQL commands to query a single table in a database.

One of the core purposes of the SQL language is to retrieve information stored in a database. This is commonly referred to as querying. Queries allow us to communicate with the database by asking questions and having the result set return data relevant to the question.
We will be querying a database with one table named `movies`.
Let's get started!
Fun fact: IBM started out SQL as SEQUEL (Structured English QUEry Language) in the 70's to query databases.

Instructions
1.
We should get acquainted with the movies table.
In the editor, type the following:

`SELECT * FROM movies;`

What are the columns?

The columns are id, name, genre, year, and imdb_rating.

### Select

Previously, we learned that `SELECT` is used every time you want to query data from a database.
Suppose we are only interested in two of the columns. We can select individual columns by their names (separated by a comma):
```
SELECT column1, column2 
FROM table_name;
```
To make it easier to read, we moved `FROM` to another line.
Line breaks don't mean anything specific in SQL. We could write this entire query in one line, and it would run just fine.
Instructions
1.
Let's only select the name and genre columns of the table.
In the code editor, type the following:
```
SELECT name, genre 
FROM movies;
```

### As

Knowing how `SELECT` works, suppose we have the code below:
```
SELECT name 
AS 'Movies' 
FROM movies;
```
Can you guess what `AS` does?
`AS` is a keyword in SQL that allows you to **rename a column or table using an alias**. The new name can be anything you want as long as you put it inside of single quotes. Here we renamed the name column as Movies.
It is important to remember that the columns have not been renamed in the table. The aliases only appear in the result.

Instructions
1.
To showcase what the `AS` does, rename the name column with an alias of your choosing, and place it inside the single quotes, like so:
```
SELECT name 
AS '______' 
FROM movies;
```
Note in the result, that the name of the column is now your alias.

### Distinct

When we are examining data in a table, it can be helpful to know what distinct values exist in a particular column.
`DISTINCT` is used to return unique values in the output. It filters out all duplicate values in the specified column(s).
For instance,
`SELECT tools FROM inventory;`
might produce:
```
tools
Hammer
Nails
Nails
Nails
```

By adding `DISTINCT` before the column name,
`SELECT DISTINCT tools FROM inventory;`
the result would now be:
```
tools
Hammer
Nails
```

**Filtering the results of a query is an important skill in SQL.** It is easier to see the different possible genres in the movie table after the data has been filtered than to scan every row in the table.

Instructions
1.
Let's try it out. In the code editor, type:
`SELECT DISTINCT genre FROM movies;`

What are the different genres?

### Where

We can restrict our query results using the `WHERE` clause in order to obtain only the information we want.
Following this format, the statement below filters the result set to only include top rated movies (IMDb ratings greater than 8):
```
SELECT * FROM movies 
WHERE imdb_rating > 8;
```
How does it work?
1. `WHERE` clause filters the result set to include only rows where the following condition is true.
2. `imdb_rating > 8` is the condition. Here, only rows with a value greater than 8 in the imdb_rating column will be returned.
> is an operator. Operators create a condition that can be evaluated as either   .
Comparison operators used with the WHERE clause are:
•	`=` equal to
•	`!=` not equal to
•	`>` greater than
•	`<` less than
•	`>=` greater than or equal to
•	`<=` less than or equal to
There are also some special operators that we will learn more about in the upcoming exercises.
1.
Suppose we now want take a peek at all the not-so-well received movies in the database.
In the code editor, type:
`SELECT * FROM movies WHERE imdb_rating < 5;`

### Like i
`LIKE` has **nothing to do with Facebook.**
`LIKE` can be a useful operator when you want to compare similar values.
The movies table contains two films with similar titles, 'Se7en' and 'Seven'.
How could we select all movies that start with 'Se' and end with 'en' and have exactly one character in the middle?
`SELECT * FROM movies WHERE name LIKE 'Se_en';`

1. `LIKE` is a special operator used with the WHERE clause to search for a specific pattern in a column.
2.`name LIKE 'Se_en'` is a condition evaluating the name column for a specific pattern.
3. `Se_en` represents a pattern with a wildcard character. The _ means you can substitute any individual character here without breaking the pattern. The names Seven and Se7enboth match this pattern.
Instructions
1.
Let's test it out.
In the code editor, type:
`SELECT * FROM movies WHERE name LIKE 'Se_en';`

### Like ii
The percentage sign `%` is another wildcard character that can be used with `LIKE`.
This statement below filters the result set to only include movies with names that begin with the letter 'A':
`SELECT * FROM movies WHERE name LIKE 'A%';`

`%` is a wildcard character that matches zero or more missing letters in the pattern. For example:
•	`A%` matches all movies with names that begin with letter 'A'
•	`%a` matches all movies that end with 'a'
We can also use `%` both before and after a pattern:
`SELECT * FROM movies WHERE name LIKE '%man%';`
Here, any movie that contains the word 'man' in its name will be returned in the result.
`LIKE` is **not case sensitive**. 'Batman' and 'Man of Steel' will both appear in the result of the query above.

Instructions
1.
In the text editor, type:
```
SELECT * FROM movies WHERE name LIKE '%man%';
```

How many movie titles contain the word 'man'?

### Is Null

By this point of the lesson, you might have noticed that there are a few missing values in the movies table. More often than not, the data you encounter will have missing values.
Unknown values are indicated by `NULL`.

It is not possible to test for `NULL` values with comparison operators, such as `=` and `!=`.
Instead, we will have to use these operators:
•	`IS NULL`
•	`IS NOT NULL`
To filter for all movies with an IMDb rating:

`SELECT name FROM movies WHERE imdb_rating IS NOT NULL;`

Instructions
1.
Now let's do the opposite.
Write a query to find all the movies without an IMDb rating!

```
SELECT name FROM movies WHERE imdb_rating IS NULL;
```

### Between
The `BETWEEN` operator can be used in a `WHERE` clause to filter the result set within a certain range. The values can be numbers, text or dates.
This statement filters the result set to only include movies with names that begin with letters 'A' up to but not including 'J'.
`SELECT * FROM movies WHERE name BETWEEN 'A' AND 'J';`

Here is another one:

`SELECT * FROM movies WHERE year BETWEEN 1990 AND 1999;`

In this statement, the `BETWEEN` operator is being used to filter the result set to only include movies with years between 1990 up to and including 1999.
Really interesting point to emphasize again:
•	`BETWEEN` two letters is **not inclusive.**
•	`BETWEEN` two numbers **is inclusive.**

Instructions
1.
Using the `BETWEEN` operator, write a query that selects all rows where the movie titles that begin with letters 'D' up to but not including 'G'.

### And
Sometimes we want to combine multiple conditions in a `WHER`E clause to make the result set more specific and useful.

One way of doing this is to use the `AND` operator. Here, we use the `AND` operator to only return 90's romance movies.
`SELECT * FROM movies WHERE year BETWEEN 1990 AND 1999 AND genre = 'romance';`
•	`year BETWEEN 1990 AND 1999` is the 1st condition.
•	`genre = 'romance'` is the 2nd condition.
•	`AND` combines the two conditions.
 
With `AND`, both conditions must be true for the row to be included in the result.
Instructions
1.
In the previous exercise, we retrieved every movie released in the 1970's.
Now, let's retrieve every movie released in the 70's, that's also well received.
In the code editor, type:

`SELECT * FROM movies WHERE year BETWEEN 1970 AND 1979 AND imdb_rating > 8;`

2.
Suppose we have a picky friend who only wants to watch old horror films.
Using `AND`, write a new query that selects all movies made prior to 1985 that are also in the horrorgenre.

```
select * from movies 
where year < 1985
and genre = 'horror';
```

### Or

Similar to `AND`, the `OR` operator can also be used to combine multiple conditions in WHERE, but there are some fundamental differences.

Suppose we want to check out a new movie or something action-packed:

`SELECT * FROM movies WHERE year > 2014 OR genre = 'action';`
1. y`ear > 2014` is the 1st condition.
2. `genre = 'action'` is the 2nd condition.
3. `OR` combines the two conditions.

With `OR`, if any of the conditions are true, then the row is added to the result.
Instructions
1.
Let's test this out:
`SELECT * FROM movies WHERE year > 2014 OR genre = 'action';`





