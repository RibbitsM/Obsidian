- One major problem with supervised machine learning is that you need labeled data
- Often, this has to be done manually and is extremely time consuming
- Most data available is unlabelled, and cannot be used for supervised machine learning
- Unsupervised machine learning is the solution, and usually works by grouping
- Dimensionality reduction is a key application of unsupervised machine learning that won't be covered in this course, instead we will focus on clustering
- In this process, we supply X and our model tries to find groups within the data
- Unlike supervised machine learning, there is not necessarily a concrete way to determine if clustering is being done correctly or incorrectly

**K-Means**

- This is the primary clustering algorithm we will be using
- The way it works is by randomly selecting K initial center points in the data
- Then, calculate the distance from these center points to all existing points in the data that are closer to that center than another center
- Then, move the center point of each "cluster" to the approximate center of all points in that cluster, and repeat the process
- This happens until the center points stabilize and data points stop being reassigned to different groups
- K-means works well for large datasets with spherical clusters, but is vulnerable to outliers and can fail due to unlucky initial center placement
- Also, having to decide the value of k before-hand is hard if you don't know how many clusters to expect in your data
- You can still pick this using hyperparameter optimization, using something called the "elbow method"
- Basically you plot the intra-cluster distances for several values of k, and try to find the point of diminishing returns on the graph
- This is a good idea in concept, but in practice it's pretty hard to actually find this elbow point
- Ideally, intra-cluster distance should fall quickly as k increases, but almost level out as we reach the optimal k value
- Increasing k will always decrease cluster distance, but having too many groups is useless
- There's another method called the silhouette method that doesn't require cluster distance
- This is good, because not all clustering methods have cluster centers and as such you can't calculate the distance from the center
- Silhouette score is calculated using the mean distance between points in the same cluster and the mean distance from that mean point to points in the nearest other cluster
- The basic idea is to figure out how well points fit in a cluster compared to neighbouring clusters
- Generally, the higher the silhouette score, the better the clustering
- Each point in a dataset can have a silhouette score, and we can graph these scores

**Clustering Images**

- One common way to represent images in data is to flatten them and represent them as an array of pixels
- K_means expects tabular data, we can't just feed it a bunch of photos as a dataset
- This creates a ton of features, usually in the hundreds of thousands
- However, this is not our only option for representing image data
- We can use a pre-trained model trained on large and diverse datasets that are purpose-built for interpreting images
- Basically this is a neural network designed to look at images and extract useful features from them
- These models give us much fewer variables, only about a thousand
- When we ran our K means model with pixel representation, it clustered our photos of birds vaguely by background tint as it made up most of the photo
- But when we used a representation model first and then ran K means, it correctly clustered the photos based on the colour of the bird, which was what we wanted