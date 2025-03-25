#  Exercise 1 (R3)

1. What does it mean for a wireless network to be operating in “infrastructure mode”?
A wireless network operating in infrastructure mode as in opposed to **ad-hoc** mode means that the devices in the network connect to a centralized access point and not directly to each other. An example of a wireless network operating in infrastructure mode is a **SOHO** (small office/ home Office) network. All devices talk to an **AP** (access point), or multiple APs, the APs connect to the router which forwards the messages or the access point forwards the messages directly if there are two wireless devices connected to the same access points. Access points works as "wireless" switche sin this instance.
2. If the network is **not** in infrastructure mode, what mode of operation is it in, and what is the difference between that mode of operation and infrastructure mode?
When the network is **not** in infrastructure mode it is in **Ad-hoc** mode. The Ad-hoc mode is not centralized and does not require infrastructure to function. Instead of each device connecting to a access point, they rather communicate directly in between each other. An example of an Ad hoc network is **Bluetooth**, which is often called a wireless personal network. A better and more applicable example of AD hoc networks are mesh networks. 

# Exercise 2 (R3)
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
# Exercise 3 (R4)

As a mobile node gets farther and farther away from a base station, what are two actions that a base station could take to ensure that the loss probability of a transmitted frame does not increase?

If the base station changes what **modulation** it uses. Generally for higher transmission rates the bit error rate will increase. For long distances with a lot of noise **BPSK** modulation can be used.
- **Adjusting the Modulation Scheme**: As you mentioned, switching to a more robust modulation scheme can help. For example, BPSK (Binary Phase Shift Keying) is more resilient to noise and interference compared to higher-order modulation schemes like QPSK or 16-QAM. Using a lower modulation scheme, like BPSK, reduces the likelihood of bit errors over long distances where the signal is weaker, although it sacrifices the data rate.
    
- **Increasing the Transmit Power**: The base station could increase its transmission power to compensate for the additional path loss as the mobile node moves farther away. However, this may be limited by power constraints and regulations. Increasing the power can help maintain a strong signal, reducing the probability of frame loss due to weak reception.
# Exercise 4 (R5)

Describe the role of the beacon frames in 802.11.
A beacon frame is sent by the an access points in IEEE 802.11, Wi-Fi, to allow devices to discover the network and confirm connectivity.
- **Network Discovery**: Beacon frames are periodically transmitted by access points (APs) to allow devices to discover available networks. When a device scans for Wi-Fi networks, it receives these beacon frames, which contain essential information about the AP, such as its **SSID (Service Set Identifier)**, supported data rates, and security protocols.
    
- **Synchronization**: Beacon frames also help synchronize the clocks of all devices in the network. The frames contain a **timestamp** field, allowing devices to synchronize their operations with the AP, ensuring proper timing for data transmission and reception.
    
- **Power Management**: Beacon frames provide power management information, allowing devices in the network to enter **sleep mode** while waiting for the next beacon frame. This helps conserve battery life on mobile devices.
    
- **Network Parameters**: In addition to basic information about the AP and network, beacon frames can also include other information such as supported channels, security settings (e.g., WPA2), and other configuration parameters necessary for a device to connect and communicate effectively with the network.
# Exercise 5 (R6)

An access point periodically sends beacon frames. What is the content of the beacon frames? 

The beacon frames contain information about the AP such as **SSID**, transmission  and receiving rates and what security protocols are in used. They also contain a **timestamp** field which allows devices to **synchronize** their operation with the access point. Additionally they provide power management information, allowing devices to enter sleep mode, while waiting for next beacon frame. Finally beacon frames include information about supported channel, security settings, for instance WPA2, and other parameters.
- **SSID (Service Set Identifier)**: Identifies the Wi-Fi network, allowing devices to recognize and connect to the appropriate network.
    
- **Timestamp**: A timestamp field that helps synchronize the device's clock with the access point, ensuring proper timing for communication and sleep cycles.
    
- **Supported Data Rates**: Lists the transmission and reception rates supported by the access point, which helps the device decide the most efficient rate for communication.
    
- **Security Protocols**: Information about the security settings, such as whether **WPA2**, **WPA3**, or **WEP** is used, allowing devices to authenticate and connect securely.
    
- **Channel Information**: The specific channel on which the access point operates, so devices can tune into the correct frequency.
    
- **Power Management Information**: Instructions for devices to enter **sleep mode** and conserve battery life, especially when they are not actively transmitting or receiving data.
    
- **Capabilities**: Information about the capabilities of the access point, such as whether it's supporting **802.11a/b/g/n/ac/ax** and other features like **quality of service (QoS)**.
    
- **Beacon Interval**: The time between successive beacon frames, which helps devices know when to wake up and listen for the next beacon.

# Exercise 6 (R9)

What are the two main purposes of a CTS frame?

A CTS frame stands for Clear to Send, and is used to avoid collisions in wireless networks. Wireless networks do not support the collision detection methods used in CSMA/CD, since they cannot (commonly) listen to data at the same time as transmitting since the strength of their transmitting signals would overpower the incoming signals. Therefore **RTS** and **CTS**, **Request to send** and **Clear to send** frames are used. RTS frames are very short and does not take up a lot of time, if the device receives a CTS it will send its pending frame in its entirety, which can be quite long.

- **Collision Avoidance**: The primary purpose of the CTS frame is to avoid collisions in a wireless network. Since devices in wireless networks cannot use **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) due to the **hidden node problem** (where devices may not be able to sense each other's signals), RTS and CTS frames are used as part of a **collision avoidance** mechanism. When a device wants to transmit, it first sends an **RTS** frame, and if the receiver is clear to accept the data, it responds with a **CTS** frame. This tells other devices in the network that the channel is about to be occupied and they should defer their transmissions, preventing collisions.
    
- **Reservation of the Channel**: The CTS frame serves as a reservation for the transmission channel. When the device that issued the **RTS** frame receives the **CTS** frame, it confirms that the channel is clear, and the sender can proceed with its transmission. The CTS frame also notifies nearby devices to **hold off** on transmitting for a specific amount of time, allowing the sender to transmit without interference.
# Exercise 7

After selecting the AP with which to associate, a wireless host sends an association request frame to the AP, and the AP responds with an association response frame. Once associated with an AP, the host will want to join the subnet (ref. IPv4 addressing of Section 4.3.2) to which the AP belongs. What does the host do next? 

The host will broadcast an DHCP request to the AP, which the AP will forward to the DHCP server on the network. The DHCP server will respond with IP information the host can use on the network. The host will then accept its given IP with an acknowledgement, and it has now joined the subnet. 

- **DHCP Request**: After associating with the AP, the wireless host needs to obtain an IP address to join the subnet. The host sends a **DHCP Discover** message to the **AP** (or broadcast to the network if directly connected to the same subnet) requesting an IP address.
    
- **DHCP Forwarding by AP**: If the AP is configured as a **DHCP relay agent**, it will forward the **DHCP Discover** message to the **DHCP server** on the network. In some cases, the AP might also act as a DHCP server, depending on its configuration.
    
- **DHCP Offer**: The **DHCP server** will respond with a **DHCP Offer** message, which contains the IP address and other network configuration details (e.g., subnet mask, default gateway, DNS servers).
    
- **DHCP Request**: The host receives the DHCP Offer and sends a **DHCP Request** back to the DHCP server to accept the offered IP address.
    
- **DHCP Acknowledgement**: The DHCP server acknowledges the host's request with a **DHCP Acknowledgement** message, confirming the IP address assignment.
    
- **Joining the Subnet**: Once the host receives the **DHCP Acknowledgement**, it now has a valid IP address and can fully participate in the subnet, including communication with other devices in the same network.
# Exercise 8

Suppose an 802.11b station is configured to always reserve the channel with the RTS/CTS sequence. Suppose this station suddenly wants to transmit a datagram and all other stations are idle at this time.

1. As a function of **SIFS** and **DIFS**, **and** ignoring propagation delay and assuming no bit errors, derive an equation to calculate the time required to transmit a frame with payload and receive the acknowledgment.

The station first waits one *DIFS* (Distributed Inter Frame space) and then proceeds to send its RTS frame, if it receives a CTS frame it then proceeds to send its frame. After the frame is sent and received, the receiver waits one SIFS, (Short *inter* frame spacing) sends the acknowledgement, then the initial station will receive the packet. If we ignore propagation delay and processing delay, we only need to account for DIFS, DIFS, and transmission delays.

Time from send to receive ACK: $$
\begin{aligned}
DIFS + D_{trans} + SIFS + D_{trans} &= DIFS + SIFS + 2D_{trans} \\
D_{trans} &= \frac{L}{R}
\end{aligned}
$$
  
Therefore our formula is
$$DIFS + SIFS + \text{2L/R}$$ Where $DIFS$ is the distributed interframe space and $SIFS$ is the short inter frame spacing and $L$ is size of the frame, and $R$ is the average transmitting speed
 

2. Assume that the datagram has a size of 1400 bytes and that the transmission rate in the wireless network is 12 Mbps. What will the total transfer time be in this case? The answer is given in microseconds. See figure 7.13 in the textbook for the framing length of payload, [11 Frame Types and Formats](https://howiwifi.com/2020/07/13/802-11-frame-types-and-formats/)
$(50+10)*10^{-6} + 2*\left( \frac{8*1400}{12\cdot10^6} \right)=933.33 \cdot10^{-6}s=933\mu s$
[Lenker til en ekstern side.](https://howiwifi.com/2020/07/13/802-11-frame-types-and-formats/) for lengths of ACK, RTS and CTS frames, [DCF Interframe Space - Wikipedia](https://en.wikipedia.org/wiki/DCF_Interframe_Space) [Lenker til en ekstern side.](https://en.wikipedia.org/wiki/DCF_Interframe_Space) for the length of DIFS and [Short Interframe Space - Wikipedia](https://en.wikipedia.org/wiki/Short_Interframe_Space)1. [Lenker til en ekstern side.](https://en.wikipedia.org/wiki/Short_Interframe_Space) for the length of SIFS.

# Exercise 9 (P9)

Power is a precious resource in mobile devices, and thus the 802.11 standard provides power-management capabilities that allow 802.11 nodes to minimize the amount of time that their sense, transmit, and receive functions and other circuitry need to be “on.” In 802.11, a node is able to explicitly alternate between sleep and wake states. Explain in brief how a node communicates with the AP to perform power management.