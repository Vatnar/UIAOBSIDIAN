```table-of-contents
```
# Overview
- Principles of network applications
- Web and HTTP
- E-mail, SMTP, IMAP
- The Domain Name System DNS
- P2P Applications
- Video streaming and content distribution networks
- Socket programming with UDP and TCP
## Our goals:
- Conceptual and implementation aspects of application-layer protocols
	- client-server paradigm
	- peer-to-peer paradigm
	- transport-layer service models
- Learn about protocols by examining popular application-layer protocols and infrastructure
	- HTTP
	- SMTP, IMAP
	- DNS
	- video streaming systems, CDNs
- Programming network applications
	- Socket API
## Some network apps
- Social networking
- Web
- text messaging
- e-mail
- multi-user network games
- streaming stored video (YouTube, Hulu, Netflix)
- P2P file sharing
- VOIP, Voice over IP Skype discord
- real-time video converefncing eg zoom
- Internet search
- Remote login

# Creating a network app
write programs that:
- run on (different) end systems
- communicate over network
- e.g., web server software communicates with browser software
no need to write software for network-core devices
- network-core devices do not run user applications
- applications on end systems allows for rapid app development, propagation
# Client-Server architecture
server:
- always-on host
- permament IP address
- often in data centers, for scaling
clients:
- contact, communicate with server
- may be intermittently connected
- may have dynamic IP addresses
- do **not** communicate directly with each other
- examples: HTTP, IMAP, FTP
# Peer-peer architecture
- no always-on server
- arbitrary end systems directly communicate
- peer request service from other peers, provide service in return to other peers
	- self scalability -- new peers bring new service capacity, as well as new service demands
- peers are intermittently connected and change IP addresses
	- complex management
- example: P2P file sharing
# Processes communicating
**process**: program running within a host
- within same host, two processes communicate using inter-process communication IPC or concurrency (defined by OS)
- processes in different hosts communicate by exchanging messages.
- Client process initiates communication. Server process waits to be contacted
- note: applications with P2P architectures have client processes & server processes.

# Sockets
- Process sends/receives messages to/from its **socket**
	- two sockets involved: one on each side
- socket analogous to door
	- sending process shoves message out door
	- sending process relies on transport infrastructure on other side of door to deliver message to socket at receiving process. 
 ![[socket as a door.jpg]]
# Addressing processes
- to receive messages, a process must have a **identifier**