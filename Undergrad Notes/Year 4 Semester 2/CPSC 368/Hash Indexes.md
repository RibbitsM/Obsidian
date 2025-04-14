- Python dictionaries are a good example of a hash table
- Basically a set of key and value pairs
- A hash function is used to take a value and generate a unique key for it
- Hash indexes are a mode of indexing using hash tables
- The keys are the field you want to search, and the values are pages containing key and pointer values
- The [[Tree Indexes#^93e7da|three index types]] still apply here
- Can be either static or dynamic, with the same trade offs as B+ trees
- Work best for equality searches, no need to search through a tree because you can find your desired key directly
##### Static Hashing
- A static hash index has a set number of primary pages that are allocated sequentially and never de-allocated
- Contains overflow pages if needed
- Each key corresponds to a bucket containing N key pointer pairs
- Basically the purpose of the hash index is to create a unique pointer corresponding directly to a record id
- Buckets contain data entries, and can consist of a primary page and overflow pages
- The hash function should distribute values uniformly over the range 0-N-1 where N is the number of pairs
- A common hash function is `h(key) = (a * key + b) % N`
- However, this is just one example
##### Converting Decimal to Binary
- Converting a number to binary is essentially just adjusting it to base 2 instead of base 10
- To do this, we need 5 steps
Step 1: Find the largest power of 2 that fits in the number
Step 2: Put a 1 in the position associated with that power
(2$^0$ is the first digit, 2$^1$ is the second digit, and so on)
Step 3: Subtract that number from your original number
Step 4: Repeat until your original number is 0
Step 5: Fill in any remaining blanks with 0s
##### Extendible Hashing
- Main difference between static hashing and EH is that there are no overflow pages in EH
- The solution is to double the number of buckets and reorganize whenever a bucket becomes full
- However, adding that many buckets is very expensive
- To fix this, instead we have a directory of pointers connected to buckets
- When a bucket fills up, we double the number of potential buckets by doubling the directory size and just split the full bucket
- This also messes with our hash function, but this is fixable
- Each bucket has a local depth, and the global depth of the index is tracked by the directory
- To find the bucket for a certain key, look at the last `n` bits of the key, where `n` is the global depth
- Values are sorted by their hashes, with values possessing hashes that share trailing digits grouped in the same buckets
- In our example, we assume the hash function just converts a number to binary
- So one bucket will be all numbers divisible by 8 with hashes ending in 000, another will be divisible by 4 and ending in 100, etc.
- If a bucket is full, split it and allocate a new page, then double the size of the directory if necessary
- When we double the directory size, we increase the global depth by 1 and also increase the local depth of the two newly split buckets
- All other buckets remain at the original depth
- That way if one of those buckets split, there will be room for them in the directory
- Only need to increase depth if a bucket that is already at the max global depth splits
- Buckets with local depth less than global depth will just have multiple pointers attached to them
- For example, assuming our global depth is two, we could have our numbers divisible by 8 and numbers divisible by 4 in the same bucket with the 000 and 100 pointers both directing to that bucket
- A comparatively small directory can correspond to a lot of data, so there is little to no need for multiple disk access
- The directory will likely fit into memory
- If a deletion would empty a bucket, just merge it with the one it split from
- If this decreases global depth, we can halve the directory
##### Linear Hashing
- Alternative dynamic hashing scheme
- Uses a family of hash functions to map keys to their corresponding buckets
- Depending on the number of buckets, the hash function will be modified
- Overflow pages are still used, and buckets are split round-robin style
- Buckets don't have to be full to be split
- All buckets take turns being split, and once every bucket has been split once the process restarts
- To search for a specific entry, apply the function for the current split level
- If that value is within the buckets that have not been split yet in this round, you should be able to locate it
- If not, you need to apply the hash function for the next level up
- To insert, use the same process to find which bucket you want to insert into
- If that bucket is full, then add an overflow page and insert it
- Then split the next bucket in the current round
- This last part isn't required, but in this course we assume at most one split per insertion
- Only split if you are trying to insert into any existing page
- Assume that reallocating overflow pages will not create splits
- Because of the round-robin approach, it's pretty rare to get a long chain of overflows