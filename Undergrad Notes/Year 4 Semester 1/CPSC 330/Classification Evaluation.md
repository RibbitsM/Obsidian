**Confusion Matrices**

- We plot confusion matrices with plot_confusion_matrix() in sklearn
- This is a graph showing the number of true and false negatives and positives
- This also lets us calculate a number of other metrics
- Generally speaking, in a binary classification problem the "positive" value is the thing that we are looking for in our question
- We can also create our matrices as numpy arrays and calculate them from our cross-validation function
- One of the metrics calculated from confusion matrices is accuracy, which is the metric calculated by the .score() method by default
- The problem with this metric is that it isn't great when there are an unequal ratio of negatives to positives
- For example, if you're trying to diagnose a very rare disease you could get a great accuracy score by just saying every patient is healthy
- The three other main metrics we'll use in this class are recall, precision, and f1 score
- Recall calculates the identification rate among all positives
- The formula is just TP over TP + FN
- Precision is the number of actual positives among all examples classified as positive, which is TP over TP + FP
- The f1 score combines these metrics, the formula is 2*((precision*recall)/(precision+recall))
- A PR curve calculates the values of precision and recall at every possible threshold, and can be useful for optimizing the threshold
- The AP score is the measure of area under the curve on the PR curve and tells us how well our model is performing
- The ROC curve is similar except the axes are the true positive rate and the false positive rate
- We want a low FPR and high TPR and the ROC curve is very good for optimizing this
- Generally, AP score is good for unbalanced models and ROC is good for balanced models
- A model with an excellent accuracy score could have a terrible recall and precision score
- You don't have to calculate all these on your own, sk learn has functions to do this for you
- An excellent one is classification_report() which takes a validation set and a set of predictions as well as the target names
- This function shows you metrics for each level of the response as well as the average, which is super useful
- It also gives two options, macro and weighted average
- Macro average give equal importance to all classes, while weighted average will weight it by the number of samples in each class
- Generally we want to use weighted average in binary problems
- We can also make cross_validate maximize for different metrics, not just accuracy

**Class Imbalances**

- Like the rare disease example earlier, most real world datasets are very imbalanced
- However, an important question to ask is if a class imbalance is because of the nature of your question, or because of your methodology
- If you think that your data collection method is creating a class imbalance, generalization will be much harder
- However, in some cases its okay to just ignore it
- Another important thing to consider is what kind of error is most important for your question
- Depending on the context you might want to maximize true positives or true negatives or minimize false positives/negatives
- Apart from adjusting our data, we can also control the training procedure to account for class imbalance
- Some options are under and oversampling, which lets you increase or decrease the examples of a certain class
- The main way to adjust the training procedure is via a parameter called class_weight
- All sk learn estimators have this, and let us assign more weight to our most important class or lower the weights of other classes
- Class_weight = 'balanced' gives all our classes the same weight, so undersampled classes are beefed up and others are brought down
- This can improve some metrics significantly, especially accuracy
- If you can't find a good value for class_weight, you can also use hyperparameter optimization methods to find one
- We can also apply the idea of balancing to splits
- By adding the argument "stratify" to train_test_split() you can maintain an equal ratio of positive to negative in both splits
- Fun fact, our cross validate function automatically stratifies folds
- Doing this method does make your samples a little less random, but generally this is acceptable
- Stratify works best in multiclass cases, especially if you have one very uncommon class