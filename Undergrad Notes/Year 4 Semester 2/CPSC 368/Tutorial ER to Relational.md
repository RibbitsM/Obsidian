**Task 1:**
 
CREATE TABLE Customer(  
customerID INTEGER PRIMARY KEY,  
streetAddress CHAR(50),  
email CHAR(50) UNIQUE,  
firstName CHAR(15) NOT NULL,  
lastName CHAR(15) NOT NULL);
 
CREATE TABLE Reservation(  
confirmationNumber INTEGER PRIMARY KEY,  
customerID INTEGER NOT NULL,  
FOREIGN KEY (customerID)  
REFERENCES Customer(customerID)  
ON DELETE CASCADE);
 
CREATE TABLE Branch(  
branchName CHAR(15) PRIMARY KEY,  
streetAddress CHAR(50) NOT NULL,  
City CHAR(15) NOT NULL);
 
CREATE TABLE VehicleType(  
typeName CHAR(10) PRIMARY KEY,  
rentalRate INTEGER DEFAULT 0,  
numberOfSeats INTEGER);
 
CREATE TABLE Reserves(  
branchName CHAR(15),  
confirmationNumber INTEGER,  
typeName CHAR(10),  
startDate DATE NOT NULL,  
endDate DATE NOT NULL,  
PRIMARY KEY (branchName, confirmationNumber, typeName)  
FOREIGN KEY (branchName)  
REFERENCES Branch(branchName)  
ON DELETE SET DEFAULT 'Scranton PA'  
FOREIGN KEY (confirmationNumber)  
REFERENCES Reservation(confirmationNumber)  
ON DELETE CASCADE  
FOREIGN KEY (typeName)  
REFERENCES VehicleType(typeName)  
ON DELETE CASCADE)
 
**Task 2:**
 
INSERT INTO Customer VALUES (101, '10 Watford St', 'a@ubc.ca', 'Kate', 'Selvarajah'), (102, '9 Jenner St', NULL, 'Ming', 'Lee');
 
INSERT INTO Reserves VALUES ('Sheffield', 1, "SUV', '2017-01-01', '2017-01-02'), ('ManCity', 2, 'SUV', '2018-02-02', '2018-04-02'), ('ManCity', 2, 'Sedan, '2018-02-01', '2018-04-03');
 
INSERT INTO Reservation VALUES (1, 101), (2,102);
 
INSERT INTO VehicleType VALUES ('SUV', 40, NULL), ('Sedan', 30, 3), ('Truck', 50, 6);
 
INSERT INTO Branch VALUES ('Sheffield', '1212 Orlando St', 'New York'), ('ManCity', '3434 Raptors St', 'Shanghai'), ('Bournemouth', '5656 Trailblazers St', 'Seoul')
 
**Task 3:**
 
A) The customerID attribute does not have any protection against deletion, so the tuple will be deleted. However, customerID is also a foreign key in the Reservation table with the ON DELETE CASCADE constraint so the first tuple in Reservation will be deleted. This tuple also contains a confirmationNumber value of 1 which is also a foreign key with ON DELETE CASCADE, but in the Reserves table. This means that the first tuple in Reserve will also be deleted.
 
B) Nothing would happen, because this tuple has a NULL value for the firstName attribute, and this attribute has the NOT NULL constraint
 
C) This tuple would be deleted, and because branchName is used as a foreign key in the Reserves table with the constraint ON DELETE DEFAULT 'Scranton PA', the value of branchName in the first tuple of Reserves would be changed from 'Sheffield' to 'Scranton PA'
 
D) The tuple would be deleted, but no other tables would be affected because although confirmationNumber is a foreign key with ON DELETE CASCADE, since Reservation is not the origin of confirmationNumber no cascade would occur
 
E) The main issue is giving customerID in the Reservation table ON DELETE CASCADE. I don't know what the motivation for this is, but there should be no reason why reservations are being deleted as a result of cascades, this seems like an accident waiting to happen. As we saw earlier, this can lead to further cascade deletions and lead to unintended consequences. Other than that, all other restrictions in the database seem to be reasonable, setting the default branch on delete to Scranton seems silly, but it's entirely possible that this is just where the main warehouse is.
 
**Part 2**
 
1. X(K1, **K2**, A1), Y(K2, A2), K2 must be unique in X
2. X(K1, A1), Y(K2, **K1**, A2), K1 must be unique in Y
3. X(K1, A1), Y(K2, A2), R(**K1**, **K2**, A3)
4. X(K1, A1), Y(K2, A2), Z(K3, A3), R(**K1**, **K2**, **K3**, A4)
5. X(K1, A1), Y(K2, **K1**, A2) K1 cannot be null
6. X(K1, A1), Y(**K1**, A2, A3)
7. X(K1, A1), R(**K1**, R1, R2) R1 and R2 must be unique in R, X(K1, A1), R(**K1**, R1, R2) , R2 must be unique in the second R relationship
8. X(K1, A1), R(**K1**, R1, R2)
9. X(K1, A1), Y(**K1**, A2, A3), Z(**K1**, A4, A5)
10. Y(K1, A1, A2, A3), Z(K1, A1, A4, A5)
 
I did not work with others or use an AI tool while completing this assignment