> [!caution] This page contained a drawing which was not converted.   

branchName
   

Branch

VehicleType

typeName

customerID

Customer

ReservedVehicle

Name

Address

Email

Rate

Seats #

Start

End

City

Address

**Question 1**

**Question 2**

branchName
   

Branch

City

customerID

Customer

Name

Address

Email

Confirmation#

Reservation

VehicleType

typeName

Rate

Seats #

PlacesReservation

VehicleReserved

StoredAt

RentsFrom

StartTime

EndTime

**Question 3**
 
Task 1 certainly looks visually much cleaner than task 2, and I think it represents the integrated nature of the relationships between all three entity sets. However, I think this comes at the cost of some nuance, especially having a separate entity set for the reservations. Technically, all relevant information in the first diagram is represented by adding attributes to the reservation relationship, but logically speaking it makes more sense to have reservations in an entity set since even when a reservation expires, the dealership would store it and want to look at that information in the future

**Question 4**

branchName
   

Branch

VehicleType

typeName

customerID

Customer

ReservedVehicle

Name

Address

Email

Rate

Seats #

Start

End

City

Address

IsA

Car

Truck

(Total Disjoint)

**Question 5**

branchName
   

Branch

VehicleType

typeName

customerID

Customer

ReservedVehicle

Name

Address

Email

Rate

Seats #

Start

End

City

Address

IsA

Car

Truck

(Total Disjoint)

IsA

ClubMembers

Points

Coverage

AddEquip

IsA

ForSale

Price