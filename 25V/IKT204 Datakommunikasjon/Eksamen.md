```table-of-contents
```
SEQ = Previous packed , SEQ + payload size
ACK = received packet SEQ + payload size

SEQ random first
Stop and wait vente på ACK
dårlig utnyttelse

pipelining
instead of  waiting for ack, send continuously 
Server responds with ack of the packet its waiting for. 

TCP has 3 error handling mechanisms
- Timer
	- Timeout. 
- Cumulative ACK
	- If an ack is lost, client can see that the server responds for the next one. 
- Fast Transmit
	- Resends old ack value, duplicate ACKS. If 3 duplicate ACKS resend data.
	- If timers times out then its sent because of the timer instead.
	- After fast transmit can be selective ack or cumulative ack on this one
- Fast transmit pipelining

Exam access to programmer calculator

# IKT204 Exam Study Guide

## 1. Internet 5-layer Model

- Learn packet names per layer:
    
    - Application: Message
        
    - Transport: Segment
        
    - Network: Datagram
        
    - Link: Frame
        
    - Physical: Bits
        
- The entire set is called the Protocol stack.
    

---

## 2. Wireshark & TCP Session Analysis

- Identify protocols at each layer (Ethernet, IP, TCP, HTTP).
    
- Understand window size, sequence numbers, and ACKs.
    
- Cookies: small data stored by browser, exchanged in HTTP headers.
    
- Types of connections: Persistent vs Non-persistent.
    
- Packet analysis: find sender, client port, data bytes, number of routers (TTL), who closes connection.
    

---

## 3. DNS (Domain Name System)

- Uses UDP port 53, application layer.
    
- Understand difference between recursive and iterative queries.
    
- Hierarchy: Root > TLD > Authoritative.
    
- Only registrars can add domains.
    
- DNS is not encrypted by default.
    

---

## 4. DHCP (Dynamic Host Configuration Protocol)

- Application layer, client-server protocol.
    
- Assigns:
    
    - IP address
        
    - Subnet mask
        
    - Gateway (router)
        
    - Local DNS server
        
- Does not assign MAC, socket, or ISP DNS/TLD IPs.
    

---

## 5. UDP Service Guarantees

- Offers no guarantees:
    
    - No reliability
        
    - No order
        
    - No authentication
        
- Correct choice: None of these
    

---

## 6. TCP Sequence & Retransmission

- Sequence and ACK numbers
    
- Reno variant: retransmits after triple duplicate ACK.
    
- Timeout = retransmit all unacknowledged segments.
    
- Out-of-order segments are buffered.
    

---

## 7. TCP Congestion Control

- Slow Start, Congestion Avoidance, Fast Recovery
    
- AIMD: Additive Increase, Multiplicative Decrease
    
- Triple duplicate ACK → Fast Recovery
    
- Timeout → Slow Start
    
- Average throughput = MSS / RTT * (3/4 * cwnd_max)
    
- Know how cwnd evolves over time (sawtooth shape).
    

---

## 8. Subnetting (IPv4)

- Practice subnetting blocks like 85.175.130.0/23 into 4 equal parts.
    
- Understand CIDR, prefix length, and host bits.
    
- 2^host_bits - 2 = usable hosts per subnet.
    

---

## 9. Routing Protocols

- BGP = between Autonomous Systems
    
    - Uses AS-PATH
        
    - Called a path vector protocol
        
    - Prefix = CIDR block
        

---

## 10. Routing Table Matching

- Match destination IP to longest prefix in routing table.
    
- Convert dotted-decimal to binary if necessary.
    

---

## 11. Dijkstra’s Algorithm (Link-State Routing)

- Understand steps of algorithm.
    
- Track:
    
    - Visited nodes N'
        
    - Distance D(n)
        
    - Predecessor p(n)
        
- Be familiar with notation: e.g., D(v) = 6, p(v) = x → 6x
    

---

## 12. Ethernet and Switching

- IEEE standard: 802.3
    
- Topology: Star with switch
    
- Cable: Twisted-pair
    
- Mask for /22 = 255.255.252.0
    
- Gateway typically ends with .1
    
- Switches forward by MAC address, self-learn switch table.
    

---

## 13. ARP (Address Resolution Protocol)

- Converts IP → MAC
    
- Operates between network and link layer
    
- ARP broadcast: ff:ff:ff:ff:ff:ff
    
- MAC: 48 bits
    
- Hosts can have multiple IPs & MACs
    

---

## 14. Delay Calculations

- Frame length: add payload + headers (TCP, IP, Ethernet)
    
- Transmission delay = bits / link speed
    
- Propagation delay = distance / speed
    
- RTT = 2 × propagation delay
    

---

## 15. Wireless & Wi-Fi (IEEE 802.11)

- Signal issues:
    
    - Path loss, Interference, Multipath
        
- Modes:
    
    - Infrastructure = AP to Internet
        
    - Ad-hoc = host-to-host
        
- Access method: CSMA/CA
    
- Frames: Beacon, RTS, CTS
    
- Wi-Fi bands: 2.4 GHz & 5 GHz
    
- Sleep mode devices wake up for beacon frames
    

---

## 16. SSL/TLS & Cryptography

- TLS 1.2 used
    
- Cipher suite: ECDHE-RSA-AES256-GCM-SHA384
    
    - ECDHE = key exchange (Diffie-Hellman over ECC)
        
    - RSA = digital signature (signed with server private key)
        
    - AES-GCM = encryption + integrity
        
    - SHA-384 = hash for integrity
        
- Digital certificate authenticates server
    
- Symmetric key used after handshake
    

---

## IKT204 Exam Study Guide

### Key Concepts to Remember

#### 1. Internet 5-Layer Model

- Know the names of data units at each layer.
    
- Understand the overall structure of the protocol stack.
    

Read: Chapter 1.5, p. 62–63

---

#### 2. Wireshark & HTTP over TCP

- Understand Ethernet, TCP, and HTTP headers.
    
- Be able to interpret Wireshark captures (window size, cookies, persistent connections).
    

Read:

- Chapter 2.2 (HTTP), p. 114–120
    
- Chapter 3.5.4 (TCP headers and segments), p. 263–267
    
- Wireshark lab references (found on textbook website)
    

---

#### 3. DNS (Domain Name System)

- What DNS does, hostname-to-IP mapping, caching, types of DNS records (A, MX, CNAME).
    
- DNS protocol and security threats (DNS poisoning, man-in-the-middle).
    

Read: Chapter 2.4, p. 150–166

## Important Port Numbers to Remember

|Port|Protocol|Description|
|---|---|---|
|20|TCP|FTP (Data Transfer)|
|21|TCP|FTP (Control)|
|22|TCP|SSH (Secure Shell)|
|23|TCP|Telnet|
|25|TCP|SMTP (Simple Mail Transfer)|
|53|UDP/TCP|DNS (Domain Name System)|
|67|UDP|DHCP (Server to Client)|
|68|UDP|DHCP (Client to Server)|
|69|UDP|TFTP (Trivial FTP)|
|80|TCP|HTTP|
|110|TCP|POP3 (Post Office Protocol v3)|
|143|TCP|IMAP (Internet Message Access)|
|161|UDP|SNMP (Simple Network Mgmt Prot)|


### TCP Reno Scenario Exercise

Assume the following conditions:

- MSS = 1000 bytes
- Initial `cwnd` = 12 MSS
- `ssthresh` = 16 MSS
- Sender has sent segments with sequence numbers: 1000, 2000, 3000, ..., 12000 (12 segments)
- Segment with SEQ = 4000 is lost
- Receiver continues to receive out-of-order segments beyond 4000

---

**Questions:**

1. What ACK number will the receiver send after receiving segments 1000, 2000, 3000, then missing 4000, but receiving 5000, 6000, 7000?

2. When the sender receives **three duplicate ACKs**, what action does it take immediately?

3. After fast retransmit, what happens to `ssthresh` and `cwnd`?

4. During fast recovery, the sender receives two more duplicate ACKs. How many new segments can it send immediately after these?

5. When the retransmitted segment (SEQ 4000) is finally acknowledged, what does the sender do with `cwnd` and which congestion control phase does it enter?

---

Give your answers with brief explanations!
1. The receiver will send ACK number 4000, causing duplicate acks since it has not received SEQ number 4000.
2. Since the `cwnd` starts at 12 MSS it increases to 15 after the first 3 packets. This means when the dup acks are received it is still in the slow start state.  When 3 DUP acks are detected it will go into the fast recovery state and immediatly retransmit the missing segment (fast retransmit). 
3.  The `sstresh` is set to `cwnd/2` and the `cwnd` is then set to `sstresh+3`
4. After the retransmit the `sstresh` has been set to 15/2 = 7 (integer) and the `cwnd` would be 7+3 = 10. 2 more because adittional acks.
5. When the retransmitted segment SEQ 4000 is acked, it means a new ACK has been sent which causes the state to go to congestion avoidance, and set the `cwnd = sstresh` and reset the dupackcount.



![[image.png]]

![[image-1.png]]
Fra 6 - 16, gjennomsnittlig congestion window size er $(42+32)*5/2=37$ 
37 sendinger per RTT
$37 MSS / 0.2s$ = 160*8

32+33+34+35+36+37+38+39+40+41+42