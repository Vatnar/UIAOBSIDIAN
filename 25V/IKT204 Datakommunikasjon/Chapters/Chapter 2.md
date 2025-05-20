```table-of-contents
```
## Principles of Network Application

### Network Application Architectures
#### Client-server-architecture
always-on host called server
- The servers services requests from other hosts, called clients.
	e.g Web application that is always-on.  Web server services requests from browsers running on client hosts. 
In this architecture clients do not directly communicate with each other; in a web applications two browsers do not directly communicate. 
- The server has a fixed known address IP-address. 
-  client can always contact the server by sending a packet to the server's IP address. 
Examples:  Web, FTP, Telnet, and e-mail	

Often a single server host cannot serve all client hosts, therefore it is common to have a *data center* which act as a large powerful virtual server. Google, bing, Amazon, gmail, Facebook, and so forth, runs in one or more data center. A data center could have hundreds of thousands of servers.
![[ClientServer.png]]

#### Peer-to-peer architecture
In P2P architecture there is minimal or no reliance on servers in data centers. It uses direct communication between pairs of intermittently connected hosts, called peers. Cause the peers communicate without passing through a dedicated server it is called peer to peer. 
Examples: BitTorrent. 
Pros: 
	Self-scalability, For example in a file sharing application, each user generates workload, but also adds service capacity. They are also cost effective.
But they do face challenges in security, performance, and reliability since they are decentralized. 
![[p2p.png]]
### Processes Communicating
