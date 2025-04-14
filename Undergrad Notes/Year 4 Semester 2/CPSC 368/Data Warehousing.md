- Data warehouses are essentially really large data storages
- Up until now we've been doing something called Online transaction processing (OLTP)
- This means we usually deal with users, and the product of interactions with them
- However, this is just a fraction of all the data that gets used
- For example, UBC bases their admissions decisions off of historical data of students that have graduated in the past
- When you consider the size of all the data on academic performance for every UBC student ever, that's a lot of data
- These can be numerical information like grades, or even qualitative information
- Keeping all of this data organized is a pretty monumental task
- To use this data you'll probably need multiple sources, you might not need super recent data, but you will need to do complex queries quickly
- You can't really just cram all of that data into one place, although improvements in technology are making this option more and more feasible
- This kind of strategy is called a "data lake"
- One central repository of data that can be queried by anyone
- Easy to build, but pretty difficult and slow to use
- A wide variety of issues can come out of this approach, like having data that's mislabelled or has different names across schema
- A data warehouse puts all the data into an application where it is constantly maintained
- Similar to a [[NoSQL#^667321|data lake]], but you put in the work to standardize and clean it before storing it away
- Online Analytical Processing (OLAP) is a more complex way of using and analyzing data which generally calculates a value
- Lots of aggregate operators, lots of grouping

**Example**

- Going back to our student schema, each student has a number, major, age, and standing
- In OLAP, we have a concept called dimensions
- These are basically different ways of grouping
- For example, the four attributes we mentioned earlier are all dimensions of student, but these attributes can also have dimensions
- For example, department is a dimension of major
- The fact table is the table that holds the basic information of our schema, but it also has dimension tables for each attribute in it
- These dimension tables can have their own dimension tables as well
- For example, we have a sales schema containing store ID, item ID, customer ID, this is the fact table
- Within customer ID we can find the name, address, or loyalty points of that customer
- In store ID we could find the city it's located in, and then within city we can find the province or state that it's in

**Queries**

- Something you can do with this is a full star [[SQL#^267745|join]], where you add all dimension tables to a fact table
- With extra dimensions, we have to start thinking of data as a cube
- Another query you can do is called Roll-up
- In this example, you replace a group in your old query with a higher dimension version of it
- For example, instead of grouping by store ID you group by city, or instead of grouping by individual customer you group by customer age
- As we roll up, the number of the dimensions remains the same but their size increases
- You don't have to keep all the dimensions though, you can discard them if you want
- Drill down is the opposite of roll up, making your query more specific
- Again, this is done by changing your group by clause
- Slicing is a technique for extracting data from a query by putting a limit on one of your dimensions
- In practice, this just means adding to your where clause
- Going further, you can dice your data by putting limits on two dimensions
- Two of the most popular schema options are star or snowflake
- Star is generally much easier to work with, but not as powerful
- Star schema means having one table for each fact, and then one table per dimension
- Set up using Boyce-Codd Normal Form, meaning that every attribute in a table is associated with the entire primary key
- However, this is only for the fact tables, dimension tables a relatively small and so are not normalized
- Snowflake schema need a lot of joins, but can allow for more complex queries
- In a snowflake schema, each dimension is a set of tables, usually with one table per level of hierarchy
- If you have a time dimension, you'd have an 24 hour time table, a week table, and a month table
- Doesn't require normalization, but makes queries harder because of all the joins required

|                     | Star                                          | Snowflake                                                               |
| ------------------- | --------------------------------------------- | ----------------------------------------------------------------------- |
| Ease of Maintenance | Has redundant data, harder to make changes to | No redundant data, easier to change                                     |
| Ease of Use         | Less complex queries                          | More complex queries                                                    |
| Query Performance   | Fewer foreign keys, faster execution          | More foreign keys, slower execution                                     |
| Joins               | Fewer joins                                   | More joins                                                              |
| Dimensions          | One table per dimension                       | Multiple tables per dimension                                           |
| When to use         | Default choice                                | Used when dimension tables are exceptionally large or need many updates |
| Normalization       | Dimensions not normalized                     | Normalized dimensions                                                   |

^0ae183

- We can create a data cube in SQL by using the CUBE BY operator
- Gives you a table with columns representing all possible dimensions and aggregate values, with Null values where a grouping is not present
- Essentially starting with your full data and then rolling up on every dimension
- When cubes lack data for some combinations, we call that a sparse cube
- To find the size of a sparse cube, take the size of the cube assuming it was dense and multiply by the sparsity factor

**Views** ^a2f3ba

- For most cases, we can treat views exactly how we treat tables
- We can actually ask databases to store our views, we call these materialized views
- This takes up storage space, so we can't store all of the possible views
- Database engineers use algorithms to determine the optimal amount of views to store based on which attributes we have
- Even with two schema with three attributes each, we have 16 possible group by options
- To summarize, the reason we use views is because we likely have immense amounts of data and we want to be efficient
- Some views are going to be more efficient to visualize compared to others, and we can find these views using the HRU algorithm
- This is a greedy algorithm, which always picks the best solution at the time it is run
- For each unmaterialized view, it will calculate the amount of work saved compared to the base table and choose the one that saves the most
- The benefit generated is equal to the benefit created from a view multiplied by the number of subviews that can be generated from that view plus one
- As more views become materialized, this calculation becomes more difficult
- If multiple views are materialized, we repeat the benefit calculation for each materialized view and add them together

**Notes Continued**

- Multidimensional expressions are what we call queries for OLAP databases
- Similar to SQL databases, except they take additional dimensions into account
- Instead of selecting columns from tables, we're selecting columns, rows, or pages from cubes
- Remember that cubes don't have to be 3d they can be 4d or more
##### Learning Goals
- Compare and contrast OLAP and OLTP processing
	- OLTP mainly focused on transaction data, very customer focused and requires fast read and write capabilities
	- Good for fast data storage and recovery, but poorly suited for deep analysis and data science
	- Requires much more data from multiple sources and the ability to process more complex queries
	- OLAP allows for more complex queries and views including trend analysis
	- Unique in their ability to drill down and roll up on schema
	- Usually used by domain experts
- Explain ETL tasks for data warehouses
	- Extract, transform, load
	- We don't do much extraction or loading, as most of the data stays in the warehouse and doesn't move
	- Create your warehouse in an initial upload and keep it like that
- Explain difference between star and snowflake design, including performance tradeoffs
	- See [[Data Warehousing#^0ae183|table]] 
- Argue for the value of data cubes in terms of the type of data in the cube, the goals of OLAP, and the operations that can be performed
	- Allows much more complex queries to be performed
	- Able to nest more complex data within a single view or table
	- Access multiple dimensions of data at once
- Estimate complexity of a data cube
	- Multiply the dimensions together to find cube size
	- Also look for scarcity