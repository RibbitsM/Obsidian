> [!caution] This page contained a drawing which was not converted.   

- We can take in a lot of visual information at once, but we aren't always very good at processing that information
- When humans look at something we process the whole image at once
- With sound, we process it sequentially and have to rewind parts to hear them again
- Touch is a somewhat viable way to transfer information but our options are pretty limited
- Overall, the bandwidth of sight greatly exceeds all our other senses combined
- Visualizations let us take full advantage of this by communicating more information in a smaller space compared to text descriptions
- Not everything needs to be visualized, if our research question can be answered with a single number, then there's no need for a graph
- We can just have our program automatically spit out a number
- Statistics and calculations are best done by computers, no interpretation needed
- Also good for snap decisions like in high frequency stock trading, no time for visualization
- However, often our goal is to not replace human decision making, but inform it
- Visualizations can be used for determining results, presenting information to laypeople, refining performance, verifying automatic data, etc.
- Statistics don't tell us everything, you can have vastly different looking plots with identical summary statistics
- In Altair, we use declarative grammar, while in most other libraries we use imperative grammar
- With declarative syntax, you tell the system what data you're using, and the encoding for whatever aspects of the graph you want to specify
- For example, what's on the x axis, what's on the y axis, and what is divided by colour
- The library handles the rest
- Compare this to matplotlib, which is a very manual library that requires writing much more code to produce a similar graph to what Altair can do with one or two lines
- This gives you much more fine-grain control over the final result, but takes much more effort
- In visualization, the language/grammar we are using is the grammar of graphics
- This has six components: data, mark, encoding, transformation, scale, and guide
- The first three are required, the rest are optional
- Our data is tabular, by default Altair likes data to be input as pandas dataframes
- The primary object in Altair is the Chart, which can be made from just a dataframe
- But you can't plot a chart without a mark, which tells it how to show the data
- This is basically the graph type, should it be a bar graph, pie chart, scatterplot, etc.
- Transformations are needed to make things like histograms, but generally transformation and data wrangling should be done outside of Altair

**Class 2**

- What are all the different ways you can represent the numbers 37 and 75?
- Blog post came up with 44 ways, but this is far from the limit
- In our textbook there are 5 different data types we might want to visualize
- Items, Attributes, Links, Grids, and Positions
- Different datasets can depict different data types, for example tables are good for items and attributes while networks can show links as well
- Data has size (volume), speed at which it is generated (velocity), quality, and structure
- Data that has structure represented in terms of known data types, unstructured data is qualitative data like photos that needs to be structured
- Without context and explanation of what it means, data is meaningless
- Humans require labels to understand the semantics of data, like the column names in a dataframe
- Keep in mind these data types are different from python types like lists and dicts
-