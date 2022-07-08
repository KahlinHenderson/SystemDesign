Functional Requirements

Real-time messaging from user to user

Group messaging

Online status

Media Uploads

Non-Functional Requirements

Low latency

High volume

Reliable

Secure

User A sends a message to User B over a chat server. We consider two models by which the recipient may connect to the chat server.

Long-polling: the recipient sends a request to the chat server. The chat server holds the request for a period of time. If the time period expires, the recipient sends a new request. Otherwise, when the requested data reaches the server it is forwarded to the recipient. The recipient sends a new request to the server. The problem with this connection is that the recipient must send a new request in order to receive a new message.

Web Socket: the recipient has a long-lived, bidirectional connection to the chat server. This allows the server to push messages to the recipient without the recipient having to request them.

Scaling Out

User A sends a message to User B.

The request goes to a load balancer

The load balancer forwards the request to a chat server

The chat server sends the message to a messaging service

The messaging service stores the message in a queue or multiple queues if there are multiple recipients

The chat server the recipient is connected to takes the message from the queue and sends it to a load balancer

` `The load balancer sends the message to the recipient

Storing and Persisting Messages

Users Table

User ID

Name

Last active

Messages Table

Message ID

User

Conversation

Text

Media\_URL

Conversations Table

Conversation ID

Conversation\_Users Table

Conversation ID

User ID

Storing Media

Chat servers send media files to an object storage service. When the recipient gets the Media\_URL it sends a request to CDN. If the CDN stores the object, it is returned to the recipient. Otherwise, the CDN requests the object from the object storage service.

Notification Service: Notifies offline users of messages they missed. If the recipient is offline, the messaging service contacts the notification service and the notification service contacts the recipient.
