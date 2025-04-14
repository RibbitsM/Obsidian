- Relational databases have some very useful features that work well for transactional data
- However, they struggle with replication and scaling
- One of these properties is called ACID
- Stands for Atomicity, Consistency, Isolation, and Durability
- All elements are all or nothing, there is no half completed transactions or partial rows (unless it is explicitly allowed)
- Each element exists in isolation, and everything is backed up and stored
- However, this relies on your computers being able to access a single database containing the entire relational database
- If something goes wrong on the server end, it can tank the entire system
- Instead, we want to distribute our data across multiple locations to ensure redundancy
- The kind of data we have now is "big data"
- That means that there is an immense volume of it, and it is not structured
- Previously, data had to be entered manually and followed a very specific format like in a csv file
- However, most of our data in the real world is not like this
- Every comment, every video, and every photo on the internet is data
- This data is not designed for storage or processing, it's designed to be used and consumed
- We also have semi-structured data like html or json where there is some scaffolding but the contents are not standardized
- We can measure data on four axes, which are Volume, Variety, Velocity, and Veracity
- Variety is the distribution of different data types, velocity is the simultaneous throughput of data, and veracity generally means accuracy to the real world

**Scaling**

- Vertical scaling involves upgrading the one single machine that you are using
- Cheaper, but also creates a single point of failure
- Often it is better to scale horizontally just by adding more computers
- This is better because it creates redundancy but also scales much further
- Can always get another computer, can't always upgrade a computer
- The problem is ensuring that all of the computers share the same data
- You want results to be consistent across your entire network
- Two ways to do this: replication and sharding
- In replication, you replicate data across different machines
- One way to do this is Primary-Replica replication, where only one computer is allowed to adjust data but has several other computers that replicate that data
- Only one is allowed to write, but all of them can read
- Can create a bottleneck for inputting new data
- In peer to peer replication, all computers can read and write
- This creates the issue of multiple edits happening simultaneously
- If two computers are processing an edit and someone tries to access the file being edited, they might get the wrong results
- Synchronizing changes across peer to peer networks is very difficult
- Sharding is when you partition data and spread it across multiple different machines
- Generally, each shard is replicated twice but this depends based on the replication policy
- Once the data in a shard reaches a critical mass, it will split again
- When you want to access data, you will automatically be directed to the machine holding that data
- An index is used that knows where all the data is stored and can be used to direct requests
- Can cause long waits when operating with data stored on multiple different machines

**CAP Theorem**

- Idea that out of three principles, a distributed database can only have two
- Consistency, Availability, and Partition tolerance (points of failure)
- Usually we choose to give up either consistency or availability
- NoSQL is a new type of database that comes in four forms
- Operates on the BASE principles
- Basically Available, Soft state, Eventual consistency
- Data will always be available, the state of the system is in flux, and the system will eventually be consistent
- Main benefits of NoSQL is scalability
- Easier to access because it is a lot closer to traditional programming languages
- Usually open source, always distributed, and don't have set schemas
- The downsides are that there is no standard across databases
- On top of this, not all NoSQL databases allow atomic transactions
- This means that we can't execute actions together, meaning they would only work if both work
- Allows for the possibility of one end of an action succeeding but the other end failing
- Not a problem with relational databases

**Column Store**

- Four different types of databases, the first type is column store
- Similar to relational in the sense that we use keys to find things
- Except, instead of columns we have column families
- This allows us to store multiple different datatypes in each row
- For example, the column family "address" can include numerical and character information
- Querying these kinds of databases is a lot faster than row stores
- This is because we usually sort all rows in a query, but not all columns

**Document Store**

- These kinds of databases usually use JSON or XML files to store data
- These are files that store information about an object that is split into different categories
- Enables us to encode information in lists
- Data within the file is divided into field:value pairs
- For example, {firstname: "Rowan", studentid: 96933502}
- Not all documents in the database need to have the same format
- However, all documents must have a unique identifier
- Different fields within a document can have relationships like one to one or one to many
- However, this risks data duplication
- We can also embed documents within documents, but there is a limit to this
- For example, the limit for mongoDB is 100

**Key Value Store**

- Pretty much identical to a hash table
- Think of it like a Python dictionary with key and value pairs
- Faster query speed than relational, but can only access key values
- Good for simple data, and can store a number of data types
- Not very good for more complex data

**Graph Database**

- Similar to our ER diagrams, graphs are made up of nodes and edges
- Good for understanding relationships, and many efficient algorithms exist to search them
- Easy to add to, but only models specific things
- Excellent for transactional and social data
- Both relational and NoSQL databases have advantages, so there have been some efforts to produce hybrids

**Data Lakes and Lakehouses** ^667321

- Talked about the concept earlier, basically a big mass of data
- Usually not super structured, and does not require a schema, which means no cleaning is required
- Designed for bottom-up data analysis
- Instead of having a stored schema, data lakes will generate a schema once the data is used
- Because of this, it's easy to add things but hard to manage them
- If a data lake becomes too unorganized, it can become a data swamp
- A data lakehouse combines the properties of a data warehouse and a data lake
- This allows you to set a schema when writing as well as reading

|                    | Data Warehouse             | Data Lake                   |
| ------------------ | -------------------------- | --------------------------- |
| Workload           | Analytical                 | Analytical                  |
| Data Type          | Structured/semi-structured | Same, but also unstructured |
| Schema Flexibility | Fixed                      | Schema generated on read    |
| Data Freshness     | Depends on last ETL run    | Depends on last refresh     |
| Analytics Approach | Top-down                   | Bottom-up                   |
