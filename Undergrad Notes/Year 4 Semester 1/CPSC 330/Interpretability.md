- Why do we care about interpretability?
- In many cases, how our model makes its predictions doesn't really matter
- For example, models for interpreting speech or filtering out spam
- But if our model is for predicting crime victimization or diagnosing diseases, we would want to figure how the model is doing it
- Plus, it's easier to identify issues and biases with your model if you can more easily understand it
- For us, the most important thing to understand about a model is the relative importance of different features
- Which features are most used by the model and which are least used?
- Usually, simple models are more interpretable but less accurate and vice versa
- With linear models like logistic regression this is easy, all you have to do is look at the coefficients to get an easy depiction of what variables influence classification in one direction or another
- For non-linear models, things are more difficult
- In sklearn, most models have an attribute called feature_importances_
- For non-linear models like trees, this is calculated from the gini index
- Doesn't work for all, for example SVM RBF doesn't have this attribute
- This attribute only tell us the relative influence of features, and nothing about the sign of these features
- Meaning, we know that a feature is important but we don't know if it is a positive or negative predictor
- This is because these models are non-linear, meaning features aren't strictly positive or negative, they can be both
- To find the feature importances of models outside of sklearn by using the eli5 tool
- To use it, type eli5.explain_weights() and input your fitted model
- The output is very similar to feature_importances_

**Feature Importance**

- We can also examine feature importance before we even create our model, correlation charts help us assess which features are most correlated with the target
- While we can pretty confidently say that features with high correlation will be useful, these are only linear relationships and we can't discount low correlation features
- Gives some information, but hardly a complete picture
- Unrelated fun fact, with your fitted transformer you can do transformer.get_feature_names_out_ to avoid having to assemble all the new feature names yourself
- With coefficients for ordinal features, the coefficient for a specific level signifies the change in the target value on that level compared to the one below it
- For categorical features, you need to choose a reference category yourself
- If you subtract the value of the reference coefficient from all other category coefficients, what you end up with is the change in target value compared to the reference category
- It's good to examine the magnitude of your coefficients and consider their applicability to the real world
- For example, our housing prices model predicts that a house having clay tiles drops its value by almost $200k
- Numerical features are interpreted as usual, its the increase in target value corresponding to the increase in one unit of the feature
- However, our numeric features are scaled so it's actually not one unit exactly, it's one scaled unit
- This makes it a little harder to translate these coefficients into real world terms, but makes comparing different features much easier
- Of course, you can always just find how much your features were scaled in the first place and use that to find the coefficient for the original units

**Interpretability**

- While feature importances for linear models are pretty easy to get, it's a lot harder for non-linear ones
- With models like decision trees we can just use the gini index, but distance-based analogy models like KNN and SVM RBF don't even have the concept of feature importance
- Even with linear models, features being correlated with each other can cause further problems
- In our housing data, we have a couple features that are highly correlated
- This can affect feature importance by splitting the utility across two or more features that are correlated with each other
- If a feature is useful, there must be some kind of relationship between that feature and the target
- One way to measure this usefulness is to see what happens to the model performance when we disrupt this relationship
- In sklearn, we can achieve this through the permutation_importance method
- This arbitrarily perturbs the values of a certain feature and then measures the corresponding change in model performance
- Just like the feature_importance method this only gives us magnitude, not sign
- This works for linear models like logistic regression as well as tree based models like RandomForest
- Permutation importance is good because it is model agnostic, and it lets us measure feature importance even on models like KNN and SVM RBF
- All these are good to look at features globally, but what if we want to understand a specific prediction?

**Shapley Values**

- This is a concept from game theory that attempts to determine individual contribution on a team effort
- In machine learning, each feature is assigned one of these values that shows the contribution of that feature to a specific prediction
- The model has an average "raw score" which is the prediction we would expect if we averaged all the feature values
- The SHAP values show how this prediction deviates from that raw score by showing how much it adds or subtracts from the average
- We do this with a method called SHAP
- SHAP values can be positive or negative, meaning the feature was leading the model to a positive prediction or a negative one
- We use a special package for this, which also lets us make excellent visualizations
- Waterfall plots show the magnitude and direction of SHAP values for all important features in a certain prediction
- Force plots overlap arrows from waterfall plots
- You can also plot multiple SHAP predictions in one graph
- These plots can get very complicated and detailed, the SHAP package is very powerful
- You can also take average Shapley values for the whole dataset to find the most useful variables overall
- We can also visualize the distribution of Shapley values for one or more variables
- SHAP has different explainers for different models, here we used TreeExplainer