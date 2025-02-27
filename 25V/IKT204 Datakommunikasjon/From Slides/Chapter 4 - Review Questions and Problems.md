**Exercise 1 (R3)**

We made a distinction between the forwarding function and the routing function performed in the network layer. What are the key differences between routing and forwarding?

Routing can be analogous to finding the overall route from point A to B using google maps. Routing is to determine the whole path. Forwarding can be analogous to taking each turn on your route, choosing turns.

**Exercise 2 (R17)**

Suppose Host A sends Host B a TCP segment encapsulated in an IP datagram. When Host B receives the datagram, how does the network layer in Host B know it should pass the segment (that is, the payload of the datagram) to TCP rather than to UDP or to some other upper-layer protocol?
The IP Datagram header includes a field called protocol (next hdr, IPV6) which specifies what protocol the underlying data is.

**Exercise 3 (R18)**

What field in the IP header can be used to ensure that a packet is forwarded through no more than N routers?

The TTL field is the closest field to that. On each router the packet passes through the TTL gets decreased by one.

**Exercise 4 (R21)**

How many IP addresses does a router have?
A router has multiple IP addresses. Each interface has its own IP address. Aditionally there is usually a loop ba ck address. Multiple subnets also means more IP addresses.

**Exercise 5 (R25)**

Suppose an application generates 40 bytes of data that gets encapsulated in a TCP segment and then an IP datagram. (Assume that the IP “options” field is 0 bytes.)

1. a) What percentage of the datagram is overhead and what percentage is application data?
2. b) What is the overhead percentage if UDP is used instead of TCP?

a) Payload  of tcp is 40 Bytes. TCP header is 20 bytes, and IP 20 Bytes. so 50% is overhead. 40/80 = 50%.
b) 28/68 = 40%.
**Exercise 6 (P17)**

Suppose datagrams are limited to 1,500 bytes (including header) between source Host A and destination Host B. Assuming a 20-byte IP header, how many datagrams would be required to send an MP3 consisting of 5 million bytes? Explain how you computed your answer.

5 million bytes
5 10^6 bytes. 5MB

5000/1480 = 3379

**Exercise 7 (R31)**

How makes “tunneling” it possible to send IPv6 packets over IPv4 routers?
Tunnelling encapsulates a IPV6 datagram within the IPv4 payload field. The protocol field of the Ipv4 header gets filled with information saying that it should not be regarded as normal data (udp or tcp) '

**Exercise 8 (P8, P13)**

Consider an IP network using 32-bit host addresses. Suppose a router has four links, numbered 0 through 3, and packets are to be forwarded to the link interfaces as follows:

|                                                                                                 |                    |
| ----------------------------------------------------------------------------------------------- | ------------------ |
| **Destination Address Range**                                                                   | **Link Interface** |
| 11010000  00000000  00000000  00000000  <br>through  <br>11010000  00111111  11111111  11111111 | 0                  |
| 11010000  01000000  00000000  00000000  <br>through  <br>11010000  01000001  11111111  11111111 | 1                  |
| 11010000  01000010  00000000  00000000  <br>through  <br>11010001  11011111  11111111  11111111 | 2                  |
| otherwise                                                                                       | 3                  |

1. Provide a routing table that has five entries, uses longest prefix matching, and forwards packets to the correct link interfaces.  
    (Hint. The third entry needs to be split to cover the given address range.)

| Prefix matching                      | Link interface |
| ------------------------------------ | -------------- |
| **11010000 00______ ______ ______ ** | 0              |
| **11010000 01000000 0_____ ______ ** | 1              |
| **11010000 01000010 ______ ______ ** | 2              |
| **11010000 110____ ______ ______ **  | 2              |
| __ _ ___ _____  ____ _  _____ ___ __ | 3              |


1. Rewrite this routing table using the CIDR a.b.c.d/x notation instead of the binary string notation.

|              |     |
| ------------ | --- |
| 208.0.0.0/18 |     |

1. Describe how your forwarding table determines the appropriate link interface for datagrams with destination addresses:

|                                        |
| -------------------------------------- |
| 11010001  11110111  01110011  00111001 |
| 11010000  00001100  10101101  11100100 |
| 11010000  01000000  11000011  01110010 |
| 11010001  10001111  01100111  00011111 |