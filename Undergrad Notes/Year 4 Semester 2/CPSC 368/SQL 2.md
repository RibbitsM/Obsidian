1. SELECT showID FROM SongsPerformed

WHERE composer = 'Mozart'  
INTERSECT  
SELECT showID FROM SongsPerformed  
WHERE composer = 'Beethoven'
 4. SELECT distinct P1.showID

FROM SongsPerformed P1, SongsPerformed P2  
WHERE P1.showID = P2.showID AND P1.composer = 'Mozart'  
AND P2.composer = 'Beethoven'
 7. SELECT showID FROM SongsPerformed P
   

WHERE EXISTS (SELECT P1.showID FROM SongsPerformed P1  
WHERE P1.composer = 'Mozart') AND  
EXISTS (SELECT P2.showID FROM SongsPerformed P2  
WHERE P2.composer = 'Beethoven') AND  
P1.showID = P2.showID = P.showID
 
1. SELECT P.showID FROM SongsPerformed P

WHERE composer = 'Mozart' AND  
P.showID IN  
(SELECT P1.showID FROM SongsPerformed P2  
WHERE P1.composer = 'Beethoven')