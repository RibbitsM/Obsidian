- Questions on the final will be more or less similar to how they were on the midterm
- First part will be [[ER Diagrams]]
- Same structure as the midterm, where you do true or false questions first and then move on to short answer
- afaik this was my weakest aspect on the midterm
- Practice questions don't include a segment on making schema, but I should assume that will also be on the exam
- Also need to study foreign key constraints and on delete statements
- Writing SQL should be fine I just need some practice
- Definitely need to review [[SQL#^267745|joins]] 
- MongoDB shouldn't be difficult but I need more practice
- More or less equivalent to SQL queries, I just need to focus on learning how to translate between the two
- Also important to memorize the syntax
- As for other stuff they will test on, it's mostly similar to the iclicker questions
- There will definitely be questions on [[Data Mining#^67283d|apriori]] and [[Data Warehousing#^a2f3ba|view materialization]]
- Both pretty easy, as long as you remember the algorithms
- HRU for views, and apriori for itemsets
- Definitely need to review data warehousing extensively because I missed one of the lectures
- Probably won't be any coverage of ethics and if there is I don't need to study for it
- Likely only going to be one section on [[Tree Indexes|hash tables and trees]], but should still review that
##### Practice
1. ``` 
Select Count(*)
From person p car c owns o accident a
Where p.sin = o.sin and o.licensePlate = c.licensePlate and c.licensePlate = a.licensePlate and a.date Like '%2002%'
Group By Distinct p.sin```
2. ```
Select Count(*)
From person p car c owns o accident a
Where p.sin = o.sin and 0.licensePlate = c.licensePlate and c.licensePlate = a.licensePlate and a.sin = p.sin ```
3. ```
Insert Into person
Values (123456, Adam James, 123 Oak st)```
