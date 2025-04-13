Ssh: ssh rmurph02@remote.students.cs.ubc.ca  
Oracle login: sqlplus ora_rmurph02@stu
 
DUE FEB 28
 
1. select pub_name from publishers; 
alter table publishers  
rename column pub_name to Publisher_Name;
 5. select ed_fname from editors

where ed_fname like 'j%' or ed_fname like 'W%';
    
1. select title_id from titles

where type = 'psychology' and title like '%Data%';
 
1. select * from titleauthors;
 
1. select title from titles

where pub_id = 0736;
 4. select qty_ordered as Order_Amount, qty_shipped as Shipped_Amount

from salesdetails  
where title_id = 'MC3021';
   

1. select au_id,count(au_id) from titleauthors

group by au_id;
 
1. select count(*) from titleditors where title_id = 'BU2075';
 
1. select e.ed_lname from editors e

where e.ed_id IN (select t.ed_id from titleditors t  
group by t.ed_id having count(t.ed_id) > 5);
 
1. describe titles
 
I used chatgpt to complete this assignment, and this is the only prompt I used:
 
Given an sql file with two schema, one called titleditors containing the editor ids and book titles of all books in a bookstore, and the other called editors containing the same editor ids and the first and last names of the corresponding editors, write me an SQL oracle query that would return the last names of all editors that have edited more than 5 books.
 
I did not work with others on this submission