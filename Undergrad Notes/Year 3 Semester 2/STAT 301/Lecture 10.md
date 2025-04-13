- We're using the protein-mRNA example
- Can't estimate it with the traditional linear regression method
- We are instead using goodness of fit and nested models
- The protein in a given tissue can be measured by the median ratio of protein to mRNA in each gene in the tissue multiplied by the mRNA level in the tissue
- This is called an f-test, and it involves using several different models
- These models vary in complexity, from a simple linear regression with one continuous variable to a multiple linear regression with multiple categorical and continuous variables
- Lets start with our second nested model, which is a LR with one continuous variable
- Looks like this: B0 + B1mrnat + e
- This model would predict the protein level for a given level of mrna in one gene, but doesn't predict protein levels in the tissue as a whole
- Our regression line comes in the form B0 hat + B1 hat * mrnat (no error because there is no error terms in the predicted model)
- These predicted values for B0 and B1 will be output in the .fitted column in R
- This also gives us the residuals, which is the difference between our predicted line and the observed response values
- This is not the error! Just the difference between our sample and our prediction, error is for the population
- We assume that the error (represented by e) is always normally distributed, this may not be the case for the residuals

**Goodness of Fit**

- To determine the value of our model, we should compare it to our other predictor of the response value, that being the sample mean
- You can predict future values simply by saying they will likely be around the sample mean
- But is this better than our linear regression model? Lets check!
- This is basically comparing it to the "null" model where we only have the intercept and no explanatory variables
- Do this by finding the explained sum of squares of our model from before and comparing it to a model that's just a horizontal line at the sample mean
- Explained sum of squares measures how much of the variation in the data is explained by the LR compared to the sample mean
- If it is large, then our model is at least better than "nothing"
- The formula is just (predicted model value - sample mean)^2 for all values
- Residual sum of squares is similar, comparing the actual and predicted values in our model
- This is the value our model is minimizing
- Total sum of squares is the same calculation but using the null model instead, basically the variance of the sample (how far each value is from the sample mean)
- In this case, TSS is equal to ESS + RSS
- If our model is good, then the TSS should be much larger than RSS, meaning that ESS is large as well (this means our model explains a lot more compared to the null model)
- Basically the more drastic the difference between our model and the null model, the better the model
- The coefficient of determination is represented by R2 and is equal to ESS/TSS
- The reason it's squared is because little r can be between -1 and 1 when we don't have an intercept so we square it to make sure it's between 0 and 1
- Basically measures the percentage of the variance our model explains, an R2 value of 0.75 means the model explains 75% of the variation
- If all dots were on the regression line, R2 would be 1
- An alternate formula is R2 = 1 - RSS/TSS, here you can see that the lower the RSS value is, the higher R2 will be
- This formula is derived from 1 = ESS/TSS + RSS/TSS (because R2 = ESS/TSS)

**Computing in R**

- When we run our model with the mRNA data, we get a coefficient of determination of 0.07
- This is only calculated based on the observations in the sample, and as such does not help with predicting out of sample values
- Remember this is only the second model in our set of 5 nested models
- As we move up in the models and increase in complexity, R2 should increase as well
- Since adding more inputs to the model will further decrease RSS, then more complex models will always increase the coefficient of determination
- To overcome this, we adjust R2
- This looks like 1 - (RSS/(n-p))/(TSS/(n-1)) where n is sample size and p is the number of regression coefficients
- Should offset the effect by increasing the value of RSS as more inputs are added
-