```table-of-contents
```
# Exercises Chapter 3 UDP
## Exercise 1 (r3)
**How is a UDP socket fully identified**:
A UDP socket is fully identified by using an IP-address + port number since one IP-address can haver multiple sockets running. 

## Exercise 2 (R4)
**Describe why an application developer might choose to run an application over UDP rather than TCP.**:
UDP does not introduce any delay when establishing a connections since it doesn't like TCP does. UDP just spews out data and requires 
## Exercise 3 (R6)
**Is it possible for an application to enjoy reliable data transfer even when the application runs over UDP? If so, how?**:

## Exercise 4 (R7)

**Suppose a process in Host C has a UDP socket with port number 6789. Suppose both Host A and Host B each send a UDP segment to Host C with destination port number 6789. Will both of these segments be directed to the same socket at Host C? If so, how will the process at Host C know that these two segments originated from two different hosts?**:

## Exercise 5 (P1)

**Suppose Client A requests a web page from Server S through HTTP (which uses TCP) and its socket is associated with port 33000.**

1. **What are the source and destination ports for the segments sent from A to S?**
2. **What are the source and destination ports for the segments sent from S to A?**
3. **Can Client A contact to Server S using UDP as the transport protocol?**