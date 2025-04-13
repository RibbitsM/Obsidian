- An A/B test is a test to compare two variations of a product/service
- A is the control and B is the variation
- Basically a comparison of population quantities from two different distributions, like comparison of two means or comparison of two proportions
- This method is often used for improving websites
- An example was when Obama's campaign tested two different variations of their website
- In this case, the purpose of the website was to attract donations so the response variable could be proportion of visitors who donated
- The covariates are the elements in the experiment affecting the response variable, in this case it could be the colors of the webpage, the graphics used, etc.
- A/B testing also needs an aspect of randomization to avoid bias, control and variation groups are distributed at random
- The final thing required is a way to compare the two samples, which is our case would be hypothesis testing
- Once you have all this, run the experiment and then analyze the data to get your conclusion
- For an example, lets say our question was whether the new (variation) website lead to larger donations to the campaign?
- To randomize, we would randomly allocate 1000 viewers to each site
- This is called a randomized controlled experiment
- For our methodology we can use a classical hypothesis test (t-test) using the CLT

**New Developments in A/B Testing**

- We now have tools that allow us to witness the progress of tests in real time
- This allows us to stop tests early before all data is collected/processed if the current results are significant enough
- In classic hypothesis tests, the sample size is set in advance but we don't have to do this
- Since we can monitor p-values on the fly, we can stop and even re-design the experiment midway through
- For an example of why we might stop an experiment early, imagine a clinical trial of a drug
- Out of 1000 participants, half will receive the drug and half will receive a placebo
- So far, 600 people have participated and none of the variation group have died, but 2/3rds of the control group have died
- Should we finish the experiment with the remaining 400 people, or stop the experiment?
- Here it's an ethical issue, but in other cases the issue is funding or accuracy of outcome
- The assumptions of classic hypothesis testing still hold since every time we "peek" at the final data we're essentially performing a single hypothesis test with a fixed sample size
- In effect, we are performing multiple experiments with different sample sizes
- Just like in ANOVA, this affects our probability of type 1 error since we're performing multiple comparisons
- Without accounting for this, the p-values we are seeing every time will be unadjusted, like performing ANOVA without using Bonferroni correction

**A/A Testing**

- In order to tests the effects of early stopping we need a null model
- For this we do A/A testing where we create a scenario where both groups are the control
- In this scenario, we know for sure that there should not be a significant difference
- We run the experiment and sequentially collect the data in small batches and analyze it
- This produces a graph of the raw p-values for many different sample sizes in the scenario where getting a significant result is false
- For example, each group could be a sample of 1000 and we collect in batches of 50 per sample
- If our A/A test gave even one p-value below 0.05, then stopping the test as soon as a significant result is achieved would be a mistake
- This is what happens when you stop a test early, you inflate your chance of type 1 error and make it more likely to reject a correct null hypothesis
- To see how likely this is to happen, we need to run many of these tests
- Lets say we run 100 A/A tests and in 5% of them there was a value below the significance level
- This is good, our chance of type 1 error is 5% as it should be
- In summary, most of the time stopping our experiment early will result in an increase in type 1 error