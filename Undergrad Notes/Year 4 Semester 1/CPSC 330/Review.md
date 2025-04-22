- What is ML? When is it suitable?
    
    - Process of writing a program to solve problems on its own
    - Suitable for very rules-based question, almost always quantitative and issues that have tabular data available
- ML terminology
    
    - Feature: Something that our model tracks, a variable in our data we use to create the output
    - Target: Whatever our model is trying to predict, usually a known variable in supervised ML
    - Example: A row of feature values that describe one "unit" in our dataset
    - Training: The process of feeding our program data so it can learn the patterns and develop the capability to perform prediction on its own
- ML types
    
    - Supervised machine learning requires data with known target values
    -  Train and test your model with your known data, and then deploy it to predict unknown targets 
    -  Unsupervised machine learning finds patterns in data without a target 
    -  Usually used for grouping datasets 
    -  Reinforcement learning teaches a program how to perform a task by assigning benefits and penalties to specific actions 
    -  Great for developing AI for video games, facial recognition, etc. 
    -  Recommendation systems predict preference for unknown items 
    -  Usually develop unique models for each user, different from supervised ML because no target but also not quite like grouping    
-  What are four splits of data we have seen so far? 
    
    -  Training data is used to create our model, never used for testing or validation 
    -  Validation data is used to fine tune our model by testing out different variations of the model 
    -  Test data is used to calculate the final performance of our model, and is never touched beforehand 
    -  Deployment data is what our model will be working on once it is finished, and we don't know the true values for this split 
-  What are the advantages of cross-validation? 
    
    -  You can validate your model without making a devoted validation split 
    -  Can get more utility out of smaller datasets where you don't want to split them up too much 
-  Why it’s important to look at sub-scores of cross-validation? 
    
    -  To make sure performance is consistent, if our model is giving inconsistent results that's not good 
    -  Just looking at mean validation score doesn't tell you everything 
-  What is the fundamental trade-off in supervised machine learning? 
    
    -  As our model becomes more complex, it becomes more specific to its training data 
    -  We want a model that is complex enough to not oversimplify the issue, but simple enough that it will be able to function using data outside the training set 
-  What is the Golden rule in supervised machine learning? 
    
    -  Never let your training data leak into your validation/testing data and vice versa 
    -  This will mess with your results and will prevent you from finding out the true ability of your model 
- Scenarios for data leakage 
    
    - This can happen at almost any part of the process, but the most common occurrence is training data being used for validation 
    -  Things to keep a close lookout for are including information from the target variable when transforming your data and fitting your preprocessor every time you cross-validate to avoid data from other folds contaminating your future folds  
**Pros, Cons, Parameters and Hyperparameters**
 -  Decision trees 
    
    -  Parameters: nodes in the decision tree 
    -  Hyperparameters: most important is max_depth which controls how specific a tree can get 
    -  Pros: Easy to use and easy to interpret, also fits and predicts fairly quickly, can model non-linear relationships 
    -  Cons: Not very strong, performs poorly on complex questions 
-  KNNs, SVM RBFs 
    
    -  Parameters: none, both models are non-parametric 
    -  Hyperparameters: For KNN you choose the number of neighbours, and for SVM RBF you choose the values of C and gamma which both increase complexity 
    -  Pros: Both fit very fast, SVM RBF works in high dimensions, KNN is interpretable, and both can model fairly complicated relationships given enough data although SVM RBF does it better 
    -  Cons: KNN is very weak at high dimensions, both predict very slowly, and SVM RBF is hard to interpret 
-  Linear models 
    
    -  Parameters: intercept/bias and coefficients of the model 
    -  Hyperparameters: Depends on the model, but for Ridge the main hyperparameter is alpha, which is a penalty term which simplifies the model at high values, logistic regression straight up has C 
    -  Pros: powerful, simple, and interpretable. Logistic regression in particular can stack up well to much more complex models with the proper hyperparameter tuning 
    -  Cons: Relies on data being linearly separable, you can get around this with feature engineering but it takes a lot of exploration and time 
-  Random forests 
    
    -  Parameters: individual trees and their respective nodes 
    -  Hyperparameters: n_estimators which controls the number of trees created, max_features which determines the number of features each tree is trained on, and max_depth which is the depth of each individual tree 
    -  Strengths: Performs well with default hyperparameters, doesn't suffer from the fundamental tradeoff, same as decision trees but better mostly 
    -  Weaknesses: limits on performance, especially on high dimension data, takes up a lot of computing power and are hard to interpret 
-  Gradient Boosting, LGBM, CatBoost 
    
    -  Parameters: individual trees and their nodes 
    -  Hyperparameters: same as random forest but without max_features and the addition of learning_rate which controls the amount of information trees can learn from their predecessors 
    -  Strengths: Very effective models, excellent performance and fit/predict times, especially LGBM 
    -  Weaknesses: Not interpretable, take a little more tweaking and may struggle at high dimensions 
-  Stacking, averaging 
    
    -  Parameters: the output of the models that make up the ensemble 
    -  Hyperparameters: generally none other than the parameters of the constituent models, all you have to do is set if you want hard or soft voting for averaging 
    -  Strengths: Very consistent and reliable results, can handle a vast variety of data and is limited only by the quality of models you used 
    -  Weaknesses: Your results will likely not be as good as the best model in your stack  -  What are various data preprocessing steps such as scaling, OHE, ordinal encoding, and handling missing values. Why and when each step is necessary? 
    
    -  SimpleImputer: Used for imputing, or filling in missing values. This can be done via dummy methods like filling in missing values with the mean, median, or mode or using a method like KNN. You'll only need to use this preprocessor if your data has missing values. 
    -  StandardScaler: Used for standardizing or normalizing numerical data, ensuring that all features use the same units and their coefficients will have the same magnitude. You only need to do this if you are using a model that cares about units, generally a linear model like logistic regression or a model that uses distance calculations like KNN or SVM RBF. Decision trees and tree ensembles do not require scaling. 
    -  OneHotEncoder: Used for converting text variables with distinct categories into numerical variables. You'll need this if you have any feature that isn't numerical but also can't be put in a hierarchy, one example would be the color of a car as opposed to the engine class. 
    -  OrdinalEncoder: Used for converting text variables with distinct categories into numerical variables. You'll need this if you have a feature that has a clear hierarchy, like maximum level of education achieved. 
    -  CountVectorizer: Used for converting text variables without distinct categories into numerical variables. You'll generally only need this if your data has a feature that is a large amount of text where every observation is likely to be unique. CountVectorizer() works by creating a "bag-of-words" representation where each unique word in the entire dataset gets its own column one-hot encoding style. 
    -  TransformedTargetRegressor: Used for transforming the target or y values, usually done if the distribution of the target variable is non-normal. Fixing skewed distributions by log transforming the target variable is fairly common practice in machine learning 
-  What’s the difference between sklearn estimators and transformers? 
    
    -  Estimators are your models, and they are unique because they output predictions, while transformers just output the input data in a different form 
-  Can you think of a better way to impute missing values compared to   SimpleImputer  ? 
    
    -  I mean SimpleImputer covers a lot of different options but you could go further in the implementation of KNN and use other models for imputation like decision trees or even linear regression 

**One-hot encoding**

-  What’s the purpose of the following arguments of one-hot encoding? 
    
    -  handle_unknown=”ignore” 
        
        -  This is to prevent errors from popping up during cross-validation if you have a category that appears in the validation fold but not the training fold 
    -  sparse=False 
        
        -  This is to prevent the output dataframe from being converted to a sparse matrix, making it easier to examine 
    -  drop=”if_binary” 
        
        -  This automatically ignores any columns with only two categories and instead converts one category to 0 and the other to 1 instead of doing one-hot encoding 
-  How do you deal with categorical features with only two possible categories? 
    
    -  You use OneHotEncoder with drop="if_binary" 

**Ordinal encoding**

-  What’s the difference between ordinal encoding and one-hot encoding? 
    
    -  Ordinal encoding assumes ordering within the categories and does not separate each category into its own feature 
-  What happens if we do not order the categories when we apply ordinal encoding? Does it matter if we order the categories in ascending or descending order? 
    
    -  If we don't order the categories, by default OrdinalEncoder will just order them as they appear in the data, which is generally not helpful at all 
    -  It does matter, by default you should order them in ascending order 
-  What would happen if an unknown category shows up during validation or test time during ordinal encoding? For example, for   class_attendance   feature what if a category called “super poor” shows up? 
    
    -  Unlike OneHotEncoder, there is no handle_unknown parameter for OrdinalEncoder, this is a really tough problem to deal with that you just kind of have to make sure doesn't happen by making sure all levels are accounted for during ordering 
-  Since   enjoy_course   feature is binary you decide to apply one-hot encoding with   drop="if_binary"  . Your friend decide to apply ordinal encoding on it. Will it make any difference in the transformed data? 
    
    -  No it won't! 
-  In what scenarios it’s OK to break the golden rule? 
    
    -  Generally never, but some small exceptions exist like when we split our data with traintestsplit by default it balances the positive and negative classes in each split which does violate it a little 
-  What are possible ways to deal with categorical columns with large number of categories? 
    
    -  If they're not ordinal, your best bet is often just doing one-hot encoding 
    -  Another strategy is to try and find similar categories and merge them to reduce the number of categories 
    -  If there are many categories that only appear once or are otherwise very uncommon you can sometimes ignore those categories without much consequence 
-  In what scenarios you’ll not include a feature in your model even if it’s a good predictor? 
    
    -  A common issue in feature selection is multicollinearity, which occurs when our features are correlated with each other 
    -  This can cause issues with prediction, but also can make choosing which variables to remove difficult 
    -  You might want to remove one feature if you have a pair of closely correlated features, even if one of those features may have a high coefficient to test if its prediction power is just an artifact of the multicollinearity 
-  What’s the problem with calling   fit_transform   on the test data in the context of   CountVectorizer  ? 
    
    -  You never want to call fit on the test data because of the risk of breaking the golden rule, you should just train your preprocessor on the training data and apply it to the test data 
    -  One way to think about this is considering how our model will work in real life, you want it to use the knowledge it learned from the training data to apply that to new data 
-  Do we need to scale after applying bag-of-words representation? 
    
    -  No, scaling after applying bag of words is a terrible idea because it would be incredibly computationally intensive due to the massive amount of columns created 
    -  Also, all of the columns created by bag of words act similar to one-hot encoding columns which don't need to be scaled because they are not really continuous, the values are just the count of words appearing in that text 
-  What makes hyperparameter optimization a hard problem? 
    
    -  The main obstacle is the massive amount of options, there are near-infinite combinations of hyperparameters we can use for any given model 
-  What are two different tools provided by sklearn for hyperparameter optimization? 
    
    -  GridSearchCV takes a matrix of hyperparameter values and tests all possible combinations within that grid via cross validation 
    -  RandomizedSearchCV takes distributions of hyperparameters and takes a set number of samples from those distributions and tests the values via cross validation 
-  What is optimization bias? 
    
    -  Optimization bias is similar to overfitting, and occurs when you accidentally optimize your hyperparameters to perform well on the existing data, but this doesn't transfer over to the deployment data 
    -  A common reason for optimization bias is sloppy cross-validation processes that result in data leakages 
-  Hyperparameter Optimization Methods 
    
    -  Nested for loops 
        
        -  The sloppiest and most inefficient method 
        -  Basically is grid search but requires many more lines of code 
        -  You can use this for some quick tests, the main advantage is being able to test just a few values without having to go through a full iteration of GridSearchCV or RandomizedSearchCV 
    -  Grid search 
        
        -  Likely the most consistent method 
        -  Advantages are having control over the values that get tested as well as the range of values getting tested, more control than randomized search and more efficient and comprehensive than nested for loops 
        -  The problem with this is that you're necessarily excluding a lot of possibilities, it's really easy to mess up a grid search if you don't have a good idea of what intervals to test 
        -  Also can be extremely slow once the number start to add up, especially if you have three or more hyperparameters 
    -  Randomized search 
        
        -  Overall best method in most situations 
        -  Main advantage is that you can technically test all possible values since there is always the possibility that any given combination within the distributions will be tested 
        -  It's also more straightforward in terms of how long it will take, no need to do math to figure out the number of iterations when you can just set it directly 
        -  Problems are that you do need a decent amount of domain knowledge to know which distributions to use, and there is always the possibility of just getting unlucky with the value choices 
-  Understand different metrics used to evaluate machine learning models like accuracy, precision, recall, F1-score, and PR curve, ROC curves for classification; mean squared error, root mean-squared error, MAPE and r2 for regression. Be prepared to discuss why you would choose one metric over another based on the problem context. 
-  Why accuracy is not always enough? 
    
    -  Accuracy ignores class imbalances, 
-  Why it’s useful to get prediction probabilities? 
-  In what scenarios do you care more about precision or recall? 
-  What’s the main difference between AP score and F1 score? 
-  What are advantages of RMSE or MAPE over MSE? 