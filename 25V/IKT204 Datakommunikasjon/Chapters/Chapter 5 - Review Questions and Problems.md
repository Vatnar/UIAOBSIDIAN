**Exercise 1 (R3)**

Compare and contrast the properties of a centralized (global) and a distributed _routing **algorithm**_. Give an example of a _routing **protocol**_ that takes a centralized and a decentralized approach.

A centralized or global routing algorithm requires the full topology of the network. The shortest path algorithm can be run either at one site (centralized controller) or replicated for every routing component. This way of doing routing requires information about link costs or link state hence it often being called link-state algorithms (LS). A centralized routing algorithm is often easier to implement than a distributed routing algorithm.  SDN with OpenFlow is centralized.

A decentralized algorithm, regards calculating paths iterative distributed manner. None of the routers contain the entire network topology. Each router knows the cost of its directly attached links, then through iteration and exchange of information with neighbours it gradually calculates least cost path. Example is distance-vector algorithm.  , RIP or BGP protocols use distance vector

Centralized algorithm guarantees the optimal paths, easier to debug and manage, and converges faster on change in topology. However its very expensive to collect and process all the routing information when the network grows, and it needs to constantly send updates. Additionally given that the algorithm is centralized there will be a single point of failure. A decentralized routing algorithm is more scalable, can still work even if routers fail, and doesnt need to recalculate everything if there are small changes. However it takes longer to react to changes in the topology, and there is a possibility of loops. Since there is no centralized part with the full topology the optimal route cannot be guaranteed. 

Regarding time the centralized algorithms often have around a O(n^2) or O(nlogn) (priority cqueues) based on implementation. Decentralised algorithsm run n times.
**Exercise 2 (P1, P2 variant)**

Consider the following network.

![[image-a9aeb3f9-4eb4-46e6-94ef-119e269187bc.png]]

1. Use Dijkstra’s shortest-path algorithm to compute the shortest path from **node** **x** to all network nodes. Show how the algorithm works by computing a table below.
   ![[Pasted image 20250304132319.png]]

2. Use Dijkstra’s shortest-path algorithm to compute the shortest path from **node** **t** to all network nodes.
![[Pasted image 20250304133506.png]]


**Exercise 3 (R7)**

Why are different inter-AS and intra-AS protocols used in the Internet?
Intra-AS intra-autonomous systems are often a lot smaller than inter-as which connects autonomous systems. In a smaller intra-as a centralized routing algorithm could work fine since its finds the optimal path and is not too big so that it takes to long or too much space. For inter-as it is often too big which leads to the use of distributed algorithms being better. 

Intra-as often use OSPF (Open Shortest Path First) and RIP Routing information protocol
Inter-as often use BGP border gateway protocol
**Exercise 4 (R8)**

When an OSPF router sends its link state information, it is sent only to those routers that are directly attached neighbors or to all routers in the same autonomous system? Justify your answer. The link state information is only sent to the neigbhours during OSPF but the neighbours will propegate (parrot) the information onwards to every connection except from the one who sent it. This is sometimes called flooding.

**Exercise 5 (R10)**

Define and contrast the following terms: subnet, prefix, and BGP route.

A subnet is a network that has been dividided into further smaller groups of networks. For instance a network that contains Ips from 193.32.42.0 to 193.32.42.255 can "borrow" some host bits, and add to the network bits so different subnets can be specified, this will then be called the subnet mask. When using dotted decimal notation it is often denoted using 0-255.0-255.0-255.0\(bitcount). Borrowing host bits to the network gives the advantage of being able to have more networks in the same block of IP addresses at the cost of each subnetwork not being able to distribute as many ip addresses to hosts.

Prefix is something that is common between for instance an IP address and a filter. In a NAT network address translator a prefix is used to differentiate what IP addresses should go to which interface based on the longest common prefix.

BGP is border gateway protocol and defines rules for traffic within the AS IBGP and between ASes EGBP (external and internal).

These concepts work in conjunction to make hierarchical network structure function.

**Exercise 6 (R11)**

How does BGP use the NEXT-HOP attribute? How does it use the AS-PATH attribute?

**Exercise 7 (P14)**

Consider the network shown below. Suppose that AS1, AS2, AS3 and AS4 are running OSPF for their intra-AS routing protocol. Suppose eBGP and iBGP are used for the inter-AS routing protocol. Initially suppose there is no physical link between AS2 and AS4.

1. Router **3c** learns about prefix **_x_** from which routing protocol: OSPF, eBGP, or iBGP?
2. Router **3a** learns about **_x_** from which routing protocol?
3. Router **1c** learns about **_x_** from which routing protocol?
4. Router **1d** learns about **_x_** from which routing protocol?
5. Once router **1d** learns about prefix **_x_**, it will put an entry _(**x,I**)_ in its forwarding table, where **_I_** is either interface **_I1_** or **_I2_**. Will **_I_** be equal to **_I1_** or **_I2_** ? Explain why in one sentence.
6. Now suppose that a link between AS2 and AS4 (shown by the dotted line) is established, and that router **1d** learns that prefix **_x_** is accessible via AS2 as well as via AS3. Will **_I_** be set to **_I1_** or **_I2_** ? Explain why in one sentence.

![[image-0d3a5714-a1f5-48d0-89b7-acb675bfbe4f.png]]
