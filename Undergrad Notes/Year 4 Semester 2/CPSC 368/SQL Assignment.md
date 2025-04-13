1. SELECT a1.firstName, a1.lastName

FROM ActedIn a1

3. SELECT a1.firstName, a1.lastName

FROM ActedIn a1

5. SELECT a1.firstName, a1.lastName

FROM ActedIn a1  
EXCEPT  
SELECT a2.firstName, a2.lastName  
FROM ActedIn a2, Location l1  
WHERE a2.movieName = l1.movieName AND l1.country <> 'Canada'

WHERE (SELECT COUNT(*)  
FROM ActedIn a2  
WHERE a1.firstName = a2.firstName AND  
a1.lastName = a2.lastName) >= ANY (SELECT (SELECT COUNT(*)  
FROM ActedIn a3  
WHERE a2.firstName = a3.firstName  
AND a2.lastName = a3.lastName)  
FROM ActedIn a2)
 
WHERE EXISTS (SELECT firstName, lastName  
FROM ActedIn a2, Location l1  
WHERE a2.movieName = l1.movieName AND  
l1.country = 'Canada')
   

1. SELECT SUM(m1.budget)

FROM Movie m1

WHERE m1.name IN (SELECT m2.name  
FROM Movie m2, ActedIn a1  
WHERE m2.name = a1.movieName AND a1.firstName LIKE 'J%')
 
1. SELECT a1.firstName, a1.lastName

FROM ActedIn a1  
WHERE  
(SELECT COUNT(*)  
FROM ActedIn a2, Movie m1  
WHERE a1.firstName = a2.firstName AND a1.lastName = a2.lastName  
AND a2.movieName = m1.name AND m1.year = 2023  
INTERSECT  
SELECT COUNT(*)  
FROM ActedIn a2, Movie  
WHERE a1.firstName = a2.firstName AND a1.lastName = a2.lastName  
AND a2.movieName = m1.name AND m1.year = 2024) >= 2
 
1. SELECT firstName, lastName

FROM ActedIn  
WHERE NOT IN  
(SELECT a.firstName, a.lastName  
FROM ActedIn a, Movie m  
WHERE a.movieName = m.name AND m.earnings <= m.budget)
 
1. Yes, these two statements are equivalent.
 
1. No, these two statements are not equivalent. Let's say that we had four rows in our data where two movies from one studio make 1000 dollars each, and two movies from another studio make 500 dollars each. If we ran statement 1 on this instance, both movies from the first studio would be returned. However, since the second statement selects by average earning grouped by studio as opposed to average earning overall, nothing would be returned because the averages for the two studios would be 1000 and 500 respectively.
 
1. ActedIn

|   |   |   |   |
|---|---|---|---|
|firstName|lastName|movieName|...|
|Michael|Cera|Scott Pilgrim vs The World|...|
|Devon|Bostick|Diary of a Wimpy Kid|...|
|Ryan|Gosling|La La Land|...|

Location

|   |   |   |
|---|---|---|
|movieName|country|...|
|Scott Pilgrim vs The World|Canada|...|
|Diary of a Wimpy Kid|Canada|...|
|La La Land|USA|...|
   
   

I have not used an AI tool to help refine my work