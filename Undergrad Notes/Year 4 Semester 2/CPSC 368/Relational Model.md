- Relational databases generally accept information in the form of tables
- What we want from our logical model is the ability to store data without worrying about the physical layout
- All you need is how the data semantically connects to itself
- They should be easy to query and easy to understand
- Competitors to the relational model were the network model and the hierarchical model
- However, these models were very difficult to query or understand, especially the hierarchical model
- Relational model introduced by Edgar Codd in 1970, was initially adopted at IBM and is now the most widely-used model
- There have been some competitors like NoSQL, but relational databases still dominate
- Compared to ER diagrams, we use different language for SQL
- Relational databases are made up of relations, which have two parts
- The first part is the schema, which contains the name of the relation and the name and type of each attribute
- The second part is the instance, which is a table containing rows and columns
- Rows have cardinality, columns have arity
- A Relational Database Schema is all schemas in the database and a relational instance is the instances of a schema
- We can't guarantee the order of rows or columns in an instance, so we have to refer to them on a higher level
- The main strength of SQL is the ability to easily query data
- When writing relations, you write its name followed by its attributes
- Example: Student(sid: int, name:str, address:str, phone:str, major:str)
- However, you don't always have to mention the domains
- SQL is far from the first relational language, the first one was called System R and was created by IBM in 1970
- SQL has set standards which determines what its variations must be able to do
- Even within SQL languages, some commands and terminology may vary
- In this class, we will mainly use Oracle but you may encounter other languages like MySQL
- Creating and deleting tables in SQL is pretty similar to just writing commands in english
- DROP TABLE Student would delete the student schema
- To add a new row to a schema, type INSERT / INTO Student(attributes) / VALUES (values)
- Specify the command you want to execute, then the schema you are executing on, and then specify other information like the location of the change, the content, etc.
- Integrity constraints are conditions that must always be true for data to be valid
- You can't derive this from just looking at data, it's mainly below the surface
- Context of the data will include the integrity constraints, and they cannot be violated
- For example, primary keys are an integrity constraint because no two entities can share a primary key
- Another constraint is that primary keys can never be null values
- Therefore, when we are considering our candidate keys, we should choose a primary key that will not be null, and also will not be changed over time
- This was one thing that we could not do in ER diagrams, but we can actually enforce rules like these in SQL
- When creating a table in SQL we can establish the primary key, but also any other requirements relating to which values must be unique
- A foreign key is a set of attributes in a relations that references a tuple in another relation
- For example, we probably want to have a connection between Student and Grades
- This is done by linking primary keys together
- In this example, student id is our primary key for student and is the foreign key for referencing grades
- Each tuple in Grades is connected to one primary key referring to a tuple in Student
- We want these to be consistent, so whenever you have a tuple that requires a foreign key, that key must refer to a real tuple somewhere else
- This means that when we are creating our table, in addition to adding the primary keys you need to include which foreign keys connect to that table and what schema they come from
- SQL should be able to reject any data that is input without the proper connections
- But what happens if a tuple connected via foreign keys is deleted?
- We can just delete all connecting tuples, disallow the deletion, or change the value of its primary key to null and apply that change to all tuples that key referred to
- If a student is deleted from a database, their sid becomes null and while their grades are still in the system, they are not connected to a real sid
- SQL/92 allows all of these options, NO ACTION means disallow, CASCADE means delete everything connected, and SET NULL deletes the tuple and changes all referenced tuples

**Relationship Sets**

- In SQL, relationships are dealt with using dependencies between tables and foreign keys
- Relationship sets act as their own tables, with the keys from both relevant tables as well as any additional attributes required for that relationship
- For example, if we are using our WorkOn relationship in our movie dataset, this table would include the Role attribute as well as the ID key from MoviePeople and ID from Movies
- Each row will have two foreign keys, showing what person is represented and from what movie, and then their role in that movie as an attribute
- Since this is a many to one relationship, we have to keep these attributes in a separate table
- With out tabular format, we can't properly express the phenomenon of one person having multiple roles in multiple movies in a single row
- Generally, you don't want to be storing lists in rows when different items in those lists map to multiple different foreign keys
- The same constraint happens with many to many relationships, you'll need an external relationship set
- In a one to many case, you can combine the relationship set with the many table, but not with the one table
- For example, if we are making a relationship showing the director of a movie, since each movie will only have one director we can merge the directed table with the movies table

**In Class Exercise**  
One B is associated with many As, One C is associated with many Bs
 
A(a, d)  
B(b, e)  
C(c, f)
 
R merges with A to become AR(a, **b**, d)
 
S merges with B to become BS(b, **c**, e)
 
You can't merge these two tables together because this dataset doesn't have participation constraints, meaning that not all members of a would participate in the BS relationship
 
**Relationships and Key Constraints**

- When you have one to one relationships, sometimes it is acceptable to merge everything into a single table, but only if there are participation constraints
- If there are no participation constraints, the resulting table would have null values which we don't want
- Another problem we may have is tables referring to themselves
- Lets use the example of PHD advisors, generally when a PHD student completes their degree, at some time in the future they may be an advisor for another student and so on
- If we want to represent this, we will need to include a column showing the ID of the advisor of a PHD student, who is also represented in the database as another PHD student
- This doesn't break the rules of foreign keys, despite not actually being "foreign" because student ID is a primary key and foreign keys must refer to a primary key
- For primary keys, if it is only one attribute you can just write primary key after the attribute
- If your primary key is two or more attributes, you have to declare it separately like PRIMARY KEY (name, id) instead of writing PRIMARY KEY on multiple attributes
- The same goes for making attributes unique, if combinations of attributes are unique you also have to declare them separately
- In order to communicate participation constraints in SQL, we can use the NOT NULL method
- You don't need to specify that a primary key is not null because that is already implied, but if you have a non-primary attribute that you need for a relationship where everything needs to participate, you can use NOT NULL
- One exception is for many to many relationships, even if every row participates in the relationship, that doesn't mean that all entities in both sets will be represented
- The participation constraint isn't saying that "all members of both sets must participate", it's saying that all elements of one set must relate to at least one element of the other set, and vice versa
- In order to enforce participation constraints for many to many relationships we need to be able to use assertions which we don't know about yet
- When we have a many to many relationship, it is always its own table

**Relational Model 1**

- We have two key constraints, if we know e then we know d and f, if we know d, we know e and f
- Remember that in SQL, a key constraint means the same thing as an arrow in an ER diagram
- To represent key constraints in SQL, we need to make the value with the key constraint unique
- Try to find the lowest common denominator, connect the relationship to the most restricted entity set
- In this example it was E, because it had both a key constraint and a participation constraint

**One to One with Participation Constraints**

- When you have one to one without a participation constraint, it works similar to many to one
- If you have total participation with only one attribute for each entity, you can just pick one as the primary key and the other as a foreign key
- However, if there were additional columns we might not want to have a table with so many columns
- In this case, we would want to separate the two into different columns
- A possible SQL statement to create this table would be:

CREATE TABLE Country(  
coName CHAR(20) PRIMARY KEY,  
caName CHAR(20),  
UNIQUE caName  
NOT NULL caName  
);

- If instead of formatting our table like this we instead made a separate table for capital and reference it as a foreign key in country, we would still need to make that key unique
- Even if capital is unique in its own table, it can be referenced more than once by country unless you make a UNIQUE constraint

**Weak Entity Sets**

- We usually use primary keys to make things unique and not null, but weak entities don't have primary keys
- In a weak entity, generally the primary key will include a foreign key
- You still have to specify that the key from the parent is a foreign key, and the other attribute in the primary key will be automatically not null and unique

CitiesInProvinces(CityName, **ProvinceName**, mayor), Provinces(ProvinceName, premier)

- This is an example of the schema for a weak entity Cities attached to a parent entity Provinces
- Weak entities are always synonymous with their relationships

**ISA Relationships**

- One option is to just make one table per entity, where all entities have all attributes
- This is a really unoptimal solution, so we should probably try to avoid this
- Another option is to make just one table, and then just have a bunch of null values for tuples where the ISA relationship doesn't apply
- However, this will probably mess with people trying to analyze your data
- For the third method you can have three tables but reduce duplication by limiting the ISA tables to contain only a foreign key referencing the main table and whatever attributes are specific to that set
- The only reason why this would fail is if you want to have all attributes in one place
- Next, you could have two tables where one holds one ISA option and the other holds the other option
- This only works if the ISA relationship is a disjoint and has total participation

**Aggregation**

- When translating aggregation, deal with the inside of the box first, then the outside
- Establish any relationships within the box, and then anything referencing the box will be identified by the primary keys of those in box relationships