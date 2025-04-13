- Databases can be seen at three different levels of abstraction
- The first level is the physical level, the binary data and machinery that make up the database
- The conceptual level is the semantic organization of the database
- Finally, the view level is what people see on their screens when they use the database
- The schema of a database is the logical structure, for example a grades database consists of students that possess overall grades based on grades for assignments they have submitted
- The instances are the actual examples of data in our database
- We need to know what the entities in our database are and the relationships between those entities
- Entities are usually nouns, and their relationships are described using verbs
- An entity generally has attributes, so going back to the grades example each student is an entity
- The attributes of an entity are the kinds of data we will collect on all those entities, and are restricted to a "domain" which is the data type (string, float, bool, etc.)
- You can't directly represent a student in data, you have to abstract it
- Some examples of attributes could be a student's name, student id, birth date, or major
- An entity set is a collection of similar entities, where all entities have the same attributes
- In order to distinguish entities from each other we need keys, which are the minimal set of attributes requires to uniquely identify an entity in its set
- If two entities have identical attributes, there's no way to figure out which entity is which
- A primary key is an attribute that is the primary means for identifying an entity, this is usually a unique id number attribute given to every entity
- When you have multiple minimal keys you just choose one as the primary key, and keep the rest as candidate keys
- Remember that primary keys have to be MINIMAL
- In your diagram, the key attributes are underlined
- On an ER diagram, an entity set is shown as a box, while attributes are shown as bubbles
- Diamonds represent relationship sets, which can also have their own attributes
- A relationship set holds the relationships between all entity sets it is attached to on that diagram
- There can also be relationships between entities in a single set
- For example, in our database of movies and people working in movies, we can have a relationship showing which people were involved in what movies, but also a relationship showing which people are the parents of other people
- The degree of a relationship is the number of entity sets connected to a relationship, so our relationship of who worked on what movie would be binary
- This is because there are two related entity sets, the people entity set and the movies entity set
- Relationships can have attributes just like entity sets can

**Constraints**

- Often, since our ER diagram is usually representing real things, restrictions will come into play
- For example, courses cannot have unlimited numbers of students in them and students cannot take an unlimited number of classes
- There are a couple different kinds of relationships we can have
- First there is many to many, where an entity in either set can be related to as many entities from the other set as they want
- The opposite would be one to one, where each entity in a set can only correspond to one entity in the other set
- This can be one sided too, like a one to many or many to one relationship
- We read these relationships left to right on our diagrams, so if an entity on the left side of the diagram can be related to several entities in a set on the right side but not the other way around, that's a one to many relationship
- Restrictions like these are called "key constraints" or "cardinality constraints" and are represented by arrows in our ER diagram
- For some reason, this works in reverse to how we describe relationships verbally because the arrow always points from the many to the one
- Another way to describe it is that the arrow points to the thing that there is only one of
- A good way to think about this is that if we know the object on the many side, we should be able to confidently determine it's corresponding object on the one side
- In a one to one relationship, the arrows point to each other
- This is helpful for narrowing down searches, because if we know the other half of a something to one relationship, we can guarantee what the other half is because there is only one possibility
- Another kind of constraint is a participation constraint, which shows what other elements are required for a relationship
- For example, for our movie database every movie must have a director, and every director must have worked on at least one movie
- In an ER diagram this is depicted with a solid line, which indicates that every member of that entity set has that relationship
- In our teaching dataset, all courses must have a professor, but not all professors teach a course
- This means that there is a participation constraint between cs courses and the teaching relationship, all entities in the courses entity set participate in that relationship
- Of course, this can stack with other constraints like key constraints

**ISA Relationships**

- ISA relationships can split entity sets into subsets, where specific objects within an entity set have different attributes that other objects lack
- In our movie examples, some people working on movies are actors, and the others are musicians or directors
- There are constraints on ISA relationships that we can't exactly draw
- An overlap constraint can either allow objects to have multiple subclasses (overlapping) or restrict them to one (disjoint)
- A covering constraint can be either total, meaning all entities in the set must belong to a subset, or partial meaning that some do not belong to the subset
- Using musicians and actors as an example, in reality we would have a partial + overlap constraint since some actors can be musicians and vice versa and not all people who work on movies are either actors or musicians
- These subsets are not distinct entity sets but subsets of the larger set
- This means that they don't need their own keys
- In an ER diagram, ISA relationships are drawn as triangles, just like other relationships
- When trying to identify which set is the parent, just look for which set has a primary key

**Weak Entity**

- A weak entity is identified by a thick line around an entity set
- This is an entity that can only be identified using the key of another entity
- The key of a weak entity is its key plus the key of its parent
- This is called a "partial key" and shows up as a dotted underline under the relevant attribute of the weak entity
- One to many relationship, a weak entity must have a parent and a parent can have any number of weak entities attached to it

**Aggregation**

- Relationships cannot be connected to other relationships
- This may become a problem if we have a relationship between entities and their relationships and another entity set
- To get around this, we need to aggregate, which we do by drawing a dotted box around whatever we want to aggregate
- In our movie example, SPCA monitors supervise animals in movies, but different monitors may be assigned to the same animal in different movies
- To represent this we need the IDs of the animal and the movie, which are linked by a relationship
- Instead of drawing a line between the relationship between the animal and the movie and the SPCA representative, draw a box around the animal set, movie set, and their relationship
- Then, you can link that aggregated box to a relationship describing how long that monitor is assigned to that animal-movie pair
- We can't model everything, for example candidate keys
- However, ER diagrams can generally model pretty much anything we want to depict
- This is entirely conceptual, there will be deign choices you have to make when creating them
- ER diagrams also can't capture domain constraints like type requirements, value requirements, etc.
- Some attributes may have to be entities, and we may not know this at the time
- For example, an address attribute may have to be an entity set if people have multiple addresses
- In our movie example, our relationship showing roles in a movie only allows for a single role
- But, if we made role an entity set than individuals could have multiple roles
- In a ternary relationship, if you know the entity with the arrow, you know all other entities in that relationship
- If you need additional constraints, instead of doing a ternary relationship just aggregate two sets and make a connection between the aggregation and the third entity
-