# Networking Exercises

## Exercise 1 (R2)
If all the links on the Internet were to provide reliable delivery service, would the TCP reliable delivery service be redundant? Why or why not?

No due to congestion the packets could still be reordered which could cause problems.

- **Packet Ordering:** Even if all links reliably delivered packets, they might not necessarily deliver them in the same order they were sent. TCP handles reordering by numbering packets and reassembling them in the correct order at the destination.
    
- **Congestion Control:** Reliable links do not necessarily handle congestion control. Without TCP's congestion control mechanisms (like slow start and congestion avoidance), networks could easily become overloaded, leading to severe performance degradation.
    
- **Flow Control:** TCP also manages flow control to ensure that the sender does not overwhelm the receiver's buffer capacity.
---

## Exercise 2 (R10)
Suppose nodes A, B, and C each attach to the same broadcast LAN (through their adapters).

1. If A sends thousands of IP datagrams to B with each encapsulating frame addressed to the MAC address of B, will C’s adapter process these frames? If so, will C’s adapter pass the IP datagrams in these frames to C’s network layer?
C will ignore these frames.
2. How would your answers change if A sends frames with the MAC broadcast address?
If so yes

---

## Exercise 3
1. Why is an ARP query sent within a broadcast frame?
	The physical addresses might not be known on before hand
2. Why is an ARP response sent within a frame with a specific destination MAC address?
	

---

## Exercise 4 (R15 variant)
Each host and router have an ARP table in its memory (an ARP cache).

A. What is the content of this table?  
B. What is the main reason for having such a table?  

---

## Exercise 5 (R14 variant)
Consider three LANs interconnected by two routers, as shown in the figure below.  

![[image-fbfc5242-ca74-4de2-be4a-bef8a1a83168.png]]  

A. Host F is sending an IP datagram to Host A. Suppose all ARP tables are up to date. Describe and enumerate all the steps, as done for the single-router example in Section 6.4.1.  
B. Assume that the ARP table in the sending host F is empty (and the other tables are up to date). Describe and enumerate all the steps.  
C. Subnet 2 is interconnected with other networks via two routers. Can the hosts in this subnet have two default gateway routers? Discuss how traffic out of this subnet is handled. (Hint: Can DHCP provide some options?)  

---

## Exercise 6 (R26)
Let us consider the operation of a learning switch in the context of a network in which 6 nodes labeled A through F are star connected into an Ethernet switch.  
Suppose that:  
- (i) B sends a frame to E  
- (ii) E replies with a frame to B  
- (iii) A sends a frame to B  
- (iv) B replies with a frame to A  

The switch table is initially empty. Show the state of the switch table before and after each of these events. For each of these events, identify the link(s) on which the transmitted frame will be forwarded, and briefly justify your answers.  

---

## Exercise 7 (R33)
Consider the hierarchical network in Figure 6.30 below and suppose that the data center needs to support e-mail and video distribution among other applications.  
Suppose **four** racks of servers are reserved for e-mail and **four** racks are reserved for video. For each of the applications, all four racks must lie below a single tier-2 switch since the tier-2 to tier-1 links do not have sufficient bandwidth to support the intra-application traffic.  
For the e-mail application, suppose that for 99.9 percent of the time only three racks are used, and that the video application has identical usage patterns.  

A. For what fraction of time does the e-mail application need to use a fourth rack? How about for the video application?  
B. Assuming e-mail usage and video usage are independent, for what fraction of time do both applications need their fourth rack?  

![[image-dcd75e26-8b85-45af-aa57-050aa2306ae1.png]]
