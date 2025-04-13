- Ensembles are models that combine multiple different machine learning models
- For an example, many years ago Netflix made a contest to improve their recommendation algorithm and the winner was an ensemble algorithm
- Kaggle also hosts many similar contests and usually the winning model is also an ensemble
- The idea is that by combining many different models they can compensate for their respective shortcomings
- There's a couple of different kinds, but we will focus on tree based ensembles
- Decision trees are good because they're interpretable and lack the shortcomings of linear models but usually overfit
- By combining multiple decision trees, we can make a significantly stronger model

**Random Forest**

- Since single decision trees tend to overfit, why don't we use several different decision trees and average the results
- Models are created randomly to create differences, and we can use n_estimators to control the number of trees we create
- Every tree is trained on a bootstrap sample from the dataset, so they all are sampling from the same source but each tree is trained on a different sample
- The second random aspect is that at each split, a random subset of features is chosen and the tree only calculates the gini index of those features
- This number is determined by the max_features hyperparameter
- To get the final numbers, we average the output of all trees in the forest
- Other than n_estimators and max_features we can also still control max_depth
- However, since we want specialized trees it's usually better to leave max_depth unchanged or set a high value
- All of these hyperparameters increase complexity at higher values
- One of the main benefits of this model is that you actually don't have to tune the hyperparameters carefully to get good results
- Also since it's non-linear you don't need to scale the data
- Some weaknesses are that they are difficult to interpret and scale poorly to high dimensions
- Since random forests are less prone to overfitting we can use higher values of hyperparameters like n_estimators without worrying about compromising results
- The main limitation will be resources and time, not the fundamental tradeoff

**Gradient Boosted Trees**

- Compared to the random forest approach, there is no randomization in gradient boosted trees
- This approach utilizes early stopping to create many shallow decision trees and then combine them
- Also the trees are not independent, each tree knows what mistakes the previous tree made and tries to correct it
- Two hyperparameters, n_estimators controls the number of trees and learning_rate affects the strength of corrections made by the trees
- Both of these increase complexity as they increase
- XGBoost is not part of sklearn and has to be installed
- It supports missing values and sparse data and generally does better than random forest
- LightGBM is similar but creates smaller models and is quite fast
- CatBoost creates better scores than the previous two but is much slower
- The simple answer to the question of what classifier you use is just whatever gets the highest CV score assuming your validation set is fine
- This gets more complicated when we consider how important interpretability is, should be use something simpler because its more understandable?
- Another consideration is code maintenance, Netflix never used the winning algorithm because it was too complicated to maintain

**Stacking and Voting**

- Ensemble strategies are not limited to decision trees
- With VotingClassifier you can combine the predictions of any number of classification estimators
- We can either use soft votes (predict_proba) or hard votes (predict) to determine the output
- Each model casts their vote which is their prediction for a certain observation, and the final classification is the most common vote
- Also you can get the prediction probability from the voting classifier
- However, this is an average and there's no guarantee this will improve your score
- Voting classifiers are more reliable, but not necessarily more accurate
- Stacking classifiers assign different weights to different models
- This lets us extract more information from our most useful models and lower the importance of our less useful ones
- The result is what is called a metamodel, which is a model learning from several smaller models
- Instead of voting, the output of one model is fed into another model
- By training a logistic regression on the predict_proba outputs of several different models, we can assign coefficient weights to them
- The features of the LR are the different models
- Via machine learning, we can figure out which models output the most reliable results and use this information to refine our predictions
- For example, our metamodel assigned negative weight to decision tree, and a higher weight to light gbm
- This also doesn't have to be a logistic regression model, you can also use decision tree as your meta estimator
- Results will be more interpretable, but likely will be worse than LR
- Ensembles can certainly give you a higher score but are also significantly slower
- To remedy this, you'll need to start thinking about feature selection
- Btw there are regressor equivalents to all of these classifier models
-