**Linear Regression**

- Linear models assume a linear relationship between x and y
- A simple linear model has two parameters, the slope and the y intercept
- However, this only works for one feature, as model complexity increases more parameters are added
- In python, as we add more features, there will be new coefficients for each new feature, and instead of the y intercept we have the bias term
- This allows us to make predictions outside of 2 dimensional space
- Traditional linear regression is weak to multicollinearity and overfits easily, so we use Ridge instead
- Data is colinear when multiple feature correlate with each other, which is very common
- This adds a parameter that controls the complexity of the model and prevents unreasonably large coefficients
- Most of the time we will want to use Ridge() because our data will have multicollinearity
- Compared to LinearRegression(), this model has an additional hyperparameter called alpha which controls the complexity of the model
- This means that our ridge models will be more regularized and will have less extreme coefficients
- Also, having alpha means we can control the fundamental tradeoff by increasing alpha, as small values are likely to cause overfitting
- To do this, we just make our estimator Ridge() and fit, predict, and score the data normally
- A new thing this model can do is return a coefficient and y intercept we can access via model.coef_ and model.intercept_

**Logistic Regression**

- We can also use this method to predict binary features using logistic regression
- Contrary to the name, this model is not actually for regression problems
- This uses the sigmoid function to predict the probability of either a 0 or 1 outcome, represented by a decimal between 0 and 1
- The decision boundary here is the point on the x axis representing your feature maps to a predicted probability of 0.5 on the y axis
- In our example, below 3 hours studied our model predicts a fail, but above 3 hours it predicts a pass
- The model is learning a threshold that it can use to determine the class of a unknown value based on its features
- These classes are always binary, for example we can think of a sentiment analysis program that predicts whether a review is positive or negative
- This model would learn key vocabulary words and assign coefficients to them, either positive or negative
- The inputs are either 0 or 1, depending on if the associated word is present in a review or not
- Multiply the coefficients by either 0 or 1, and tally up the results
- If the resulting number exceeds the threshold, the review is positive and if it doesn't the review is negative
- The formula looks very similar to linear regression, but with the addition of a threshold value r
- Just like in Ridge, we can access the coefficients and intercepts the same way
- Our threshold is also our decision boundary, which will be a straight hyperplane on our graph
- This is weak at lower dimensions and is easily outclassed by models like SVM RBF, but scales well to high dimensions
- The most important hyperparameter for LogisticRegression is C, which controls the tradeoff and overfits at large values
- Both linear and logistic regression are parametric models, which means they have a fixed number of parameters no matter the size of the dataframe

**Predicting Probabilities**

- predict_proba is a method for models in sklearn which can give us the confidence the model has is classifying an example
- This is a soft prediction, instead of just outputting the prediction like .predict, this tells us how close the decision was
- Also lets us see how confident the model is in different cases
- Useful to know when our model is confidently getting things wrong or getting things right with low confidence
- Generally relates to the distance from the point to the decision boundary
- This is done through the sigmoid function, which allows us to convert raw model output to a result between 0 and 1, a probability value
- When you call predict_proba, we'll get two numbers
- The first is the probability for the negative outcome, and the second is for the positive outcome