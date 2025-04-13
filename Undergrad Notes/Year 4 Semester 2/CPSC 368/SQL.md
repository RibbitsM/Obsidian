 - SQL consists of multiple different parts, we've already explored how to write SQL DDL statements which stands for Data Definition Language
- In this section, we will learn DML or Data Manipulation Language
- We have access to SQL Plus through an Oracle Database by logging in to the UBC CS server

**Creating Tables**

- Start your statement by writing "create table", then all your variables and their datatypes, and finally include the integrity constraints
- In the past we've mostly used integer and char, but there are many more datatypes
- These include time types like timestamp or interval, which are powerful but very fiddly
- When possible, try to use built in time types or avoid them altogether

**Query**

- A basic SQL query involves three aspects, what you want, where you are getting it from, and what kind of information you want
- These three sections are depicted by Select, From, and Where
- To start with, select lets us choose what column(s) we are looking for
- If we want name and age, type select (name, age)
- To get all columns from a table, type select *
- From lets us choose which table(s) to look at, yes this can be multiple
- If we want to gather the game scores from a football dataset, query select Score1, Score2 from Scores
- The where section lets us use boolean statements to filter the results of our query
- Syntax for this may differ from database to database, but this is unfortunately unavoidable
- But, what if we want to get information from multiple relations?
- The structure mostly stays the same, but we have to change Where
- When two or more tables are listed in From, SQL will combine those two tables
- In the Where section we have to write alias1.PrimaryKey = alias2.PrimaryKey, and in From we have to write Relation1 alias1, Relation2 alias2
- This is because these relations will have overlapping variable names, and including aliases will make writing our Where query much faster
- The combination of these two tables created by SQL is effectively a cross product
- This is a table consisting of every possible combination of values from two tables
- By including our equality clause in the Where section, we can remove all of the impossible combinations created by this cross product
- The Distinct command lets us ensure that we only look at distinct values if we are looking at a non primary key
- Within the Where command, we are able to perform string operations
- Another command you can use in your SQL query is the Order By clause
- This clause is added onto the end of your query, and sorts the results based on the attribute that you input
- By default this sorts by ascending order, but you can do otherwise
- You can also sort by multiple attributes, and if there are repeats of the first attribute those will be sorted by the second attribute and so on
- If all ordering attributes are the same, the tuples will be returned in random order
- Apart from string operations, we also have the option of using set operations
- There are three options, union, intersect, and except
- All three of these will eliminate duplicates, but if you want to keep them you can type all after the set operation
- The way union works is that you type your first query, then write UNION, and then type the second query
- Union will join the two sets together, outputting the total results of both sets combined
- Intersect works in a similar way, except it outputs only the results that are the same between sets
- This is a very useful tool because we can do things that we can't do with normal SQL commands
- For example, we can find tuples that have the same ID attribute but have other attributes that meet certain categories
- Actor that was in a movie in 1944 and 1974
- Finally, except takes the results from the query on top, and removes all results that appear in the query on the bottom
- Aggregate operations do exactly what you'd expect, and generally only work on numerical data
- Usually using a * instead of a specific column does nothing

**Group By**

- Group by also works exactly as you'd expect
- However, you can also add the Having method which lets you add a boolean requirement to the groups
- For example, group by major having count(*) > 50 will only give you majors with more than 50 students in them
- Group by usually comes after where, but if you're not using where it goes after from
- When selecting values from a group, unless you are doing an aggregate operation you won't be able to return any values you didn't group by

**Views**

- When we create a table, it exists permanently
- However, views work as temporary tables that can have info from any number of tables
- Views let you hide some data from your users, and make queries easier without having to create an entire permanent table
- Also, what you can do is create private tables that can be used to hold sensitive information from those who don't need to access it
- With views, we can pull information from hidden tables when it is needed
- Views are created similarly to creating tables
- Write create view, the schema you are drawing from, and the attributes you need from those schema
- Views cannot update data, because they don't need primary and foreign keys
- Also can't insert or delete on a view
- We can delete views with drop view, just how we drop tables
- When we're dropping tables, we can do it with restrict, which means any views associated with it survive, or with cascade, which drops all views associated with that table

**Null**

- As long as a value isn't a primary key, and isn't not null, that attribute can have null values
- We can check for null values using the is null clause
- If we try any mathematic expression involving null, the result is null

This also extends to logical statements like and, or, not

- If a where clause results in null, that is treated as false
- Aggregate operations always ignore null, except for count(*)

**Natural Join**  ^267745

- So far, when we've been joining our tables we just do it through from and where
- This kind of join is called a natural join
- If our tables have columns of the same name and type, they will be merged
- However, if this isn't the case we'll have to use the on clause while joining
- What we normally do is after putting two tables in from, we then use an equality statement to filter the cross product
- However, we have other kinds of joins, either natural or unnatural
- If we have a natural inner join with two columns using the same name and data type, only rows where that column has the same value in both tables will be kept
- A natural left outer join will keep all values from the left table and fill in nonmatching rows on the right with nulls, and vice versa for right joins
- A pure natural outer join will do this on both sides, meaning all values from the matching column will be kept
- If you're not doing a natural join, you will have to specify which column is being used for that join

**Insert**

- Previously, we've been inserting into tables row by row
- However, we can mass insert by using entire columns from other tables
- We can also mass delete by using a where condition
- Another thing we can do are creating check constraints
- This lets you do things like set a limited range for an integer attribute
- With check constraints, we can limit what values people can insert or update
- Like anything else, we can use subqueries to do this
- Another kind of restraint is an assertion, which exists across multiple tables and relations
- Allows us to do things like enforce many to many participation constraints
- To do this, create an assertion with Create Assertion, name it, and then set a check constraint
- A many to many participation constraint would look like this:
-   
    

Create Assertion Participation  
Check  
(Not Exists ((Select attribute from table1)  
Except  
(select attribute from table2)));
 
**Evaluation of a Query**

1. If from has multiple arguments, do the cross product
2. Then if you have a where clause, remove everything that doesn't meet the requirements
3. If there is a group by, group the remaining students according to the requirements
4. If there is a having clause, filter the groups
5. Finally, select your attributes from the remaining rows

**All SQL Methods/Features**

- Select: determines which attributes will be returned by a query
- From: determines which schema will be searched
- Where: determines criteria for which rows will be selected
- Within a where statement, = means equal and <> means unequal
- In: returns true if the chosen attribute(s) appears in a chosen sql query
- Not In: returns true if the chosen attribute(s) appears in a chosen sql query
- Exists: returns true if a chosen sql query returns at least one result
- Not Exists: returns true if a chosen sql query returns no results
- Unique: returns true if a chosen sql query returns no duplicate results
- Any: returns true if a boolean condition is fulfilled by any result from a chosen sql query
- All: returns true if a boolean condition is fulfilled by all results from a chosen sql query
- Distinct: when appended onto an attribute, removes all duplicates when selecting
- Order By: determines the order in which attributes will be returned by a query
- And: adds another criteria to a where statement
- Or: adds an optional criteria to a where statement
- Union: inserted between two queries, returns the results of both queries combined, removes duplicates
- Intersect: inserted between two queries, returns only the results that were outputted by both queries, removes duplicates
- Except: inserted between two queries, returns all the results outputted by the top query which were not output by the bottom query, removes duplicates
- All can be added to any of these three to include duplicates in the output
- Count: returns the number of rows output by a query
- Sum: returns the sum of all rows output by a query
- Avg: returns the mean of all rows output by a query
- Group By: divides query into separate groups divided by the chosen attribute
- Having: determines which rows will be admitted into each group created by group by
- Like: filters rows depending on the presence of certain characters
- Within a like statement, % fills in for any characters and _ fills in for one instance of any character