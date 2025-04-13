- Recall that A/A testing is used to find the risks of early peeking
- Creates opportunity cost for running longer experiments

**Sequential Testing**

- Multiple comparisons performed sequentially
- Sample size is dynamic, not fixed
- Several different classes
- Group sequential designs are when the inspection interval is set beforehand
- This way, each analysis is like taking a fixed sample
- A full sequential design is when you do the analysis after every single observation in sequence
- There are several correction methods, apart from Bonferroni you can use Pocock or other methods
- Bonferroni correction can change p values, alpha, or the critical value
- These all have the same result of reducing type 1 error, but do it in different ways
- Using Bonferroni's correction will always make your test more conservative, and less likely to reject H0
- Another method is the Pocock method
- This creates a boundary, or a common critical value for all analyses
- For this we use the gsDesign() function
- For this you need to set the number of analyses, test type, effect size(delta), alpha, and beta
- Pocock's boundary is usually less conservative than the bonferroni correction and will result in a slightly higher type 1 error
- Another method is the O'Brien-Fleming boundary
- Instead of a set value, this method gives a different boundary for every test
- Makes boundary less conservative as sample size increases to avoid incorrectly rejecting H0 with a small sample
- Starts extremely conservative, even more than Bonferroni
- Our goal isn't to minimize rejections, but get our false rejection rate to the same as our initial alpha value
- For example if we use an alpha of 5 with 100 experiments, we'd expect 5 false rejections
- Bonferroni would give us less like 2, Pocock might give us 7, and O'Brien-Fleming is generally the closest around 4-6 rejections