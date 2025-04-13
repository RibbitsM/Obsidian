**Analogy-Based Algorithms**

- Two significant applications for these algorithms are recommendation systems and facial recognition systems
- This is because these algorithms work by comparing new examples to known examples and classifying them based on their similarity
- KNN and support vector machines (SVMs) with the RBF kernel are examples of similarity-based algorithms
- These algorithms use metrics based on euclidean distance between points or similarity between observations to predict the target variable
- This isn't necessarily the 2d space we're used to because the dimensionality depends on the number of variables
- Since we need one dimension for each variable, we can end up with many many dimensions in our final model
- 20 is low dimensional, 1000 is medium, and 100,000 is high
- This is easier to reach than you'd think, many image recognition programs have a variable for each pixel
- A feature vector is a vector listing the values of all variables relating to a specific example
- Basically just a row in the dataset
- For calculating the euclidean distance, we can use a function built into scikit learn called euclidean_distances()
- We can think of algorithms like these as "lazy learners", they don't come up with rules for classification beforehand, but instead compare new data to the training data
- KNN classifies an object based on the label of it's nearest neighbors by euclidean distance
- It's a simple and intuitive model, but not a particularly powerful one
- The main hyperparameter here is k, which decreases the fit of the model as k increases
- However, the model doesn't work unless the units of the data are scaled properly
- Also vulnerable to high dimensionality
- As we add more dimensions, the volume of the space increases exponentially, making it more difficult to properly calculate distance metrics
- In extreme examples, all data appears to be equidistant
- We can fix this with dimension reduction methods

**KNN**

- The point of the KNN algorithm is that it predicts the class of an unknown object by comparing it's euclidean distance to a certain amount of neighbors
- This is set by the variable k, hence the name
- By counting up the classes of all these neighbors, the class with the largest count is what is assigned to the unknown object
- We pick our value of k with hyperparameter optimization
- Choosing a low value usually causes overfitting, while higher values tend to underfit the data
- You can also assign weights to the neighbours so closer points are worth more in the count using a hyperparameter called weights
- You can also use KNN for regression by taking the average of all neighbours and even do weighted regression
- The main benefits are that knn is easy to use and interpret, fits very quickly, and can fit very complex problems with enough data
- The cons are that prediction takes a long time, doesn't work well when many values are 0, and has not great accuracy
- KNN is what we call a non-parametric model which means that it needs to store all the examples to be able to make predictions
- This is because every new value is checked against the entire dataset
- The curse of dimensionality is bad for all models but KNN is very vulnerable to this
- Works well at lower dimensions but falls apart as more variables are introduced

**SVM RBFs**

- RBF stands for Radial Basis Function, which increases the dimensionality of the data
- This model functions excellently with high-dimensional data and also captures complex decision boundaries in sparse and non-linear data
- Two hyperparameters, C and gamma
- C is a regularization parameter, and adjusts the fundamental ML tradeoff by changing the complexity of the model, higher C means a more complex model
- Gamma affects the influence of each example, and can cause overfitting at higher values
- Large gamma means more complex, smaller gamma means less complex
- The problem with this is that right now we only know how to optimize one hyperparameter at a time
- Model is kind of like weighted KNN
- Creates a decision boundary by classifying examples as negative or positive based on their similarity to known negative or positive examples, and calculates the boundary based on weight
- The model doesn't save the whole dataset like KNN does, but rather a couple key examples
- These examples are called support vectors, and speeds up prediction
- Every example in the training data is classified as a support vector or not a support vector during the fitting process
- The resulting decision boundary only depends on the support vectors
- Basically, the support vectors are the points closest to the boundary
- If a point is far away from the boundary, there's not much of a point of pulling out the whole dataset to classify it
- If a point is close to the boundary, we have all the information required to classify it on hand
- Also uses a different similarity metric compared to KNN
- This is called a kernel, and we use the RBF kernel
- The decision boundaries are much smoother than in KNN, and prediction accuracy is usually higher as well
- Also, you can use it for regression as well

**Pros and Cons**

- Decision trees are the most scalable model, followed by SVM RBF and KNN
- KNN and decision trees are most vulnerable to outliers, SVM RBF is less so
- KNN is more memory intensive because it needs the full dataset to compare each point to when performing classification, although more efficient methods exist
- SVM RBF is less intensive since it only stores vectors, and decision trees only save the model
- Because of the same reasons, KNN has a very fast training time but slow prediction times
- Decision trees take longer to train than predict, and the same goes for SVM RBF
- KNN and decision trees both have native support for multiclass data, but SVM RBF does not