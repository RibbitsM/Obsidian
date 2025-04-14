- An index in a book functions like a table of contents, showing you where in the book a certain phrase or concept appears
- Previously when we talked about locating things, we talked about where they are in a semantic sense
- But for indexing, we need to know the physical locations of data
- Lower level data systems have more capacity, but retrieving them is slower
- Higher level systems are smaller, but much faster
- Another factor to consider is that high level systems also cost much more per byte of data
- Data is read from a disk by using a moving arm to track physical 'rings' of data on the disk
- Seek time the amount of time it takes for the arm to find the proper ring
- Rotational delay is the time it takes for the arm to read all data in a ring
- Transfer time is the time it takes for that data to be moved to working memory
- All of these affect the time it takes to read data
- SSDs do speed up this process, but the same idea of hierarchy still exists
- Data is split up into distinct blocks, ideally all the blocks we want to search are right next to each other
- If blocks are split between rings, read time is longer
- What an index does is that it tells us where to look, speeding up the process
- Indexing allows us to store immense amounts of data while also being able to query it fairly quickly
- The syntax for creating an index in SQL is similar to creating a view or table
- We can create index for specific attributes, and even ones meeting conditions
- Two main types of structures we'll look at: Tree and Hash indices
- Hash indices are very similar to dictionaries, trees look like decision trees
- We call the top node the root node, which has no parents
- Leaf nodes are nodes that have no children
- All other nodes are called child or internal nodes

**Index Entries**

- Indexes contain combinations of keys and pointers connecting to data pages
- The key is the search key associated with that data, and the pointers shows the location of that page on your drive
- There are three main ways to store entries in an index ^93e7da
- The first way is to just record the whole thing with a search key
- This way you don't need pointers, as your key functions as both key and pointer
- The second way is to have a key with record ids
- A record id is just another word for a pointer
- A third way is to have a list of record ids that all correspond to a single search key
- In trees, each page will correspond to a leaf node with a unique record id
- Trees are especially good at range and equality searches
- Hashes are also very good at equality searches
##### B+ Trees
- We're going to use a structure called a B+ tree
- B+ trees are unique in how they automatically balance themselves in response to a tree being updated
- Searching through trees is fast, as we add and remove data from our dataset we can make sure that our tree is balanced with equal numbers of levels on all sides
- This is done through a couple of rules
- First, when data is added, nodes will have to be split and levels added to ensure all nodes are the same size
- If a page is less than half full, we will need to borrow data from other pages
- The size of a page is determined by the order of a tree
- Each node contains `d <= m <= 2d` entries, where `m` is the number of keys in the node and `d` is the order
- You can never have less keys than the order in a node, and never more than two times the order so it is always half full
- This can cause merging of pages and shrinking the tree
- The less than half-full rule does not apply to the root
##### Searching
- When searching a B+ tree, we start at the root and compare keys until we reach the right node
- Say we are looking for key 15, and our root contains keys 13, 17, 24, and 30
- 15 is between 13 and 17, so we go to the node between 13 and 17
- If that leaf node doesn't have 15, it's not in the tree
- Remember that only leaf nodes contain the actual keys, all other nodes are just pointers showing us which way to go to find the key we are looking for
##### Inserting
- First, find the correct node to insert into, in this example we'll be inserting into leaf node L
- If that node has enough space, you are done
- If not, split that node into two nodes, L and L2
- The entries should be distributed evenly between the two, and the middle key is copied up to the next level, and will now point to L2
- If copying the key exceeds the capacity of the above node, the process repeats
- When you do this for an internal node, instead of copying up the middle key you push it up
- Remember that because of the way that order works, the maximum capacity of a node will always be an even number
- Usually, splitting nodes will push up the root and increase the overall height of the tree
##### Deleting
- To delete, first find the node where the entry we are deleting is
- If deleting it would keep the node half full, we're done
- If not, we can try to borrow an entry from an adjacent node, by default we look to the right
- If we can't do this either, merge with the adjacent node
- When we merge, we have to delete the entry pointing to that node from the parent
- Similar to insert, this can create a cascading merge process
- Remember that if you borrow or merge, you will have to update the parent pointer accordingly to match the new split point
##### Clustered Indexes
- Building a clustered index can be very expensive, but groups tuples together physically
- Can only have one clustered index per table
- Usually guarantees that data can be collected in a single read
- Normal indexes will store data and indexes separately
- Clustered indexes are also designed based on which queries will be asked
- These indexes can use any of the [[Tree Indexes#^93e7da|three approaches]] to indexing
- Option one will automatically be a clustering index because it contains both the keys and pointers
- Option two will be a dense clustering index, and option 3 works better with many duplicates
##### Bulk Loading
- If we have a ton of records we want to create a B+ tree for, we want to be able to insert many records at once
- Bulk loading works by sorting all the data entries and putting them all in a single leaf node
- From there, the splitting and pushing process will automatically form the tree
- One particular advantage of B+ trees is that they have high fanout
- Since there is a pointer for every element in an internal or root node plus one, width increases exponentially for each level
- Usually only 3 or 4 layers deep depending on the order value
- Algorithm time is O(log$_f$ N) for unique searches, insertions, and deletions
- By far the most widely used index, one of the most optimized parts of a database management system