**Data Preprocessing**

- Preprocessing is important for models like KNN where the model will not be fit properly unless the scale of the variables is properly adjusted
- If you are using real data, you can't just plug it into a model right away
- Think about our spotify dataset, you wouldn't be able to just fit a KNN model on it as is
- Euclidean distance only works if all axes have the same scale
- If one variable ranges from 0 to 1 and another goes from 50 to 1000, the distance between two points will be dominated by the second variable
- If we scale all the variables to have the same range, all variables will have the same weight in the distance calculation
- This process is called normalization, but what we will be doing is standardization
- You use MinMaxScaler() to normalize, but what we want to do is set the sample mean to 0 and the standard deviation 1, and scale the data that way
- Apart from these two options, you can also use Normalizer() that performs the same operation but on rows instead of columns
- You can also perform log scaling, but only do this if your data is already logarithmic
- An example of this would be movie ratings, a few movies have many reviews, but the vast majority only have a few
- This way the relative range of the data is preserved as well as the relative distance between points
- We do this with the StandardScaler() function in sk learn
- Create the object, then use object.fit() on your data, and then do object.transform() to apply it to your desired data
- .fit and .predict are what we call estimators
- Imputation is another common preprocessing method, which is used to fill in missing values in your data
- Most models will not work with missing values, and it's often not feasible to just remove these rows or replace them with zeros
- If you cannot simply remove your NaN values, you can fill them in with the mean, median, mode, or through KNN using SimpleImputer()
- However, most of these methods only really work with continuous variables, for categorical variables you'll probably have to use KNN
- Of course, you can always just fill in missing categorical variables with the most common level
- Also, we want to do these steps in a specific order
- Before we try to scale our data, we'll need to impute it first to get rid of missing values
- Another important transformation is one-hot encoding
- Most algorithms in our workflow do not work with non-numerical inputs
- To use them, we need to encode them to numbers
- There are two main options: ordinal and one-hot encoding
- With ordinal encoding, we just assign each level of the variable to a number
- Unfortunately, this really only works if our variable is already ordinal
- Sometimes, it may be unclear whether to use one-hot encoding or ordinal encoding
- For example, you could interpret a variable by giving equal weight to each category, or by assigning them to levels (weather conditions for example)
- In one-hot encoding, we add new columns to our dataset to represent the different levels
- This can be a issue when we have many different categories, you may need to bucket some categories or only consider the most common ones
- These are binary columns, which display zero if the level for that observation is not of that level, and one if it is
- A side effect of this is adding many more columns to our dataset, one for each level
- This is also a problem if we want to do scaling and one-hot encoding in the same dataset
- We solve this problem with ColumnTransformer()
- We don't want to apply different transformations to the train and test data, this is why we transform the test data with the scaler used for the training data
- This isn't as bad as transforming the whole dataset before splitting, but is still a poor methodology

**Transformers vs Estimators**

- Fit() methods are estimators, which create new parameters from the data and enable prediction
- Transformers just apply different methods of transforming the data, like SimpleImputer and StandardScaler
- However, often we will have to fit our transformers first, but we don't need to include y in this step
- With this method, we can apply the transformation to the test data as well but without risking data leakage by including test data while fitting the transformer
- We never want to transform the whole data at once, just on the training data
- You can certainly make changes to the data before splitting it, but you cannot do anything using data from other parts of the dataset
- For example, it's fine to make a column that's numerical by default a categorical variable as long as no information is used
- You can also create new columns as long as it's done 1 row at a time
- For example, you can multiply two columns together to create a new column since the process is done row by row
- But just to be safe it's better to do stuff like this after splitting
- Otherwise we may accidentally include data from our test sets in the training data

**Pipelines**

- Sklearn pipelines don't work like they do in R, you have to decide which functions to apply in what order beforehand, and then call your pipeline like a function later
- As a general rule, the last step will be your estimator, and all the transformers come at the beginning
- In usual syntax, you need to create a pipeline object with the variable steps, where steps is a list of functions with arguments and every step needs a name
- But by using make_pipeline() instead we can skip the naming process
- These become important because even when we do everything properly, we can still cause data leakage that will interfere with our cross-validation
- This is not a drastic violation of the golden rule, but it can still affect the results
- Since all our training data is transformed, cross-validation no longer properly emulates a train/test split
- To do things properly, we need a pipeline that will redo the transformation process for every cross-validation fold
- Pipeline.fit() works differently from predict, it will fit every step before transforming, while pipeline.predict() just transforms
- Very convenient, lets us easily perform cross-validation without violating the golden rule
- If we want to perform multiple different operations on different columns, pipelines won't be enough
- The ColumnTransformer() function lets us do this by applying different transformations to different columns within the same pipeline
- To do this, first we need to identify the types of each column in our dataset, and figure out what we need to change in each column
- It's generally a good idea to sort the titles of your columns into lists
- For example, you can pass the functions StandardScaler() and your list of numerical column names to make_column_transformer() to scale all numerical features
- You also need to name every column at least once, the ones we don't want to change will go through the "passthrough" feature
- This ensures we don't break the golden rule by putting all our transformations into one big object
- Only issue is that it returns a numpy array so to turn it back into a dataframe you have to manually add column names
- Remember that if you applied one-hot encoding you'll have a bunch of new columns and you'll have to name them now
- Also you should generally make your ColumnTransformer object ahead of time and then pass it to your pipeline

**Encoding Text Data**

- We know how to deal with numerical and categorical data, but what do we do with raw text?
- As an example, think about our spam classification model
- How do you encode something like a text message?
- If you try one-hot encoding, it'll likely just make a new column for each row
- This question is the entire point of Natural Language Processing and has several solutions
- The Bag of Words or BOW representation is the most popular
- This method ignores the syntax and word order of each observation and instead just counts how many times words appear in the text
- You can get vocabulary from this which is a list of all unique words in all observations, or a variable representing the count of each word in each observation
- The CountVectorizer() function turns text documents into word counts which allows us to perform the BOW method
- The rows are the raw text, the columns are all words in the vocabulary, and the cells are the count of the word for that text blurb
- A problem with this approach is that most rows will just be 0s
- To save space, we can store these values in a sparse matrix
- This only saves the nonzero cells, but also saves their locations in the df
- OneHotEncoder also outputs a sparse matrix by default
- CountVectorizer() also has hyperparameters
- This lets us tweak which words we want to include, letting us ignore very common words or very rare words for example
- We can also remove the count feature and make the cell just show 0 if the word isn't present and 1 if it is
- By the way, CountVectorizer() is doing some preprocessing of its own
- It converts all words to lowercase and removes punctuation
- This loses a lot of information, but works surprisingly well in most cases