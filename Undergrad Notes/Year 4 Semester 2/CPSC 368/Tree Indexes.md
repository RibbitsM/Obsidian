- An index in a book functions like a table of contents, showing you where in the book a certain phrase or concept appears
- Previously when we talked about locating things, we talked about where they are in a semantic sense
- But for indexing, we need to know the physical locations of data
- Lower level data systems have more capacity, but retrieving them is slower
- Higher level systems are smaller, but much faster
- Data is read from a disk by using a moving arm to track physical 'rings' of data on the disk
- Seek time the amount of time it takes for the arm to find the proper ring
- Rotational delay is the time it takes for the arm to read all data in a ring
- Transfer time is the time it takes for that data to be moved to working memory
- All of these affect the time it takes to read data
- SSDs do speed up this process, but the same idea of hierarchy still exists
- Data is split up into distinct blocks, ideally all the blocks we want to search are right next to each other
- If blocks are split between rings, read time is longer
- What an index does is that it tells us where to look, speeding up the process
- The syntax for creating an index in SQL is similar to creating a view or table
- We can create index for specific attributes, and even ones meeting conditions
- Two main types of structures we'll look at: Tree and Hash indices
- Hash indices are very similar to dictionaries, trees look like decision trees
- We call the top node the root node, which has no parents
- Leaf nodes are nodes that have no children
- All other nodes are called child or internal nodes

**Index Entries**

- Indexes contain combinations of keys and pointers connecting to data pages
- There are three main ways to store entries in an index
- The first way is to just record the whole thing with a search key
- The second way is to have a key with record Ids
- Trees are especially good at range and equality searches
- Hashs are also very good at equality searches
- We're going to use a structure called a B+ tree
- Searching through trees is fast, as we add and remove data from our dataset we can make sure that our tree is balanced with equal numbers of levels on all sides
- This is done through a couple of rules
- First, when data is added, nodes will have to be split and levels added to ensure all nodes are the same size
- If a page is less than half full, we will need to borrow data from other pages
- This can cause merging of pages and shrinking the tree
- The less than half-full rule does not apply to the root

**Clustered Indexes**

- Building a clustered index can be very expensive, but groups tuples together physically
- Usually guarantees that data can be collected in a single read
- Normal indexes will store data and indexes separately
- Clustered indexes are also designed based on which queries will be asked
-