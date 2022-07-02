WhatsApp is a service that allows users to send messages to each other. Here we consider two use cases of the service.

Case 1: Sending a text message to an online user

Message from user A to user B is forwarded to the chat server to which user A is connected

Chat server responds to user A with an acknowledgment that the message was sent

Chat server makes a request to data storage to fetch information about the chat  server to which user B is connected

Data storage returns info about the chat server user B is connected to

Chat server A forwards the message to chat server B

Message is pushed to user B’s device

Case 2: Sending image to an offline user

Image from user A to user B is forwarded to the chat server user A is connected to

The chat server sends the image to a file server where it is stored

The file server returns the image URL to the chat server

The image URL is returned to user A’s device

The chat server fetches info from the data store about the server user B is connected to, which shows user B is offline

The chat server forwards the message containing the image URL to a transient server

The transient server stores the message in transient storage(a message queue)

User B comes online and his chat server notifies the transient server to fetch messages in  in queue

The transient server forwards messages to User B’s chat server

User B’s chat server forwards messages to his device

User B’s device fetches the image from the file server
