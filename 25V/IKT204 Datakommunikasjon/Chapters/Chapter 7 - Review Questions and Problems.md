**Exercise 1 (R1)**

1. What does it mean for a wireless network to be operating in “infrastructure mode”?
A wireless network operating in infrastructure mode as in opposed to **ad-hoc** mode means that the devices in the network connect to a centralized access point and not directly to each other. An example of a wireless network operating in infrastructure mode is a **SOHO** (small office/ home Office) network. All devices talk to an **AP** (access point), or multiple APs, the APs connect to the router which forwards the messages or the access point forwards the messages directly if there are two wireless devices connected to the same access points. Access points works as "wireless" switche sin this instance.
2. If the network is **not** in infrastructure mode, what mode of operation is it in, and what is the difference between that mode of operation and infrastructure mode?
When the network is **not** in infrastructure mode it is in **Ad-hoc** mode. The Ad-hoc mode is not centralized and does not require infrastructure to function. Instead of each device connecting to a access point, they rather communicate directly in between each other. An example of an Ad hoc network is Bluetooth, which is often called a wireless personal network. But other ad hoc networks also exists and are in continuous development.
**Exercise 2 (R3)**

What are the differences between the following types of wireless channel impairments: path loss, multipath propagation, interference from other sources?

**Exercise 3 (R4)**

As a mobile node gets farther and farther away from a base station, what are two actions that a base station could take to ensure that the loss probability of a transmitted frame does not increase?

**Exercise 4 (R5)**

Describe the role of the beacon frames in 802.11.

**Exercise 5 (R6)**

An access point periodically sends beacon frames. What is the content of the beacon frames?

**Exercise 6 (R9)**

What are the two main purposes of a CTS frame?

**Exercise 7**

After selecting the AP with which to associate, a wireless host sends an association request frame to the AP, and the AP responds with an association response frame. Once associated with an AP, the host will want to join the subnet (ref. IPv4 addressing of Section 4.3.2) to which the AP belongs. What does the host do next?

**Exercise 8**

Suppose an 802.11b station is configured to always reserve the channel with the RTS/CTS sequence. Suppose this station suddenly wants to transmit a datagram and all other stations are idle at this time.

1. As a function of SIFS and DIFS, and ignoring propagation delay and assuming no bit errors, derive an equation to calculate the time required to transmit a frame with payload and receive the acknowledgment.
2. Assume that the datagram has a size of 1400 bytes and that the transmission rate in the wireless network is 12 Mbps. What will the total transfer time be in this case? The answer is given in microseconds. See figure 7.13 in the textbook for the framing length of payload, [11 Frame Types and Formats](https://howiwifi.com/2020/07/13/802-11-frame-types-and-formats/)

[Lenker til en ekstern side.](https://howiwifi.com/2020/07/13/802-11-frame-types-and-formats/) for lengths of ACK, RTS and CTS frames, [DCF Interframe Space - Wikipedia](https://en.wikipedia.org/wiki/DCF_Interframe_Space) [Lenker til en ekstern side.](https://en.wikipedia.org/wiki/DCF_Interframe_Space) for the length of DIFS and [Short Interframe Space - Wikipedia](https://en.wikipedia.org/wiki/Short_Interframe_Space)1. [Lenker til en ekstern side.](https://en.wikipedia.org/wiki/Short_Interframe_Space) for the length of SIFS.

**Exercise 9 (P9)**

Power is a precious resource in mobile devices, and thus the 802.11 standard provides power-management capabilities that allow 802.11 nodes to minimize the amount of time that their sense, transmit, and receive functions and other circuitry need to be “on.” In 802.11, a node is able to explicitly alternate between sleep and wake states. Explain in brief how a node communicates with the AP to perform power management.