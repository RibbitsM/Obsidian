**Generalization**

- Generalization is the process of applying patterns from a limited set of data to similar unknown data
- This is the goal of machine learning, to generalize from limited data
- The more advanced your model becomes, it also becomes more adapted to the specific training data
- This is called overfitting, and can interfere with a model's ability to correctly identify data outside of the training set
- Generalization is the fundamental goal of machine learning, to reach beyond our training data and generalize it to real-world examples
- We usually consider two different kinds of error in machine learning
- First is the error on the training data, and the second is the error on the full distribution
- However, since we don't have access to the full distribution of any real data, we cannot access the error of the full distribution
- We can only estimate this error, which is called the generalization error

**Data Splitting**

- A way to estimate this error is to split our data into training and testing data
- We just fit the model on the training data, and score it with the testing data it hasn't seen yet
- In the scikit learn workflow we do this with the test_train_split() function
- All you have to do is input your X and y data and specify the proportion you want to be test data
- We can also split the whole dataframe if we want to keep the target values in the training data for graphing purposes
- There is no real rule on what kind of split you need, some common ones are 80 20, 90 10, or 70 30
- You can also set a random_state to get a reproducible split
- Another thing people like to do is add a validation split
- This is a portion of the data set aside from the test and training data to be used for tuning hyperparameters
- We never need to actually fit the validation data but just use it as test data to score your models while tweaking hyperparameters
- Test data is only used to evaluate the final model after we have finished building it
- The final kind of data is deployment data
- This is the data the model will deal with in the real world, and we don't know the target values of this data
- This is what the validation and test sets are trying to emulate
- Deployment data is only for prediction, and has an unknown error

**Cross-Validation**

- Depending on the size of your dataset, your training data may be quite small after doing all the splitting
- If this happens, you may encounter problems with validation
- One way to overcome this is cross-validation
- This process divides your data into "folds" and runs the same test multiple times until every fold has been used as the validation set
- Way to get more gas out of your limited data
- The number of folds can be whatever you want, 10 is recommended
- Main limiting factor is the size of your training data and the power of your CPU, this is a computationally intensive and time-consuming process
- To do this in scikit learn, pass your unfitted model, number of folds, and training data into the cross_validate() or cross_val_score() function
- cross_validate() is more powerful because you can see the train scores as well as the validation scores

**Fundamental Tradeoff of ML**

- A typical problem to encounter in ML