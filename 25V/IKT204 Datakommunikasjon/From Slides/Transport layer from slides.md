```table-of-contents
```
# Exercises Chapter 3 UDP
## Exercise 1 (r3)
**How is a UDP socket fully identified**:
A UDP socket is fully identified by using an IP-address + port number since one IP-address can haver multiple sockets running. 

## Exercise 2 (R4)
**Describe why an application developer might choose to run an application over UDP rather than TCP.**:
UDP does not introduce any delay when establishing a connections since it doesn't like TCP does. UDP just spews out data and requires the application to choose how to handle it. Due to the lack of initial delay and ability to spew out as much as the application wants it might be favorable when speed and throughput is more valuable than reliability. 
## Exercise 3 (R6)
**Is it possible for an application to enjoy reliable data transfer even when the application runs over UDP? If so, how?**:
Yes, but it requires the application to manually validate the payloads since there is no inherent indexing of UDP segments. The UDP segment does contain a checksum that can be used for error-checking for invalid segments, but due to the inner workings of the network layer the order cannot be guaranteed. 
## Exercise 4 (R7)

**Suppose a process in Host C has a UDP socket with port number 6789. Suppose both Host A and Host B each send a UDP segment to Host C with destination port number 6789. Will both of these segments be directed to the same socket at Host C? If so, how will the process at Host C know that these two segments originated from two different hosts?**: The header of the UDP segment contains the source IP and port of the sender which lets Host C differentiate the transmitting hosts. Normally a server will have a dedicated socket to establish incoming request

## Exercise 5 (P1)

**Suppose Client A requests a web page from Server S through HTTP (which uses TCP) and its socket is associated with port 33000.**

1. **What are the source and destination ports for the segments sent from A to S?**
	The source port of A cannot be determined since it is not implicitly inherent of the destination port of S. But S can read the source port from the segment header. The destination port would be 33000.
2. **What are the source and destination ports for the segments sent from S to A?**
	In this instance the source and destination ports would be flipped.
3. **Can Client A contact to Server S using UDP as the transport protocol?**
	Yes, if its using (HTTP/3).
	HTTP
	HTTP1.0
	HTTP1.1
	HTTP/2
	HTTP/3