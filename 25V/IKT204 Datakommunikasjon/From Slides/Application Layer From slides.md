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
# Web and HTTP
First, a quick review...
- web page consists of **objects**, each of which can be stored on different Web servers
- object can be HTML file, JPEG image, Java applet, audio file,...
- web page consists of <span style="color:rgb(255, 0, 0)">base HTML-file</span> which includes <span style="color:rgb(255, 0, 0)">several reference objects, each</span> addressable by a <span style="color:rgb(255, 0, 0)">URL</span> e.g., `www.someschool.edu/someDept/pic.gif`
## HTTP overview
### HTTP: hypertext transfer protocol
- Web's application-layer protocol
- client/server model:
	- client: browser that requests, receives, (using HTTP protocol) and "displays" Web objects
	- server: Web server sends (using HTTP protocol) objects in response to requests.
![[HTTP overview.jpg]]
### HTTP uses TCP:
- client initiates TCP connection (creates socket) to server, port 80
- server accepts TCP connection from client
- HTTP messages (application-layer protocol messages) exchanged between browser (HTTP client) and Web Server (HTTP server)
- TCP connection closed
### HTTP is "stateless"
- server maintains no information about past client requests
#### aside
Protocols that maintain "state" are complex!
- past history (state) moust be maintained
- if server/client crashes, their views of "state" may be inconsistent, must be reconciled

## HTTP connections: two types
### Non-persistent HTTP/1.0 [1996]
1. TCP connection opened
2. at most one object sent over TCP connection
3. TCP connection closed
downloading multiple objects required multiple connections

### Persistent HTTP/1.1 [1997]
- TCP connection opened to a server
- multiple objects can be sent over single TCP connection between client, and that server
- TCP connection closed
### Non-persistent HTTP: response time: 2RTT + file transmission time
#### RTT (definition):
time for small packet to travel from client to server and back. Stands for round-trip time
#### HTTP response time (per object):
- one RTT to initiate TCP connection
- one RTT for HTTP request and first few bytes of HTTP response to return
- object/file transmission time.
 ![[Non-persistent RTT.jpg]]
### Persistent HTTP (HTTP 1.1)
#### Non-persistent HTTP issues:
- Requires 2 RTTs per object
- OS overhead for each TCP connection
- browsers often open multiple parallel TCP connections to fetch reference objects in parallel.
#### Persistent HTTP (HTTP1.1):
- server leaves connection open after sending response
- subsequent HTTP messages between same client/server sent over open connection
- client sends requests as soon as it encounters a referenced object
- as little as one RTT for all the referenced objects (cutting response time in half)

## HTTP message
### HTTP Request message
- two types of HTTP messages: <span style="color:rgb(255, 0, 0)">request, response</span> 
- <span style="color:rgb(255, 0, 0)">HTTP request message:</span> 
	- ASCII (human-readable format)
![[ASCCIIHTML.jpg]]
#### General format:
![[general format of HTTP request.jpg]]
#### Other HTTP Request messages
##### Post method:
- web page often includes form input
- user input sent from client to server in entity body of HTTP POST request message

##### GET method (for sending data to server)
- include user data in URL field of HTTP GET request message (following a '?')
##### HEAD method:
- requests headers (only) that would be returned if specified URL were requested with an HTTP GET method.
##### PUT method:
- uploads new file (object) to server
- completely replaces file that exists at specified URL with content in entitiy body of PUT HTTP request message.
### HTTP response message
![[HTTPresponse.jpg]]
#### HTTP response status codes
- status code appears in 1st line in server-to-client response message.
- some sample codes:
- <span style="color:rgb(255, 0, 0)">200 OK</span>
	- requests succeeded, requested object later in this message
- <span style="color:rgb(255, 0, 0)">301 Moved Permamently</span> 
	- requested object moved, new location specified later in this message (in Location: field)
- <span style="color:rgb(255, 0, 0)">400 Bad Request</span> 
	- request msg not understood by server
- <span style="color:rgb(255, 0, 0)">404 Not Found</span> 
	- requested document not found on this server
<span style="color:rgb(255, 0, 0)">505 HTTP Version Not Supported</span> 
## Maintaining user/server state: cookies
Web sites and client browser use cookies to maintain some state between transactions.
### four components:
1. cookie header line of HTTP response message
2. cookie header line in next HTTP request message
3. cookie file kept on user's host, managed by user's browser
4. back-end database at Web site
### Example:
- Susan uses browser on laptop, visits specific e-commerce site for first time
- when initial HTTP requests arrrives at site, site creates:
	- unique ID (AKA cookie)
	- enttry in backend databse for ID
- subsequent HTTP requests from Susan to this site will contain Cookie ID value allowing site to Identify susan.
![[maintainingstatewithcookies.jpg]]
## Web caches
<span style="color:rgb(255, 0, 0)">Goal</span>: satisfy client requests without involving origin server
- user configures browser to point to a (local) <span style="color:rgb(255, 0, 0)">Web Cache</span> 
- browser sends all HTTP requests to cache
	- if object in cache: cache returns object to client
	- else cache requests object from origin server, caches received object, then returns object to client.
## Conditional GET
goal: don't send object if cache has up-to-date cached version
	- no object transmission delay (or use of network resources)
- client: specify date of cached copy in HTTP request
	if-modified-since: <date;
- server: response contains no object if cached copy is up-to-date: `HTTP/1.0 304 Not Modified`
![[condit.jpg]]

## HTTP/2 
Key Goal: decreased delay in multi-object HTTP requests

HTTP1.1: introduced multiple, pipelined GETs over single TCP connection
- server responds in-order (FCFS: first-come-first-served scheduling) to GET requests
- with FCFS, small object may have to wait for transmission (head-of-line (HOL) blocking)) behind large objects
- loss recovery (retransmitting lost TCP segments) stalls object transmission

HTTP/2: [RFC 7540, 2015] increased flexibility at server in sending objects to client:
- methods, status codes, most header fieds unchanged from 1.1 but represented in compressed binary frames
- transmission order of requested objects based on client-specified object priority (not necessarily FCFS)
- push unrequested objects to client
- divide object into frames schedule frame to mitigate HOL blocking
### Mitigating HOL blocking HTTP2
HTTP 1.1: client requests 1 large object (e.g., a big chunk of a video file) and 3 smaller objects
![[mitigate.jpg]]
HTTP/2: objects divided into frames. frame transmission interleaved
![[mitigate2.jpg]]
## HTTP/2 to HTTP/3
HTTP/2 over single TCP connection means:
- recovery from packet loss stil stalls all object transmission
	- as in HTTP 1.1, browsers have incentive to open multiple parallel TCP connections to reduce stalling, increase overall throughput
- no security over vanilla TCP connection
HTTP/3: adds security, per object error- and congestion-control (more pipelining) over UDP
- More on HTTP/3 in transport layer

# E-mail SMTP
## E-mail
### Three major Components:
- user agents
- mail servers
- simple mail transfer protocol: SMTP
### User Agent
- a.k.a "mail reader"
- composing, editing, reading mail messages
- e.g., Outlook, iPhone mail client
- outgoing, incoming messatges stored on server. 
 ![[EMAIL.jpg]]
## SMTP RFC [~~821, 2811, ~~5321]
- uses TCP to reliably transfer  email message from client (mail server initiating connection) to server, port 25 (or TLS port 587)
	- direct transfer: sending server (acting like client) to receiving server
- three phases of transfer
	- SMTP handshaking (greeting)
	- SMTP transfer of messages
	- SMTP closure
- command/response interaction (like HTTP)
	- commands: ASCII text
	- response: status code and phrase
![[mail.jpg]]
```SMTP
S: 220 smtp.example.com ESMTP Postfix

C: HELO relay.example.org

S: 250 Hello relay.example.org, I am glad to meet you

C: MAIL FROM:<bob@example.org>

S: 250 Ok

C: RCPT TO:<alice@example.com>

S: 250 Ok

C: RCPT TO:<theboss@example.com>

S: 250 Ok

C: DATA

S: 354 End data with <CR><LF>.<CR><LF>

C: From: "Bob Example" <bob@example.org>

C: To: "Alice Example" >alice@example.com>

C: Cc: <theboss@example.com>

C: Date: Tue, 15 Jan 2008 16:02:43 -0500

C: Subject: Test message

C:

C: Hello Alice.

C: This is a test message with 5 header fields and 4 lines in the message body.

C: Your friend,

C: Bob

C: .

S: 250 Ok: queued as 12345

C: QUIT

S: 221 Bye
```
## Mail message format
SMTP: protocol for exchanging e-mail messages, defined in RFC 5321.
RFC 5322 defines syntax for email message itself like html defines syntax for web docs.

![[2025.01.30.10.16.25.442 POWERPNT.jpg]]
![[ESMTP.jpg]]![[esmpt2.jpg]]
![[2025.01.30.10.18.25.887 POWERPNT.jpg]]
# DNS: Domain Name System
people: many identifiers: SSN, name, passport

internet hosts, router:
- IP Address (32 bit) - used for addressing datagrams
- "name", e.g., vg.no - used by humans
Q: how to map between IP address and name, and vice versa
## Domain Name System (DNS):
- distributed database implemented in hierarchy of many name servers
- application-layer protocol: hosts, DNS servers communicate to resolve names (address/ name translation) 
	- note: core internet function, implemented as application-layer protocol
	- complexity at network's "edge"
## DNS: services, strucutre
### DNS services:
- hostname-to-IP-address translation
- host aliasing
	- canonical , alias names
- mail server aliasing
- load distributiojn
	- replicated Web servers: many IP addresses correspond to one name
Q: Why not centralize DNS?
- single point of failure
- traffic volume
- distant centralized database
- maintenance
A: doesnt scale!
- Comcast DNS servers alone: 600B DNS queries/day
- Akamai DNS servers alone: 2.2T DNS queries./day
### Thinking about the DNS
humongous distributed database:
- ~ billion records, each simple
- handles many trillions of queries/day:
	- many more reads than wrirtes
	- performance matters: almost very internet transaction interacts with DNS - msecs count!
organizationally, phyiscally decentralized:
- millions of different organizations responsible for their records
Bulletproof: reliability, security. 
![[DNSdatabse.jpg]]
#### DNS: root name servers
- official, contact-of-last-resort by name servers that can not resolve name
- incredibly imoportant internet function
	- internet couldnt function without
	- DNSSEC - provides security (authentication, message integrity)
- ICANN (internet corporation for assigned names and numbers) manages root DNS domain
![[rootdns.jpg]]
#### Top-level domain, and authoritative servers
##### Top-levell domain TLD servers:
- responsible for .com, .org, .net, .edu, and all top-level country domains. .no, .uk
- network solutions, authooritive registry for .com, .net. TLD.
- educase .edu
#### authorative DNS service
- organizations own DNS servers, providing authjoritative hostname to IP mappings for organizations named hosts
- can be maintained by orgnaization or ISP.
- §when host makes DNS query, it is sent to its local DNS server

•Local DNS server returns reply, answering:

•from its local cache of recent name-to-address translation pairs (possibly out of date!)

•forwarding request into DNS hierarchy for resolution

•each ISP has local DNS name server; to find yours:

•MacOS: % scutil --dns

•Windows: >ipconfig /all

§local DNS server doesn’t strictly belong to hierarchy

![[2025.01.30.10.39.46.073 POWERPNT.jpg]]![[2025.01.30.10.39.57.682 POWERPNT.jpg]]![[2025.01.30.10.42.04.450 POWERPNT.jpg]]
## Getting your info into the DNS
example: new startup "network utopia"
1. register name networkuptopia.com at DNS registrar e.g domeneshop
	- provide names, ip addresses of autoritative name server, primary and secondary
	- registrar inserts NS, A RRs into .com TLD server
	`networkutopia.com, dns1.networkutopia.com, NS)`
	 `(dns1.networkutopia.com, 212.212.212.1, A)`
2. create authoritative DNS server locally with IP Adress `212.212.212.1`
	- type A record for www.networkuptopia.com
	- type MX record
## DNS security
### DDoS attacks
- bombard root servers with traffic
	- not successful to date
	- traffic filtering
	- local DNS servers cache IPs of TLD servers, allowing root server bypas
- bombard TLD servers
	- potentially more dangerous
- spoofing attacks
	- intercept DNS queries, returning bogus replies
	- DNS cache poisoning
	- RFC 4033: DNSEC authentication services.
# P2P applications
- no always-on server

- arbitrary end systems directly communicate

- peers request service from other peers, provide service in return to other peers

- self scalability – new peers bring new service capacity, and new service demands

- peers are intermittently connected and change IP addresses

- complex management

- examples: P2P file sharing (BitTorrent), streaming (KanKan), VoIP (Skype)
# File distribution: client-server vs P2p
Q: how much time to distribrute file (size F) from one server to N peers?
- peer upload/download capacity is limited resource
![[2025.01.30.10.50.26.472 POWERPNT.jpg]]
# File distribution time: P2P
- server transmission: must upload at least one copy:
	- time to send one copy: $F/u_s$ 
- client: each client must download file copy
	- min client dowanlod time: $F/d_{min}$ 
- clients: as aggregate must download NF bits
	- max upload rate (limiting max download rate) is $u_s+\Sigma u_{i}$ 
	Time to distribute F to N clients using P2p Approach
	$$
D_{P2P}\geq \max{(F/U_{s}\;,F/d_{min}, NF/(u_{s}+\Sigma u_{i}))}
$$
NF incereases linearly, but so does the capacity. 
![[2025.01.30.10.55.20.124 POWERPNT.jpg]]
![[2025.01.30.10.55.33.211 POWERPNT.jpg]]
# Video streaming and content distribution networks
## Video streaming and CDNs: context
- stream video traffic: major consumer of internet banmdwith
	- netflix, youtube, amazon prime: 80% of residential isp traffic 
- challenge: scale - how to reach ~1B users?
- challenge: heterogeneity
	- different users have different capabilities (e.g wired versus mobvile; vbandwith rich versus bandwidh poor)
- solution: distributed, application-level infrastructure.
CDN: stores copies of content at CDN nodes
subscriber requests content, service provider returns manifest
- using manifest, client retrieves content at highest supportab le rate
- mayu choose different rate or copy if network path congested
![[2025.01.30.10.58.24.830 POWERPNT.jpg]]
# wireshark
![[2025.01.30.10.58.42.381 POWERPNT.jpg]]
