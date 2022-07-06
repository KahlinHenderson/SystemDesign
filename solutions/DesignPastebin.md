Pastebin is a service that allows users to store plain text. Users of the service will enter a piece of text and get a randomly generated URL to access it.

Functional Requirements

Users should be able to upload or “paste” their data and get a unique URL to access it

Users will only be able to upload text

Data and links will expire after a certain timespan automatically, and users should be able to specify expiration time

Users should be able to pick a custom alias for their paste

Non Functional Requirements

Highly Reliable, i.e. data should not be lost

Minimal latency when users access their paste

Paste links should not be guessable

Extended Requirements

Analytics, e.g. how many times is the average paste accessed?

Our service should be accessible to other services through REST APIs

Other Design Considerations

We limit paste size to 10 Mb

We impose a size limit on custom URLs in order to have a consistent URL database

APIs

addPaste(api\_dev\_key, paste\_data, customer\_url=None, user\_name=None, paste\_name=None, expire\_date=None)

api\_dev\_key(string): The API developer key of a registered account. This is used to throttle users.

paste\_data(string): text uploaded by the user

customer\_url(string): optional customer URL

user\_name(string):

paste\_name(string):

expire\_date(string):

returns a string, the URL through which the user can access their paste

getPaste(api\_dev\_key, api\_paste\_key)

api\_paste\_key identifies the paste the user wants to retrieve

deletePaste(api\_dev\_key, api\_paste\_key)

returns True if the paste is successfully deleted. Otherwise, returns False.

Database Schema

Paste Table

User ID (primary key)

Short URL

Paste Path

Expiration Date

Last Accessed

User Table

User ID (primary key)

Name

Password

Email

High Level Design

Application Server: runs a copy of the Pastebin service

Metadata Database: stores the Paste and User tables

Object Store: stores the data in an object

Key Generation Service: a standalone service that generates random six-letter strings beforehand (short URLs) and stores them in a key database. When the user uploads their content Pasatebin requests a short URL from the KGS. It stores the short URL in a database and then returns it to the user. When a user requests the content from Pastebin the service will attempt to fetch the short URL from the database. If the short URL is in the database, Pastebin will use the paste path to fetch the content from the object store. If the short URL is not in the database Pastebin returns an error.

Data Replication

We use consistent hashing to map a short URL and its associated data to a server. The server creates k copies of the data and forwards them to the next server in the network.

Caching

The most frequently accessed URLs and their associated content will be cached. When a user requests some content, Pastebin will check to see if the short URL is stored in a cache. If the short URL is stored in a cache, the content is sent to the application server and then returned to the user. If the short URL is not stored in a cache, the application server attempts to fetch it from the database. If the short URL is in the database, Pastebin uses the paste path to fetch the content from the object store and has it stored in  a cache along with the corresponding short URL. If the short URL is not in the database, Pastebin returns an error.

Load Balancing

We position load balancers between clients and application servers and between application servers and object stores.



