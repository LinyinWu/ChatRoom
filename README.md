This is a chat application with a message center server, and the key criteria of the new design is that no permanent connection is maintained between the server and client. The states of each party will need to be maintained locally, and synchronized using the network connection when needed.

1. Message Center
The message center, also known as the server, has the following responsibilities:

a. User Authentication: 
Each user logs into the message centre with a username and a password. On entering invalid credentials, the user is prompted to retry. After 3 consecutive failed attempts, the user is blocked for a duration of 60 seconds (this should be configurable), and cannot login during this duration (even from another IP). While a user is online, if someone uses the same username/password to log in from another IP, current user will be notified and automatically logged out.

b. User Message Forwarding: 
Forward each chat message to the correct recipient.

c. Timeout:
The message centre should have a configurable timeout value. If it does not receive a ‘LIVE’ signal from a user within the timeout, it considers the user to be disconnected.

d. Blacklisting:
Allow a user A to block / unblock any other user B. If user A has blocked user B, B can no longer send chat messages to A i.e. the message centre should intercept such messages and inform B that the message cannot be forwarded. Blocked users also do not get presence notifications i.e. B will not be informed each time A logs in or logs out.

e. Presence Broadcasts:
Notify the presence of other users logged into the chat room i.e. send a broadcast notification to all online users when a user logs in /logs out.

f. Offline Messaging:
When the recipient of a message is not logged in, the message will be saved by the message centre. When the recipient logs in next, the message centre will display all the unread messages stored.



2. Chat Client
The chat client has the following responsibilities:

a. Authentication:
Provide a login prompt to enable the user to authenticate with the message center.

b. Chat:
i. Allow the user to send a message to any other user.
ii. Display messages sent by other users.

c. Notifications Display:
presence notifications sent by the message center.

d. Find users online:
Obtain a list of all the users currently online.

e. Heartbeat:
Every 30 seconds (this duration should be configurable), the client should send a ‘LIVE’ signal to the message centre to indicate that the user is still logged in.

f. User Interface:
A simple graphical user interface can be implemented for extra credit.


Peer-to-peer chat
The aim of this feature is to implement a chat service in which the message centre has minimal intervention once a conversation has been established. It can be developed on top of the basic chat room architecture. The basic requirements of this feature are:

g. Any user A wanting to private chat with user B will first request the message centre for user B’s IP address.
i. If B is online, the message centre will provide B’s IP address and PORT, else it notifies A that B is offline.
ii. If B is offline, the chat client should report that the request failed.

h. On obtaining B’s IP address, user A can establish a connection directly with user B using said address.

i. From this point onwards, A can send private messages directly to B using the “private” command. Such private messages would be sent directly to the IP address without going through the server.


Advanced
P2P Privacy and Consent
1.1 When A requests for B’s IP address, the message centre should notify B that A wants to talk it. If B agrees to the conversation, the server should provide A with B’s IP address. Else, A cannot initiate a conversation with B.
1.2 When A requests for B’s IP address, the message centre should check B’s blacklist preferences. If B’s blacklist includes A, the message centre should not provide B’s IP address to A.

Sample Run

login
![Alt text](https://raw.githubusercontent.com/LinyinWu/ChatRoom/master/test%20pictures/login.png)

block
![alt tag](https://raw.githubusercontent.com/LinyinWu/ChatRoom/master/test%20pictures/block.png)

display current users
![alt tag](https://raw.githubusercontent.com/LinyinWu/ChatRoom/master/test%20pictures/display%20current%20users.png)

broadcast
![alt tag](https://raw.githubusercontent.com/LinyinWu/ChatRoom/master/test%20pictures/broadcast.png)
display offline message when login
![alt tag](https://raw.githubusercontent.com/LinyinWu/ChatRoom/master/test%20pictures/offlineMsg.png)
![alt tag](https://raw.githubusercontent.com/LinyinWu/ChatRoom/master/test%20pictures/offlineMsg2.png)

basi P2P

![alt tag](https://raw.githubusercontent.com/LinyinWu/ChatRoom/master/test%20pictures/basicP2P.png)
