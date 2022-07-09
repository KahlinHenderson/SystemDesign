Requirements

Video upload

View uploaded videos

Search for videos

Track stats of videos

Comment on videos

Capacity Estimates

500 hours of video uploaded per minute

1 billion hours of video watched per day

Storage

500 x 60 = 30,000 minutes of video uploaded per minute

30,000 x 50 MB // 1,000 = 1,500 GB uploaded per minute

1,500 GB x 60 x 24 // 1,000 = 2,160 TB uploaded per day

2.16 PB per day

Bandwidth

1 billion hours of video watched daily on YouTube

1,000,000,000 x 3 GB per hour // 1,000 = 3,000,000 TB

3,000 PB bandwidth/day

Database Design

Video Table

Video ID

Title

Description

Thumbnail

User ID

Likes

Dislikes

Views

User Table

User ID

Username

Email

Bio

Comments Table

Comment ID

Video ID

User ID

Comment

Time

High Level Overview

Content Distribution Network: stores frequently requested uploads at a location that’s physically closer to the client than the data center is.

Load Balancer: distributes requests equally across a set of app servers.

App Servers: execute business logic. If the client uploads a video, an app server sends the file and its metadata to a processing queue. If the client sends a search request, the app server queries the database for video metadata (titles, descriptions, etc.) and user data that best matches the keywords and returns the top results to the client.

Processing Queue: when a client uploads a file, the app server sends it here. The file is assigned a task id so that if the upload fails at a later stage in the process, the client doesn’t have to send another request.

Video Upload Server: encodes the video into various formats that are suitable for different connection speeds.

Video Object Storage: stores the file and its metadata in a bucket.






