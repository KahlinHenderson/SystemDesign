Requirements

Allows the user to upload files to a remote server and download files on a device

Has a sync folder containing every file the user uploads/downloads through the service

Keeps a history up file updates

Scale

10 million users

100 million requests/day

High number of reads and writes

Components

Client: the Dropbox application running on a mobile device or desktop

The client is composed of the following parts.

1.Chunker: when a file is added to the sync folder the chunker splits it into pieces of equal size and uploads it to the cloud.

2.Watcher: monitors the sync folder for any changes. When a file is added to, deleted from or modified in the sync folder the watcher notifies the indexer of the event.

3.Indexer: receives notifications from the watcher about changes to the sync folder and updates the metadata database accordingly.

4.Metadata Database: stores information about each chunk of each file in the sync folder.

Global Metadata Database: stores information about file chunks and versions, users and their sync folders.

Synchronization Service: updates the global database about changes to sync folders. When there’s a change in a sync folder the synchronization service updates the global database and broadcasts a message to the other clients to update their local databases.

Messaging Service: receives messages about updates to the client’s sync folder. Whenever a file is added to, deleted from or modified in the sync folder the client sends a message to the messaging service, where it is stored in a request queue. The message is  then forwarded to the synchronization service. The broadcast message from the synchronization service is stored in response queues.

Object Storage Service: stores the files and their metadata in buckets. With Amazon S3 multiple versions of an object can be stored in the same bucket.








