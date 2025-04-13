- Feature engineering is extremely important for machine learning since often your model is only as good as the data you give it
- Sometimes we want to use a linear model, but our data is not linearly separable
- However, if there is still a clear grouping we can use a feature cross to separate them
- A feature cross is just multiplying two features together, useful if there is an XOR pattern
- You can also create feature crosses of one-hot encoded features to combine them together and get even more specific features
- We can also transform numerical features into categorical ones by creating "bins"
- Feature engineering is also very useful for text data, often just a default bag of words representation isn't really enough
- Of course, feature engineering requires domain knowledge and if you don't know much about the question sometimes it's better to just do trial and error with cross-validation
- Plus if you have enough data, you can also do deep learning

**Feature Selection**

- Now that we have all these new features, the dimensionality of our model is going to increase
- This means a more complex model that's more prone to overfitting
- Because of this, sometimes we need to get rid of some features to trim things down
- This is fairly easy with linear models when we have coefficients for all our features, but gets trickier for other kinds of models
- The idea is to make a normal model first, find the feature importances in that model, and then make a new model with only features that met a certain importance threshold
- However this ignores the possibility that getting rid of one feature may make another more important if importance is shared between correlated features
- This is why we use recursive feature elimination
- Similar process, except we just eliminate one feature at a time
-