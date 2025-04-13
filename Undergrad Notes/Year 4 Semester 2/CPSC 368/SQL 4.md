1. SELECT sum(attendanceNumber)

FROM Show  
GROUP BY day
 
1. SELECT count(*)

FROM Musician  
GROUP BY instrument  
HAVING nationality = 'Canada'
 
1. SELECT sp.title

FROM SongsPerformed sp,

WHERE (SELECT avg(pe.age)  
FROM Person pe) < (SELECT avg(pe.age)  
FROM Person pe, Purchase p  
WHERE sp.showID = p.showID AND  
pe.email = p.email)