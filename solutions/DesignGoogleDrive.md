Google Drive is a system that allows users to store their files on a remote server and share them with other users.

The client is the Google Drive app installed on your computer of phone. When a file is uploaded to the could storage, the chunker is responsible for splitting the file into smaller pieces of equal size, e.g. splitting a 10 Mb file into 5 chunks of 2 Mb each. When the client updates a file, the chunker is responsible for detecting the chunks that are updated so that only those chunks are uploaded to the cloud storage.

When the client creates, updates or deletes a file the watcher notifies the indexer of the event. When the client creates a file the indexer stores information about each chunk in the client’s metadata database. Most importantly,

chunk\_id

chunk\_order

file name

file version

When the client updates a file, for each chunk that’s modified, the indexer only updates the file version.

The client sends a message to the message queueing service, which stores the message in a global message queue. The request if forwarded to the synchronization service, which updates the global metadata database about the latest version of the file. The synchronization service sends a broadcast message to the other clients, notifying them to update their local metadata databases about the latest version of the file. Each copy of the message is stored in a different response queue, one for each client. For each client, the indexer picks up the latest chunks from cloud storage.

To upload or download files the client communicates with a block service.

Amazon S3 is the file storage service.
