**Apriori Algorithm**  ^67283d

- Designed to minimize the amount of counting we have to do when determining association rules
- Counting the support is one of the slowest parts of the process
- If our minimum support level is 50% and only one of our four rows contains a certain item, we know that any itemset containing that item is not supported
- This is how apriori works, by eliminating the items that will never be supported right away so we don't have to count them
- A strict subset is a set where all items in that set appear in a larger set
- Very popular algorithm, like 20k citation
-