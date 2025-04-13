- When making a visualization, we should consider what tasks we want our users to be able to accomplish
- These tasks can be high level or low level, depending on how specific the task description is
- For example, a high level task might be "extract insights from a graph" while a low level task would be more like "what is the range of this attribute"
- Basically the act of considering what kinds of questions people might have about this topic and how our visualization can answer these questions
- Database catalog and from data to viz are great resources for figuring out what kind of visualizations are appropriate for your data
- The database also tells you how to make these visualizations in Altair
- From data to viz gives you options based on number of attributes and their data types which is super useful
- Datavizproject.com has some more advanced visualization options

**EDA**

- Iterative process, you want to come up with a question, answer it, and then use that information to generate more questions
- Doesn't just use graphical summaries, numerical summaries are also useful and important
- Leveraging both the advantages of mass amounts of data but also your personal knowledge
- We want to facilitate data exploration done by humans, not replace it
- Other good strategies are focusing on one or two variables at a time, or doing full chart summaries like correlation plots
- We can make interesting plots even from just one variable, univariate density plots are very useful
- Basically just smoothed out histograms, show the most and least common values of a certain attribute
- You can also do this for multiple variables with stacked or overlapping histograms
- Same works for categorical variables too, just do a bar chart instead of a histogram
- Scatterplots are also good, specifically for finding correlations between two variables
- Always want to at least examine your distributions, you want to know if you have normal, bimodal, gaussian, etc
- EDA also helps a lot with knowing what you need to do later once you move on to cleaning and feature engineering
- We can also tidy our data by turning all our columns into variables in a single column which will let us encode column into a channel like colour
-