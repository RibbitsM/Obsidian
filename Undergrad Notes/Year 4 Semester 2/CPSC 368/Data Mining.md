- Data mining is just examining large quantities of data for patterns
- We want these patterns to be valid, novel, useful, and understandable
- Done through [[Undergrad Notes/Year 4 Semester 1/CPSC 330/Intro#^bccc1b|supervised and unsupervised machine learning]] methods
- Examples of supervised learning are [[Classification Evaluation|classification]] algorithms for categorical data, and [[Undergrad Notes/Year 3 Semester 2/STAT 301/Lecture 4|regression]] algorithms for numerical data
- Unsupervised methods include clustering and other automatic grouping algorithms
- Other kinds of data mining include modelling associations and correlations, detecting outliers, and analyzing trends
- A common trend we try to spot in machine learning are association rules
- Classic example of diapers and beer
- Used in department stores, medical clinics, insurance companies, and DNA sequencing labs
- Say we have data on customers and purchases and we want to develop association rules for grocery store purchases
- A rule is supported by a certain percent in that percentage of transactions contain both item X and item Y
- For example, if 4 of 7 customers bought both chicken and milk, the rule of buying chicken and milk has ~57% support
- Rules can also have confidence, which is the percentage of transactions containing item X that also contain item Y
- Our previous rule would have 80% support as we have 5 transactions containing chicken, with 4 of those also containing milk
- That rule would be expressed as Chicken -> Milk as in this case, item X would be chicken
- An association rule is valid if it's support and confidence both meet a set threshold
- When a set of items has at least minimum support, we call that a frequent itemset
- To calculate these over mass amounts of data, we use the Apriori algorithm
**Apriori Algorithm**  ^67283d

- Designed to minimize the amount of counting we have to do when determining association rules
- Based on the idea that each subset of a frequent itemset will also be a frequent itemset
- Counting the support is one of the slowest parts of the process
- If our minimum support level is 50% and only one of our four rows contains a certain item, we know that any itemset containing that item is not supported
- This is how apriori works, by eliminating the items that will never be supported right away so we don't have to count them
- A strict subset is a set where all items in that set appear in a larger set
- Very popular algorithm, like 20k citation
- The first step is to identify all itemsets of size 1 that meet the support threshold
- Then, calculate all possible itemsets of size 2, eliminating any itemsets including items that were not identified in step 1
- Repeat this process by identifying all remaining itemsets of size 2 not meeting the threshold and move on to size 3
- This continues until there are no more itemsets that meet the threshold
- As a result, we saved a lot of time by not counting the support of all possible itemsets, only those that had the potential to be frequent itemsets

f1 = {{cake},{jam},{rolls},{tea}}
c2 = {{cake, jam},{cake,rolls},{cake,tea},{jam,rolls},{jam,tea},{rolls,tea}}
f2 = {{cake,jam},{jam,rolls},{jam,tea},{rolls,tea}}
c3 = {{cake,jam,rolls},{cake,jam,tea},{jam,rolls,tea}}
f3 = {}
Answer = {{cake},{jam},{rolls},{tea},{cake,jam},{jam,rolls},{jam,tea},{rolls,tea}}
##### Clustering
- Type of unsupervised learning
- Doesn't require labelled data, algorithm will examine data for hidden patterns/correlations and group it accordingly
- Can also be used as a preliminary step for other data mining processes
- Clustering is used for a number of things ranging from document analysis to movie recommendations
- Make sure you are clustering by variables that matter, libraries organize books by content, not by colour
- We can measure the quality of our clusters by calculating the similarity between items within a cluster and the difference between items in different clusters
- A particularly powerful method is [[K-Means|k-means clustering]]
- Creates k clusters from data, has the potential to go infinitely if not limited
- Good for large datasets, but can end up with low-quality clusters
- We usually cluster by transforming our data into numerical form, and calculating the distance between points in high-dimensional space
- Easier to think about with just two variables on a Cartesian plane
- K-means randomly places k centroids in your data space, and assigns all data to the closest centroid
- Then average all points in a cluster, and move the centroid to that point
- Repeat until centroids stop moving
- K-means assumes clusters are roughly circular, and relies somewhat on the initial position of the clusters, both major weaknesses
- 