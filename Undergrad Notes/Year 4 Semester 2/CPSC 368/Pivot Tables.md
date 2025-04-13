1. Select Avg(pi.height), Avg(pi.weight), Avg(pi.bmi), Avg(pi.age)

From PlayerInfo pi  
Group By pi.team  
Order By pi.olympic_year, pi.country
 
Select Avg(pi.height), Avg(pi.weight), Avg(pi.bmi), Avg(pi.age)  
From PlayerInfo pi  
Group By pi.team, pi.olympic_year
 6. I definitely think that working with pivot tables was easier, but at this point I'm much more comfortable with databases. Pivot tables would be better for simple operations, especially ones that involve aggregating and grouping like finding the average and sum of all columns and then grouping by another. But more specific questions, like finding lists of all rows that meet a certain criteria like Canadian womens hockey players born between 1985 and 1992, can only really be done effectively through a database. 
I did use ChatGpt to complete this assignment, but I did not work with anyone else. Here are all the prompts I used:
 
Using a provided csv file, can you write me a formula to create a new column?
 
Here is the .csv file, I am using Google sheets
 
Create a column called Age and use the DATEIF function to calculate the age of each player by the start of the Olympics