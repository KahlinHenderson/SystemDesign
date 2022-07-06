Requirements

Users should be able to upload photos

Users should be able to view the photos they’ve uploaded

Users should be able to follow others users

Users can view feeds containing posts from the other users they follow

Users should be able to like and comment on posts

Database Design

Relational database for storing photo metadata

Users Table

User ID (primary key)

Name

Email

Location

Photos Table

Photo ID (primary key)

User ID (foreign key)

Caption

Location

Path

Followers Table

User 1 (foreign key comprised of User IDs)

User 2 (foreign key comprised of User IDs)

High Level Design

Metadata Database: stores the above information

Object Store: stores the image itself

App Servers: one set for handling reads and another set for handling writes

Cache: positioned between read servers and the database. When write server stores info in the database it is also stored in cache.

Load Balancers: positioned between clients and app servers

Use Cases

Reading: the client request goes to a load balancer, which forwards the request to an instance of the read service. The read service checks the cache for the image meta data. If the meta data is in cache, it will be returned to the read service and subsequently returned to the client(including the image path). Next, the client sends a separate request to the object store.

Writing: the client request goes to a load balancer, which forwards the request to an instance of the write service. The image meta data is stored in the database and cache and the image is uploaded to the object store.

Feed Generation Service

Communicates with the database to determine which content is new and uses this information to generates feeds and stores them in the cache. This allows the read service to fetch feeds from the cache upon request.







