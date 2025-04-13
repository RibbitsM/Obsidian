> [!caution] This page contained a drawing which was not converted.   

- All Altair charts are created with JSON specifications that allow the user to replicate this visualization in any browser
- This specification also includes the original dataset as well, allowing it to run in any browser even without the dataset or a Python compiler
- This means that there is a restriction on dataset size, 5000 is the max amount of rows that can be embedded in a visualization without having to run .disable_max_rows()
- Another option is to use a data transformer to shrink the file size using VegaFusion
- Tooltips are good for encoding more data
- Small multiples are a powerful tool allowing you to fit more graphs within a graph
- You can even incorporate tooltips into these to make them more readable even at a small scale

**Class 6B**

- Who are the audience? What are their needs and considerations?

|   |   |   |   |
|---|---|---|---|
|Data Attribute|Semantic|Attribute Type|Cardinality|
|State|Name of the state in Wakanda|Categorical|10|
|Time of collection|Time the tweet was collected, not posted|Temporal|[10:00, 9:00]|
|Volume|Total number of tweets/mentions made during the last 10 minutes|Numerical|0 <=|
|Amount of Change/Variability|Variation in sentiment over the last 10 minutes|Numerical|[-2,2]|
|Average Sentiment|Sentiment on a candidate between 1 and -1|Numerical|[-1,1]|
|Candidate Name|Name of candidate|Categorical|2|
|Date|Current date|Temporal|[2023-10-18, 2023-11-01]|

|   |   |
|---|---|
|Task Group|Question to Explore|
|Retrieve Value|What is the current average sentiment towards M'baku in Rivendell?|
|Filter|What did sentiment for all candidates and states look like at 2 pm on October 24th look like?|
|Compute Derived Value|What is the average volume of tweets from Isengard mentioning Gandalf?|
|Find Extremum|Which time period had the greatest combined volume of tweets?|
|Sort|Which candidate currently has the most positive sentiment in each state?|
|Determine Range|What are lowest and highest sentiment values recorded for either candidate?|
|Characterize Distribution|What is the density distribution of average sentiment values coloured by candidate?|
|Find Anomalies|Which periods of time had abnormally high variation?|
|Cluster|Which states have overall higher sentiment for M'baku? Which states have overall higher sentiment for Gandalf?|
|Correlate|Is there a correlation between state and average sentiment towards M'baku?|