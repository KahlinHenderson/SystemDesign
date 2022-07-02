Facebook’s News Feed is a system that displays content posted by a user’s friends or other entities they follow(e.g. businesses, news sources). The system uses a ranking algorithm to determine what content to show.

Database Entities

User(name, email and creation date attributes)

Post(user ID, content, creation date and likes attributes)

Three models for generation a News Feed

Pull model:

User creates a post

Post is stored in server’s memory

When user’s friends request a news feed the post is retrieved from memory and added to the feed

Push model:

User creates a post

Post is stored in a database

Post is forwarded to user’s friends’ news feeds

Hybrid model:

If the user has a small number of friends, push model is used. If the user has a large number of friends, pull model is used.

Ranking Algorithm

Determines the likelihood that a post will be added to a user’s feed

Any two users have an affinity score, a measure of how closely related they are. Affinity score is affected by how often they like each other’s posts, comment on each other’s posts, click each other’s links, etc. The higher the affinity score the more likely their posts are to be added to each other’s news feeds.

Each post has a weight, with videos and images having a higher weight than text-based posts. Also affected by number of likes/comments.

Time decay is a measure of how old a post is


