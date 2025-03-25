#  

1. What does it mean for a wireless network to be operating in “infrastructure mode”?
A wireless network operating in infrastructure mode as in opposed to **ad-hoc** mode means that the devices in the network connect to a centralized access point and not directly to each other. An example of a wireless network operating in infrastructure mode is a **SOHO** (small office/ home Office) network. All devices talk to an **AP** (access point), or multiple APs, the APs connect to the router which forwards the messages or the access point forwards the messages directly if there are two wireless devices connected to the same access points. Access points works as "wireless" switche sin this instance.
2. If the network is **not** in infrastructure mode, what mode of operation is it in, and what is the difference between that mode of operation and infrastructure mode?
When the network is **not** in infrastructure mode it is in **Ad-hoc** mode. The Ad-hoc mode is not centralized and does not require infrastructure to function. Instead of each device connecting to a access point, they rather communicate directly in between each other. An example of an Ad hoc network is **Bluetooth**, which is often called a wireless personal network. A better and more applicable example of AD hoc networks are mesh networks. 

# **Exercise 2 (R3)**
What are the differences between the following types of wireless channel impairments: **path loss**, **multipath propagation**, **interference** from other sources?
Path loss describes the the fact tat electromagnetic radiation attenuates as it passes through matter (mountains, walls) and even in free space the signal will still disperse, which in turn results in decreased signal strength, whereas multipath propagation refers to the signal reflecting off objects or the ground leading to the same signal being received at different times, blurring the the received signal. Interference is an effect of electromagnetic waves, waves are additive which means they will disrupt each other and potentially cancel each other out. If two waves are in different frequency bands they still can be read separately, but it requires consideration when choosing frequencies, to efficiently apply FDM, and with a lot of concurrent signals TDM might be needed.

Your explanation of the three impairments is solid, but here are a few suggestions to expand and clarify the details:

1. **Path Loss**:
    
    - You can mention that **path loss** is typically modeled using a formula like the **Friis transmission equation**, which quantifies the attenuation of a signal based on distance and frequency. It would also be helpful to highlight that path loss is often dependent on the **environment** (e.g., urban areas, rural areas, indoor vs. outdoor). You could also mention **Free Space Path Loss (FSPL)** as a specific case for line-of-sight communication.
        
2. **Multipath Propagation**:
    
    - It's good to mention that **multipath** occurs because the signal can take different paths to reach the receiver, either via reflection, diffraction, or scattering. This results in **interference** at the receiver because multiple versions of the same signal arrive at different times, which can cause constructive or destructive interference, leading to a phenomenon known as **fading**.
        
    - To improve the explanation, you could mention **selective fading** (where certain frequencies are more affected than others) and how this might impact communication, especially for high data rates or **wideband** signals.
        
    - In addition, you can briefly touch on how **diversity techniques** like **MIMO (Multiple Input Multiple Output)** are used to mitigate multipath effects.
        
3. **Interference**:
    
    - Interference could be elaborated further by categorizing it into **co-channel interference** (from other users on the same frequency) and **adjacent channel interference** (from nearby frequencies). You could also mention **systematic interference** (e.g., from hardware or environmental noise) vs. **random interference** (e.g., from other devices).
        
    - Also, note how **interference** can degrade signal quality and **bit error rates** (BER), leading to the need for techniques such as **error correction** and **spread spectrum** (e.g., **CDMA**) to minimize the effects of interference.
# **Exercise 3 (R4)**

As a mobile node gets farther and farther away from a base station, what are two actions that a base station could take to ensure that the loss probability of a transmitted frame does not increase?

If the base station changes what **modulation** it uses. Generally for higher transmission rates the bit error rate will increase. For long distances with a lot of noise **BPSK** modulation can be used.
- **Adjusting the Modulation Scheme**: As you mentioned, switching to a more robust modulation scheme can help. For example, BPSK (Binary Phase Shift Keying) is more resilient to noise and interference compared to higher-order modulation schemes like QPSK or 16-QAM. Using a lower modulation scheme, like BPSK, reduces the likelihood of bit errors over long distances where the signal is weaker, although it sacrifices the data rate.
    
- **Increasing the Transmit Power**: The base station could increase its transmission power to compensate for the additional path loss as the mobile node moves farther away. However, this may be limited by power constraints and regulations. Increasing the power can help maintain a strong signal, reducing the probability of frame loss due to weak reception.
# **Exercise 4 (R5)**

Describe the role of the beacon frames in 802.11.
A beacon frame is sent by the an access points in IEEE 802.11, Wi-Fi, to allow devices to discover the network and confirm connectivity.
- **Network Discovery**: Beacon frames are periodically transmitted by access points (APs) to allow devices to discover available networks. When a device scans for Wi-Fi networks, it receives these beacon frames, which contain essential information about the AP, such as its **SSID (Service Set Identifier)**, supported data rates, and security protocols.
    
- **Synchronization**: Beacon frames also help synchronize the clocks of all devices in the network. The frames contain a **timestamp** field, allowing devices to synchronize their operations with the AP, ensuring proper timing for data transmission and reception.
    
- **Power Management**: Beacon frames provide power management information, allowing devices in the network to enter **sleep mode** while waiting for the next beacon frame. This helps conserve battery life on mobile devices.
    
- **Network Parameters**: In addition to basic information about the AP and network, beacon frames can also include other information such as supported channels, security settings (e.g., WPA2), and other configuration parameters necessary for a device to connect and communicate effectively with the network.
# **Exercise 5 (R6)**

An access point periodically sends beacon frames. What is the content of the beacon frames? 

[2] The beacon frames contain information about the AP such as **SSID**, transmission  and receiving rates and what security protocols are in used. They also contain a **timestamp** field which allows devices to **synchronize** their operation with the access point. Additionally they provide power management information, allowing devices to enter sleep mode, while waiting for next beacon frame. Finally beacon frames include information about supported channel, security settings, for instance WPA2, and other parameters.

# **Exercise 6 (R9)**

What are the two main purposes of a CTS frame?

# **Exercise 7**

After selecting the AP with which to associate, a wireless host sends an association request frame to the AP, and the AP responds with an association response frame. Once associated with an AP, the host will want to join the subnet (ref. IPv4 addressing of Section 4.3.2) to which the AP belongs. What does the host do next?

# **Exercise 8**

Suppose an 802.11b station is configured to always reserve the channel with the RTS/CTS sequence. Suppose this station suddenly wants to transmit a datagram and all other stations are idle at this time.

1. As a function of SIFS and DIFS, and ignoring propagation delay and assuming no bit errors, derive an equation to calculate the time required to transmit a frame with payload and receive the acknowledgment.
2. Assume that the datagram has a size of 1400 bytes and that the transmission rate in the wireless network is 12 Mbps. What will the total transfer time be in this case? The answer is given in microseconds. See figure 7.13 in the textbook for the framing length of payload, [11 Frame Types and Formats](https://howiwifi.com/2020/07/13/802-11-frame-types-and-formats/)

[Lenker til en ekstern side.](https://howiwifi.com/2020/07/13/802-11-frame-types-and-formats/) for lengths of ACK, RTS and CTS frames, [DCF Interframe Space - Wikipedia](https://en.wikipedia.org/wiki/DCF_Interframe_Space) [Lenker til en ekstern side.](https://en.wikipedia.org/wiki/DCF_Interframe_Space) for the length of DIFS and [Short Interframe Space - Wikipedia](https://en.wikipedia.org/wiki/Short_Interframe_Space)1. [Lenker til en ekstern side.](https://en.wikipedia.org/wiki/Short_Interframe_Space) for the length of SIFS.

# **Exercise 9 (P9)**

Power is a precious resource in mobile devices, and thus the 802.11 standard provides power-management capabilities that allow 802.11 nodes to minimize the amount of time that their sense, transmit, and receive functions and other circuitry need to be “on.” In 802.11, a node is able to explicitly alternate between sleep and wake states. Explain in brief how a node communicates with the AP to perform power management.