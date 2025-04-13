1. This query does not accomplish the stated task. The reason is because since the database is set to reference the movies collection, when it runs $lookup to try and retrieve the actor details they will find nothing and then get an empty array for actorDetails which will make the whole query return nothing when you try to unwind it. This is a shame because they actually had somewhat of a correct query before this. If you remove all code from line 11 onwards, you will get a query that returns the actor who has acted in the most movies, which in the setup case was Anne Hathaway. However, this only returns a single actor, to get all actors tied for the most movies you would have to take the maximum value of movieCount with $max and use $match to filter for actors with movieCount equal to the maximum value
2. First, the $unwind operator is used to extract the individual actor information as rows, they are usually held in arrays containing all actors for each movie. Unwinding this will give us a row for each actor. Next, $group is used to group by actor ID and make a new column called movieCount which contains the number of rows in each group, which would be the number of movies that actor has appeared in. $sort is then used to sort the results by movieCount in descending order to get the most prolific actors at the top, and $limit is used to return only a single actor with the highest (or tied for highest) movieCount value. Next, $lookup is used to attempt to get the information on the actor with the highest movieCount from the actors table, which is intended to be stored as an array with the name actorDetails. Then, unwind is used again to extract those details, and finally $project is used to ensure the final product displays first and last name in separate columns and the id column is removed.
 
1. db.find({'year':2023}, {'_id':0, 'name':1}) 3. db.aggregate([{'$unwind': '$actors'},

{'$match' : {'year':2023}},  
{'$project' : {"_id": 0, "actors": 1}}])
 6. db.aggregate([{'$group': {'_id':'$studio','NumFilms':{'$sum': 1 }}},

{'$sort':{'NumFilms':-1}}])
    
1. Not possible, I used this code: 
db.aggregate([{'$match':{'locations':{'$all':[{'$elemMatch':{'country': 'Canada'}}]}}}])
 
This code is supposed to return only rows where all elements of the nested array meet the condition, but $all appears to be not functioning properly as it is returning all rows were at least one element meets the condition
    
1. db.aggregate([{'$match':{'name':{'$regex':'^I'}}},

{'$group': {'_id': None,'Total_Budget':{'$sum': '$budget' }}}])
 4. db.find({'$expr':{'$gt':["$earnings", "$budget"]}})
   

1. db.aggregate([{'$addFields': {'actorIds': {'$map': {'input': "$actors",'as': "a",

'in': "$$a.$id"}}, 'noRyan': {'$setDifference': [["RyanGosling"],

{'$map': {'input': "$actors", 'as': "a", 'in': "$$a.$id"}}]}}}, {'$match': {'$expr': {'$gt': [{'$size': {'$ifNull': ["$noRyan", []]}}, 0 ]}}},{'$group': {'_id': None, 'noRyan': { '$push': "$name" }}}])
 3. This query finds all movies that have listed actors that do not have Ryan Gosling in them and returns the names of those movies
   

1. Assuming there is an id value linking movies and actors

SELECT name FROM Movies  
WHERE actorFirstName <> 'Ryan' AND actorLastName <> 'Gosling'
 
1. For questions 1 and 2, we need an actor who is tied for most number of movies acted in

For question 3, nothing is needed  
For question 4, we need to have actors who have acted in more than one movie in 2023  
For question 5, nothing is needed  
For question 6, nothing is needed  
For question 7, we need a movie that has I in the title but not in the first word of the title  
For question 8, nothing is needed
 
In total, we only need 2 new movies: one of them needs to have an actor who was in a movie in the dataset released in 2023, one of them needs to have an "I" in the title but not in the first word, and both movies should have the same actor which would bring their number of movies from 1 to 3, tying them for most movies.
 
Stephanie Hsu was in a movie called Joy Ride the same year as Everything Everywhere All at Once and she also has a movie called Asking For It which has a capital I not in the first word of the title, so we will add both of these movies to fulfill our testing requirements
 
Movies

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
|Name|Year|Studio|Budget (millions)|Earnings (millions)|Actors|Locations|
|Joy Ride|2023|Point Grey Pictures|32|15|Stephanie Hsu|Vancouver, Canada  <br>Kelowna, Canada|
|Asking For It|2020|Street 12 Productions|1|0.5|Stephanie Hsu|New York City, USA|
   
       
I used ChatGPT to complete this assignment, specifically I used it to write the code for question 9. I did not use it for any other parts of the assignment