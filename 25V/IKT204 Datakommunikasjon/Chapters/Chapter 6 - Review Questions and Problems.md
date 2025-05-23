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
	Because the response should be returned to the original sender who requested it and not to all other devices.

---

## Exercise 4 (R15 variant)
Each host and router have an ARP table in its memory (an ARP cache).

A. What is the content of this table?  
This table holds the mappings between known IP-addresses to MAC addresses. If the device in question is not adjecent to the device (meaning one switch seperating) the MAC address consists of the MAC of the router.
B. What is the main reason for having such a table?  
	Switches are link-layer devices and cannot read IP headers, it rather works based on physical addresses.
A. The ARP table (or ARP cache) holds mappings between **IP addresses and MAC addresses**. These mappings are for devices on the **same local network segment** (i.e., the same broadcast domain). If the destination IP address is not on the same local network (e.g., on another subnet), the MAC address in the ARP table will be the **MAC address of the router’s interface** (default gateway) that connects to the next hop.
 B. The main reason for having an ARP table is to **efficiently map IP addresses to MAC addresses** to enable communication at the data link layer. Since switches are link-layer devices and do not read IP headers, the ARP table allows hosts and routers to **quickly resolve IP addresses to physical MAC addresses** without needing to send an ARP request every time.
---

## Exercise 5 (R14 variant)
Consider three LANs interconnected by two routers, as shown in the figure below.  

![[image-fbfc5242-ca74-4de2-be4a-bef8a1a83168.png]]  

A. Host F is sending an IP datagram to Host A. Suppose all ARP tables are up to date. Describe and enumerate all the steps, as done for the single-router example in Section 6.4.1.  

1. **Host F Constructs the IP Datagram:**
    
    - Host F sets the **destination IP address** in the IP header to **192.168.10.10** (Host A's IP).
    - It checks its ARP table for the **MAC address corresponding to the default gateway (R2)** since Host A is on a different subnet.
    - The ARP table of Host F contains the MAC address of **R2’s eth1 interface (33-33-33-33-33-01)**.
    - Host F encapsulates the IP datagram into a **frame** with:
        - **Source MAC:** 33-33-33-33-33-10 (Host F)
        - **Destination MAC:** 33-33-33-33-33-01 (R2 eth1)
    - The frame is sent to **Switch3**, which forwards it to **R2**.
2. **Router R2 Receives the Frame:**
    
    - R2 **de-encapsulates the frame**, extracts the IP datagram, and inspects the **destination IP address (192.168.10.10)**.
    - R2 uses its **routing table** to determine the next hop and finds that the destination is reachable via **R1**.
    - R2 encapsulates the datagram into a new frame with:
        - **Source MAC:** 22-22-22-22-22-02 (R2 eth0)
        - **Destination MAC:** 22-22-22-22-22-01 (R1 eth1)
    - The frame is sent to **Switch2**, which forwards it to **R1**.
3. **Router R1 Receives the Frame:**
    
    - R1 **de-encapsulates the frame**, checks the **destination IP (192.168.10.10)**, and determines that the destination is on its **eth0 interface** (Subnet 1).
    - R1 uses its ARP table to find Host A’s MAC address (**11-11-11-11-11-10**).
    - R1 encapsulates the datagram into a new frame with:
        - **Source MAC:** 11-11-11-11-11-01 (R1 eth0)
        - **Destination MAC:** 11-11-11-11-11-10 (Host A)
    - The frame is sent to **Switch1**, which forwards it to **Host A**.
4. **Host A Receives the Frame:**
	    Processes the frame recognizing its own MAC address and de-encapsulates the IP datagram and passes it to network layer.

B. Assume that the ARP table in the sending host F is empty (and the other tables are up to date). Describe and enumerate all the steps.  
1. **Constructs ip datagram with destination IP of Host A.**
	Host A is on a different subnet so F sends datagram to default getaway (R2).
2. **ARP request created with broadcast address FFFFFFFFFFFFFFFF.**
	The arp request gets broadcasted by the switch Switch3. to the entire subnet.
3. **Router recieves the broadcast and recognizes its IP address and replies with an ARP reply.**
	It is sent directly (uni-cast) and not broadcasted
4. **Host F updates its  ARP cache.**
5. **The rest of the steps are the same as in A.**
C. Subnet 2 is interconnected with other networks via two routers. Can the hosts in this subnet have two default gateway routers? Discuss how traffic out of this subnet is handled. (Hint: Can DHCP provide some options?)  

It is theoretically possible to be configured with two getaway routers but it can lead to issues.
The best approach is to use one default getaway with a dynamic routing protocol between like OSPF or BGP.

---

## Exercise 6 (R26)
Let us consider the operation of a learning switch in the context of a network in which 6 nodes labeled A through F are star connected into an Ethernet switch.  
Suppose that:  
- (i) B sends a frame to E  
- (ii) E replies with a frame to B  
- (iii) A sends a frame to B  
- (iv) B replies with a frame to A  

The switch table is initially empty. Show the state of the switch table before and after each of these events. For each of these events, identify the link(s) on which the transmitted frame will be forwarded, and briefly justify your answers.  

i)
Host E doesn't necessarily need to respond to B and therefore only host B's address is learned
& denotes address of (MAC). The interfaces number are arbitrary.

| Host  | Interface |
| ----- | --------- |
| $\&B$ | 1         |
Since the switch doesnt know the interface of E, it floods the network (multiplexes the frame) to all devices except from B. 

ii)
Now the switch learns E's address since it can read the address from the header field of the frame.

| Host  | Interface |
| ----- | --------- |
| $\&B$ | 1         |
| $\&E$ | 2         |
iii)
The switch learns what interface A resigns on.

| Host  | Interface |     |
| ----- | --------- | --- |
| $\&B$ | 1         |     |
| $\&$E | 2         |     |
| $\&A$ | 3         |     |
iii)
Nothing new happened.

---

## Exercise 7 (R33)
Consider the hierarchical network in Figure 6.30 below and suppose that the data center needs to support e-mail and video distribution among other applications.  
Suppose **four** racks of servers are reserved for e-mail and **four** racks are reserved for video. For each of the applications, all four racks must lie below a single tier-2 switch since the tier-2 to tier-1 links do not have sufficient bandwidth to support the intra-application traffic.  
For the e-mail application, suppose that for 99.9 percent of the time only three racks are used, and that the video application has identical usage patterns.  

A. For what fraction of time does the e-mail application need to use a fourth rack? How about for the video application?  

Each application have 4 dedicated racks. Since they use 3 of them 99.9% of the time it uses the 4th rack for $1-99.9\% = 0.1\%$ of the time.

B. Assuming e-mail usage and video usage are independent, for what fraction of time do both applications need their fourth rack?  

The time where both of them use the same time is the intersection of these events meaning$0.1\% \cdot 0.1\% =0.0001\%$ 

![[image-dcd75e26-8b85-45af-aa57-050aa2306ae1.png]]
