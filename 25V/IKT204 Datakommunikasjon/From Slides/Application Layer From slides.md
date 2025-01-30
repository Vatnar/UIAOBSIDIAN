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
- host device has unique 32-bit IP address
- Q: Does the IP address of host on which process runs suffice for identifying the process?
	- A: No, many processes can be running on the same host.
- **Identifier** includes both **IP address** and **port numbers** associated with process on host. 
- Example port numbers:
	- HTTP server: 80
	- mail server: 25
- To send HTTP message to gaia.cs.umass.edu web server:
	- IP address: 128.119.245.12
	- port number: 80
- More shortly
# What transport service does an app need?
## data integrity
- some apps (e.g., file transfer, web transactions) require 100% reliable data transfer
- other apps (e.g audio) can tolerate som loss
## timing
- some apps (e.g., Internet telephony, interactive games) require low delay to be "effective"
## throughput
- some apps (e.g., multimedia) require minimum amount of throughput to be "effective"
- other apps ("elastic apps") make use of whatever throughput they get
## security
encryption, data integrity
# Internet transport protocol services
## TCP service:
- <span style="color:rgb(255, 0, 0)">reliable transport:</span> between sending and receiving process
- <span style="color:rgb(255, 0, 0)">flow control:</span> sender won't overwhelm receiver
- <span style="color:rgb(255, 0, 0)">congestion control:</span> throttle sender when network overloaded
- <span style="color:rgb(255, 0, 0)">connection-oriented:</span> setup required between client and server processes
- <span style="color:rgb(255, 0, 0)">does not provide:</span> timing, minimum throughput guarantee, security
## UDP service:
- <span style="color:rgb(255, 0, 0)">unreliable data transfer:</span> between sending and receiving process
- <span style="color:rgb(255, 0, 0)">does not provide:</span> reliability, flow control, congestion control, timing, throughput guarantee, security, or connection setup
- Q: why bother? Why is there a UDP. A: just faster
# Internet applications, and transport protocols
| application            | application layer protocol                                        | transport protocol |
| ---------------------- | ----------------------------------------------------------------- | ------------------ |
| file transfer/download | FTP [RFC 959]                                                     | TCP                |
| e-mail                 | (sending) SMTP [RFC 5321]<br>(receiving)IMAP[9051] and POP3[1939] | TCP<br>TCP         |
| Web documents          | HTTP/1.1 [RFC 7320]<br>HTTP/3 [RFC 9114]                          | TCP<br>UDP         |
| Internet telephony     | SIP[RFC 3261]<br>RTP[RFC 3550], or prop                           | TCP or UDP<br>UDP  |
| streaming audio/video  | HTTP [RFC 7320], DASH                                             | TCP                |
| interactive games      | WOW, FPS (proprietary)                                            | UDP or TCP         |
# Securing TCP
## Vanilla TCP & UDP sockets:
- no encryption 
- cleartext passwords sent into socket traverse Internet in cleartext (!)
## Transport Layer Security (TLS)
- provides encrypted TCP connections
- data integrity
- end-point auuthentication
## TLS implemented in application layer
- apps use TSL libraries, that use TCP in turn
- cleartext sent into "socket" traverse Internet encrypted
- more in [[chapter 8]]
- 