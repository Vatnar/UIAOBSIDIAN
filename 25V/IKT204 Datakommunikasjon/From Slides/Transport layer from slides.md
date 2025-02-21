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
# Exercises Chapter 3 TCP
## Exercise 1

**How many sockets does a UDP server need to serve N clients?**
A UDP server only require one socket to server an arbitrary amount of clients. UDP is connectionless, it instead listens on a single socket and distinguishes clients based on senders IP and PORT.
## Exercise 2 (R3)

**How is a UDP socket fully identified? What about a TCP socket? What is the difference between the full identification of both sockets?**
A UDP socket is fully identified by the IP-address and port. The TCP socket is identified by the servers (destination) iP-address and port and the clients ip address and port. The difference is due to UDP being connectionless and TCP requiring a connection (individual socket per connection). 4 tuple.

## Exercise 3 (Ch. 2.7, R26)

**If a TCP server were to support N simultaneous connections, each from a different client, how many sockets would the TCP server need?**
The TCP server would need N+1 sockets, one for each ongoing connection, and one for initial contact (listening socket). 

## Exercise 4 (R10)

**What is the purpose of timers in TCP?**
To account for packet loss. If the coundown timer runs out the packets gets retransmitted. This timer can run out either if the packet itself is lost or the ACk packet.
- **Retransmission Timer:** Used to retransmit lost packets after a timeout.
- **Persistence Timer:** Prevents deadlock when the receiver’s window size is zero.
- **Keepalive Timer:** Detects if a connection is still active.
- **Time-Wait Timer:** Ensures the connection is closed properly before reusing ports.
## Exercise 5 (R15)

**Suppose Host A sends two TCP segments back-to-back to Host B over a TCP connection. The first segment has sequence number 90; the second has sequence number 110.**

1. **How much data is in the first segment?**
	20 bytes
2. **Suppose that the first segment is lost but the second segment arrives at B. In the acknowledgment that Host B sends to Host A, what will be the acknowledgment number?**
	90
## Exercise 6 (P15)

**Consider the cross-country example shown in Figure 3.17. Suppose that the round-trip time RTT is 33 milliseconds, the channel transmission rate _R_ is 1.2 Gbps, and the size of a packet is 1500 bytes, including both header fields and data. ACK packets are small, and their transmission delay can be ignored.**
![[Pasted image 20250221110333.png]]


1. **How big is channel utilization (in percent) when a *stop-and-wait* protocol is used?**
	
2. **How many unacknowledged segments in transit are permissible to achieve a channel-utilization greater than 98 percent when a *pipelined protocol* is used?**
3. **What is this in terms of window size, i.e., the range of permissible sequence numbers for transmitted but not yet acknowledged packets?**
## **Exercise 6 (P15) Solution**

### **1. Channel Utilization with Stop-and-Wait**
The channel utilization for a stop-and-wait protocol is given by:

$$
U = \frac{T_{\text{trans}}}{T_{\text{trans}} + RTT} \times 100
$$

Where:
 $T_{\text{trans}}$ is the transmission time:

$$
T_{\text{trans}} = \frac{\text{Packet Size}}{\text{Channel Rate}} = \frac{12000}{1.2 \times 10^9} \text{ seconds}
$$

- \( RTT = 33 \) ms \( = 0.033 \) seconds

Computing:

$$
U = \frac{\frac{12000}{1.2 \times 10^9}}{\frac{12000}{1.2 \times 10^9} + 0.033} \times 100 \approx 0.0303\%
$$

Thus, the channel utilization for stop-and-wait is **0.0303%**, which is extremely low.

---

### **2. Number of Unacknowledged Segments for >98% Utilization**
For a pipelined protocol, we use:

$$
N = \frac{RTT}{T_{\text{trans}}}
$$

To achieve more than 98% utilization:

$$
U = \frac{N \times T_{\text{trans}}}{RTT + T_{\text{trans}}} > 0.98
$$

Rearranging for \( N \):

$$
N > \frac{0.98 \times (RTT + T_{\text{trans}})}{T_{\text{trans}}}
$$

Substituting values:

$$
N > \frac{0.98 \times (0.033 + \frac{12000}{1.2 \times 10^9})}{\frac{12000}{1.2 \times 10^9}}
$$

$$
N \approx 3235
$$

Thus, at least **3235 unacknowledged segments** are required.

---

### **3. Window Size**
The window size in a pipelined protocol corresponds to the number of unacknowledged segments in transit:  

$$
\text{Window Size} \geq 3235
$$

Thus, the required window size is **at least 3235** to achieve the desired utilization.
