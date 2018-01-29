---
layout: post
title: "PostgreSQL Beginner Tutorial III: More Basic SQL Programming"
author: Rana Khalil
categories: [databases]
description: A beginner tutorial to PostgreSQL using pgAdmin 4.
fullview: true
permalink: /_posts/databases/postgresql_tutorial3
---

This blog covers part 3 of a series of tutorials explaining PostgreSQL. In the [previous tutorial](/_posts/databases/postgresql_tutorial2), we covered the basics of SQL programming which included the basic CREATE TABLE, INSERT, SELECT and DELETE statements. In this tutorial we'll go into more detail on the SELECT statement that involves single table queries and multiple table queries. We'll also cover the ALTER TABLE statement and the ORDER BY, GROUP BY and HAVING clauses. 

The topics covered are: 
- SQL ALTER TABLE statement
- SQL SELECT statement (single table and multiple table queries)
- SQL ORDER BY, GROUP BY and HAVING clauses

Prerequisite tasks: Create a **laboratories** schema that includes the tables and data given in [tutorial 2](/_posts/databases/postgresql_tutorial2).

## SQL ALTER TABLE Statement
The SQL ALTER command can be used to add/drop columns in a table, change the definition of a column in a table and add/drop table constraints. The general syntax for the SQL ALTER TABLE command is:

```*
ALTER TABLE <table_name>
ADD <column_name> <column_type>
```

Let's take our first example: Add the column "Nationality" with type VARCHAR(20) to the table Artist. Using the above syntax, the query should look like this:

```*
ALTER TABLE Artist ADD Nationality VARCHAR(20);
```

Now if we display all the columns in the table artist using the SELECT command, you should get the following table:

<center><img src="/images/blogs/pgadmin-tutorial-3/add_column.png" width="80%" height="80%" style="border: 2px solid black"/></center><br> 

Notice that since we added the column to a table that already has data (rows) and we didn't set a default value in the query, the nationality column for that data will have NULL values. 

If you want to add a column with an additional integrity constraint, you use the following syntax:

```*
ALTER TABLE <table_name>
ADD <column_name> <column_type> CONSTRAINT(<constraint>);
```

To demonstrate that, let's take our second example: Add a column "Cust_age" with type integer to the table Customer with the integrity constraint that the customer has to be older than 12. Using the above syntax, the query should look like this:

```*
ALTER TABLE Customer ADD Cust_age INTEGER CHECK(Cust_age > 12);
```

Now if you try to fill the entry that has Cust_id = 1 with Cust_age = 11:

```*
UPDATE Customer SET Cust_age=11 WHERE Cust_id=1;
```
 
 you'll correctly get a violates check constraint since the specified age is not bigger than 12.


## SQL SELECT statement
In the [previous tutorial](/_posts/databases/postgresql_tutorial2), we learned about the simple select-from-where block that was used to query a single table. For this tutorial, we'll start with explaining how to query multiple tables using the SELECT statement. Then we'll go through the GROUP BY, HAVING and ORDER BY clauses. 

The syntax to query **multiple tables** using the SQL SELECT statement is as follows:

```*
SELECT <attribute list>
FROM  <table list>
WHERE <condition>
```

To demonstrate that, let's take our third example: List the name and birthplace of the artist that painted "End of Summer". This query requires information from both the Artist table and Artwork table. Namely, the artist name can be taken from either table, but the BirthPlace is only available in the Artist table and the Title is only available in the Artwork table. Using the above syntax, the query should look like this:

```*
SELECT Artist.AName, BirthPlace
FROM Artist, Artwork
WHERE Artist.AName = Artwork.AName and Title='End of Summer';
```
First thing to notice over here is that the attribute/column name AName is prefixed with the table it comes from, whereas the attribute BirthPlace is not. The reason behind that is that AName exists in both the tables Artist and Artwork. So if it is not prefixed with the table name, the compiler will not know which table it came from and therefore you will get the error "column reference "aname" is ambiguous". Second thing to notice is the condition Artist.AName = Artwork.AName in the WHERE clause. This condition is called a **join condition** because it combines the two tables Artist and Artwork whenever the name of the artist in the Artist table is the same as the name of the Artist in the Artwork table.


The **ORDER BY** clause is used to specify the order for displaying the results in a query. The syntax to use the **ORDER BY** clause in the SELECT statement is:
```*
SELECT <attribute list>
FROM <table list>
WHERE <condition>
ORDER BY <attribute list>
```

To demonstrate that, let's take our fourth example: List the names and ages of artists and order the results by age.  Using the above syntax, the query should look like this:

```*
SELECT AName, Age
FROM Artist
ORDER BY Age;
```

When the query is executed, you should get a list of names and ages of artists that are ordered by increasing age.

<center><img src="/images/blogs/pgadmin-tutorial-3/order_age.png" width="40%" height="40%" style="border: 2px solid black"/></center><br> 

The **GROUP BY** clause is used to group/gather all the rows together that contain the data in the columns specified in the GROUP BY clause. The clause can also be used to perform aggregate functions such as sum, avg and count on one or more columns. The syntax to use the **GROUP BY** clause in the SELECT statement is:

```*
SELECT <attribute list>
FROM <table list>
WHERE <condition>
GROUP BY <grouping attributes>
```

Note that if an attribute appears in the SELECT query it has to appear in the GROUP BY statement unless it is part of an aggregate function. Also, an aggregate function cannot appear in the SELECT query unless the query contains a GROUP BY clause. 

In order for us to demonstrate the GROUP BY functionality with an example, we need to add an extra row to the Artist table:

```*
INSERT INTO Artist(AName, Birthplace, Style, Age, Nationality) VALUES ('Andrew', 'Montreal', 'Modern', 33, 'Canada');
```

The fifth example will make use of both an aggregate function and a GROUP BY clause. Let's take the following query: For every Artist style, list the maximum age of the Artist. Using the above syntax, the query should look like this:

```*
Select max(Age), Style
from Artist
Group by Style;
```

Notice that in our data, each style is unique to the artist except for the style "Modern" that is used by two artists "Joseph" and "Andrews" of ages "31" and "33". Since we use the aggregate function max that displays the maximum age of each style, you only see one entry for the style "Modern" with the maximum age "33".

<center><img src="/images/blogs/pgadmin-tutorial-3/group_by.png" width="60%" height="60%" style="border: 2px solid black"/></center><br> 

A **HAVING** clause can appear in conjunction with a GROUP BY clause if the groups have to satisfy a set of conditions. The syntax to use the **HAVAING** clause in the SELECT statement is:

```*
SELECT <attribute list>
FROM <table list>
WHERE <condition>
GROUP BY <grouping attributes>
HAVING <group selection conditions>
```

To demonstrate that, let's take our sixth example: For every Artist style, list the maximum age of the artist such that the maximum age cannot exceed 80. Using the above syntax, the query should look like this:

```*
Select max(Age), Style
from Artist
Group by Style 
HAVING max(Age) < 81;
```
The group selection condition should now remove the "Impressionism" style from the resulting table.

This concludes our tutorial. In the next tutorial we will cover advanced SQL queries.

**References**: 
- Most of the examples and queries presented in this tutorial are taken from the CSI2132 lab 3 material that can be found [here](https://github.com/rkhal101/CSI2132-Databases-I/tree/master/labs/lab3).  