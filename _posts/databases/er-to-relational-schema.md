---
layout: post
title: "Converting ER diagram to Relational Schema"
author: Rana Khalil
categories: [databases]
description: A beginner tutorial to converting an ER diagrams to a relational model.
fullview: true
permalink: /_posts/databases/er-to-relational-schema
---

In this blog, we'll learn how to convert an Entity-Relationship (ER) diagram to a relational schema. This conversion is approximate, in the sense that it is not always possible, and it is not unique. There is more than one approach to translating an ER diagram to relational schema. This blog covers some of the main algorithms with the aid of examples. 

The topics covered are:
- Mapping entity sets
- Mapping many-to-many relationships
- Mapping one-to-many relationships

Prerequisites: Know the basic definitions in ER diagrams: entity, attribute, key attribute, relationship


## Mapping Entity Sets

<u>Algorithm #1</u>
1. Create a table for every entity.
2. Create a field/column in the table for each attribute of the entity and set an appropriate data type for the attribute.
3. Declare the key attribute(s) to be a primary key. 

Let's take an example.

<figure>
<center><img src="/images/blogs/ER-diagram/example1.png" width="50%" height="50%" style="border: 2px solid black"/> <figcaption><b>Figure #1</b></figcaption></center><br></figure>

Figure 1 is an ER diagram of an entity **Customer**, with attributes **Name**, **Address** and **Amounts**, and key attribute **Cust_id**. Using the algorithm above, the following would be the SQL code for the table that represents this ER diagram. 

```*
CREATE TABLE Customer
(
	Cust_id INTEGER,
	Name VARCHAR(20),
	Address VARCHAR(20),
	Amount NUMERIC(8,2),
	PRIMARY KEY (Cust_id)
);
```

## Mapping Many-to-Many Relationship

<u>Algorithm #2</u>
1. Create a table for the participating entities using algorithm #1
2. Create a table for the relationship.
3. Add the primary keys of all the participating entity sets as fields/columns in the table.
4. Create a field/column in the table for each attribute of the relationship. 
5. Declare the primary key as a combination of all the primary keys of the participating entity sets.
6. Declare a foreign key constraint for every primary key of the participating entity sets.

Let's take an example.

<figure>
<center><img src="/images/blogs/ER-diagram/example2.png" width="90%" height="90%" style="border: 2px solid black"/> <figcaption><b>Figure #2</b></figcaption></center><br></figure>

Figure 2 is an ER diagram of two entities **Customer** and **Artist** connected with the many-to-many relationship **Like_Artist**. In the first part of this tutorial we learned how to represent entities like **Customer** and **Artist** as tables. Our main focus now is to represent the **Like_Artist** relationship as a table. Using algorithm #2 above, the following would be the SQL code for the table that represents the **Like_Artist** relationship. 

```*
CREATE TABLE LikeArtist
(
	Cust_id INTEGER,
	AName VARCHAR(20),
	PRIMARY KEY(AName, Cust_id),
	FOREIGN KEY (AName) REFERENCES Artist,
	FOREIGN KEY (Cust_id) REFERENCES Customer

);
```

## Mapping One-to-Many Relationship

<u>Algorithm #3</u>

Let's take an example.

<figure>
<center><img src="/images/blogs/ER-diagram/example3.png" width="100%" height="100%" style="border: 2px solid black"/> <figcaption><b>Figure #3</b></figcaption></center><br></figure>

Figure #3 is an ER diagram of two entities **Artist** and **Artwork** with a one-to-many relationship **Paints**. In plain English, this diagram is saying that an artist can paint many artwork, and an artwork can only be painted by one artist. 