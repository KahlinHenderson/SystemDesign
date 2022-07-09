Functional Requirements

Users can post tweets, or messages with a max of 140 characters

Generates timelines

The home timeline is a page showing the latest tweets from people a user follows

The user timeline is a page showing the user’s tweets

The search timeline is a page showing tweets containing a given keyword.

Non-Functional Requirements

Read heavy

Eventual Consistency

Scalable

Database Schema

Tweet Table

Tweet ID

Content

Creation Date

Num Favorites

User Table

User Table

User ID

Name

Email

Follower Table

User ID1

User ID2

When a user posts a tweet the request goes to a load balancer. The load balancer forwards the request to an app server and the app server stores the tweet data in a database.

User Timeline

We store the following data in a cache:

User_ID-User_Tweets: [1, 2, … , n ] where 1, 2, … , n are Tweet IDs

Tweet_ID-Tweet: “content associated with the given Tweet ID”

Home Timeline

When a user posts a tweet, the data(content, Tweet ID, etc.) is stored in a database. Also, a new key-value pair is stored in the cache. When a follower requests their home timeline the request is directed to the cache. The cache generates the home timeline and returns it to the follower.

When a celebrity posts a tweet, the data(content, Tweet ID, etc.) is stored in a database. Also, a new key-value pair is stored in the cache. When a follower requests their home timeline the request is directed to the cache. The response time is higher since the page has to be returned to millions of followers. To minimize response time, the cache precomputes the home timeline but only populates it with non-celebrity tweets. When the cache receives the request, it adds any celebrity tweets to the follower’s timeline.







