Requirements

Functional Requirements:

Given a URL, the service should generate a shorter and unique alias of it. Also called a short link, the alias is a reference to the original URL.

When a user clicks on the short link, they should be redirected to the original URL.

Users should be able to pick a custom short link for their URL.

The link will expire after a a certain time. Users should be able to pick an expiration time.


Non-Functional Requirements:

Highly Available

Minimal latency when fetching the original URL

Short links should not be guessable

APIs

createURL(api\_dev\_key, original\_url, custom\_alias=None, user\_name=None, expire\_date=None)

Parameters:

api\_dev\_key(string): API developer key of a registered account. Used to throttle users.

original\_url(string): Original URL to be shortened

custom\_alias(string): Optional custom alias for the original URL

user\_name(string): Optional user name

expire\_date(string): Optional expire date

returns a shortened URL(string) or an error

deleteURL(api\_dev\_key, url\_key)

url\_key is a string representing the short URL to be deleted

Database Design

URL Table:

Key

Original URL

Creation Date

Expiration Date

User ID

User Table:

User ID

Name

Email

Creation Date

Last Login

Key Generation Service

We have a standalone service that randomly generates unique 6 letter strings beforehand and stores them in a key database. Whenever a user submits a URL, a string will be retrieved from the key database and used as part of the short link. The service will maintain a table of used keys and a table of unused keys to resolve concurrency issues. When a client submits a URL to the TinyURL service it sends a request to the Key Generation Service. The Key Generation Service retrieves a key from the key database and sends it to TinyURL. The TinyURL service generates the short link and stores the key in a database, along with the original URL, creation date, expiration date and user ID.

Data Replication

We can use consistent hashing to map each key and the associated data to a server. The server will create k copies of the data and forward them to the next server. If the next server is online it will store one copy and forward k-1 copies to the next server, etc.

Cache

We use a cache server to store the most frequently accessed URLs. When the user clicks a short link, a request goes to the application server. The application server requests the the URL from the cache server. If it’s there, the URL is sent to the application server and then returned to the client. If it’s not there, the application server requests the URL from the database. If it’s there, the application server requests to have the URL stored in cache and then returns it to the client. If the URL is not in the database, the application server returns an error to the client.

Load Balancer

We can position load balancers between clients and application servers, between application servers and cache servers and between application servers and database servers.



