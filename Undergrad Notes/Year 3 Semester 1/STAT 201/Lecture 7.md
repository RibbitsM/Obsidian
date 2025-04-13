- The central limit theorem states that even if a variable has a uniform distribution, when a sufficiently large number of samples are taken, the sampling distribution will be normal
- There are three assumptions here
- First, the data is obtained through random sampling
- Second, the sample is sufficiently large, meaning n >= 30
- To construct confidence intervals, we need to check these assumptions
- If they do, we can assume a normal distribution
- We can also estimate proportion with the CLT
- Can derive x/n from the sample mean
- Can also use the same method to estimate mean differences
- However, we can't use CLT to calculate variance or standard deviation, but we can use other methods

**Theoretical Statistical Methods**

- A normal, or Gaussian distribution, is defined by it's mean and standard deviation
- The mean determines the center of the curve, and the standard deviation determines the spread of the curve
- Normal distributions are symmetrical, with a bell shape and a single peak
- If you have a normal distribution with a mean of 0 and a standard deviation of 1, it's a **standard normal distribution**
- In all normal distributions, we have three rules of thumb
- About 68% of values are within 1 SD of the mean
- About 95% of values are within 2 SD of the mean
- About 99.7% of values are within 3 SD of the mean
- To calculate the probability of getting a certain value n in R, use pnorm(n, mean, sd)
- For a quantile q, use qnorm(q, mean, sd)
- A sampling distribution of means is usually sufficiently large if n >= 30, but this isn't guaranteed
- A sampling distribution of proportions is sufficiently large if n x p >= 10 and n x (1-p) >= 10
- If a sampling distribution of proportions is normal, it will have mean p and standard error sqrt((px(1-p))/n)
- If a sampling distribution of means is normal, it will have mean mu and standard error sigma/sqrt(n)
- Recall that mu stands for population mean and sigma stands for standard deviation
- For a sampling distribution to be normal, we assume the sample is random
- We also assume that the sample values are independent, meaning sample size is less than 10% of the population
- Finally, the sample must be large enough as stated above

**Confidence Intervals**

- We can also construct confidence intervals with theoretical methods and the CLT
- We call these margins of error and take this form: statistic +/- margin of error
- The margin of error is the standard error multiplied by a critical value
- This critical value depends on your confidence value, it's basically the value of the upper quantile of your confidence level
- So to calculate it in R, a confidence level of 95% would be qnorm(0.975, mean, sd)
- Of course, this only works if your sample meets the criteria of the CLT
-