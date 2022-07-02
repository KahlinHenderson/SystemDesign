An API layer connects the user to one of several microservices.

User Manager: creates and updates user profiles and stores the profile data in a database

Listing Manager: generates a list of products for the user. Product data is fetched from a database.

Cart Manager: adds, removes and updates items in the user’s cart

Payment Manager: processes payments

Order Manager: creates orders and stores the order data in a database

When the user places an order the Cart Manager communicates with the Order Manager, and then the Payment Manager.





