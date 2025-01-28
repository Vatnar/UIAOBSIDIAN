```table-of-contents
title: Contents
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
Nuts and bolts:
![[some pieces of the Internet.jpg]]
**Distributed applications**
Multiple end systems that exchange data. Internet application run on end systen, not in the packet switches in the <span style="color:rgb(255, 0, 0)">network core</span>. 
I.e you write your applications in programming languages that run on end systems. End systems attached to the internet provide a <span style="color:rgb(255, 0, 0)">socket interface</span> that specifes how a program on a end system asks the internet infrastructure to deliver data to a destination program on another end system. The socket interface is rules that the sneding program must follow to deliver the data. More in [[Chapter 2]]. Can be compared to a postal service, name is needed, address zip code, seal, stamp and so on. Official mailbox. Postal service interface. 

# Protocols
## Human protocols
A protocol can be compared to human protocol e.g: "Hi, Hi, Whats the time, 2.0". Starts with offering a greeting to initiate communication. Then it returns the greeting. Returning the greeting signals that sender can continue. If it rather says dont bother me or something they are unwilling or inable to communicate. *specific messages we send, and specific actions we take in response to teh received reply messages or other events*. If people run different protocols they cannot interoperate. Same is true in computer networking.  ^81cfcc
## Network protocols
Similar to human equivcalent but the entites exchangging messages and taking actions are hardware or software components of some device. All internet activity invloving two or more communicating entites is governed by a protocol. E.g hardware-implemented protcols in two physically connected computerrss conmtrol the flow of bits on the wire; congestion control protocols ion end system control the rate at which packets are transmitted between sender and receiving; protocols in routers dfeteermine a packes path, . Example of network protocol is HTTP, retrieve a web page. 

*A protocol defines the format and the order of messages exchanged between two or more communicating entities, as well as the actions taken on the transmission
and/or receipt of a message or other event*

# Network edge
End systems or hosts. Can be devided into clients and servcers. Network physically connecting end system to the first router on a path from the end system to any other distant end system is called the <span style="color:rgb(255, 0, 0)">access network</span>. 
![[accessnetworks.jpg]]
## DSL Digital Subscriber Line and cable
DSL from the same local telephone company that provides wired local phone access. WHen DSL is used, a customers telco is also its ISP. DSLAM (Digitial subscriber line access multiplexer.). The DSL modem takes digital data and transalte it to high frequency tones for transmission over telephone wirtes to the CO; the anolog signals from many such houses are translated back into digital format at the DSLAM.

Telephone line carries:
- A high-speed downstream channel, in the 50 kHz to 1 MHz band
• A medium-speed upstream channel, in the 4 kHz to 50 kHz band
• An ordinary two-way telephone channel, in the 0 to 4 kHz band

This makes the DSL link appear as if there were three seperate links, so that a telephone call anda an internet connection can share the DSL link at the same time.

### FDM og TDM
Frequency Division multiplexing (FDM)
- Optisk, electromagnetisk frekvenser delt inn i narrow frekvensbånd. Velger ett bånd hvor det blir overført forbindelse. Bånd eller kanal. band orChannel.
- Hvert opprop call allokert sit eget bånd, kan overføre mded max rate av båndet.
- FM radio.

Time Division Multiplexing (TDM)
- Time delt til plasser.
- Hvert opprop er allokert periodiske plasser og kan overføre på max rate brede frekvens bånd kun under sin tid. Round robin.
![[Pasted image 20250120105149.png]]
GCM mobil, har man både tidsdelt, men samtidig som det hopper på ulike frekvensbånd.
Linjesvitsjing brukes ikke på internett, da bruker man pakkesvitsjing. Eneste kan være visse enheter. Kan være på edge.

<span style="color:rgb(255, 0, 0)">Cable internet access</span> makes use of the cable television companys existing cable infrastructure. Same company as its cable television. Connects to neighborhood junctions, coaxial cables to reach individual houses. Fiber and coaxial cable are employed in this system, so its often called hybrid fiber coax (HFC). Cable internet requires cable modems. An external device connects to a home pc through an ethernet port. [[chapter 6]]. At cable end the cable modem termination system (CMTS) serves a similar function to DSLAM. turning the anlog signal sent from cable modems in many downstream homes back into digital format. It divides the HFC netwriok into downstream and upstream channel. Often assymetric access. Downstream having a higher aallocated transmission rate. DOCSIS 2.0 and 3.0 standards. As in the case of DSL networks, the
maximum achievable rate may not be realized due to lower contracted data rates
or media impairments.

Cable internet is shared broadcast medium, meaning that if multiple users loads a video ile it will be shared. DSL and cable are the majority of broadbands, but a newer tech is fiber to the home (FTTH). Concept is simple, provide an optical fiber path from the CO CENTRAL OFFICE. FTTH can potentially oprovide access rates in the gigabits per second range. Server competing techs. Simples optical distrubition netowrk is direct fiber, with one fiber per home leaving the CO. more commonly its shared by many homes< when it gets close to the homes its split into many. 

**Splitting**: AONS and PONS, active oiptical networks and passive optical networsk. AON is essentiallly switched  ethernet. 
![[FTTHinternetaccess.jpg]]
Figure 1.7 shows FTTH discuss PON. Each home has a optical network terminator ONT> which is connected to dedicated optical fiber toa  neighborhood splitter. Combines into a single shared optical fiber. Which connnects to a OLT optical line terminator in the telcos CO. the OLT provides conversion etween optical and electrical signals, connects to the internet via telco router. At home users conmnect a home router typically wireless to the ONT and access the internet vi this home router. IN the pon architecture all poackats sent from OLT to the splitter are replicated at the splitter.

In additaion to DSL cable and FTTH 5G fixed wireless is beginning to be deployed. 5G uses beam forming technololgy, data is sent wirelessly from a provider base station to the a modem in the home. A wifi wireless router is connected to the moden or bundled toegher, similar to how a wifi wireless router is connected toa cable or DSL modem. CHAPTER 7. 
## Ethernet and Wifi
On coproprate and campsses and many home ssettings a local area network LAN is used to connect end system to edge router. Ethernet is the most prelevant access techonology. 
![[ethernetinternettaccess.jpg]]
Using TP wires, twisted pair copper wire, to connect to a ethernet switch. CHAPTER 6. The ethernet switch or a network of such interconnectedc switches is in turn connected into the larger internet. With ethernet  access user typically have 100 Mbps to tens of Gbps access to the ethernet switch, wheas servers may have 1 Gbps to 10 GBpos access. Many people are increasilny using  internet form latpop and other things. In a wireless LAN setting, wireless user transmit/recieve packets to/from an access point that is connnected into the network. most likely using wired ethernet. Which in turn is connected to the internet. A wireless lan user musty typically be within a few tens of meters to the access point. Wireless LAN WLAN. In this sertting  wireless users transmit and recieve packets to and from an access point connected to the local network most likely internet wiich is connnected to wired internet. Many homes connect residential acces cagble or dsl or ftth with wireless LAN to create powerful home networks. Roaming laptop, multiple connected aplpiiacnes, wired pc; a base station the wireless access point which communcates with the wirelss PC and other wireless devices in the home, and a home router that connects the wireless access point an any other wired home devices to the internet. 

### 1.2.2 Physical Media

This section provides an overview of the various physical media used for internet transmission, highlighting their importance in network access technologies. It describes how bits travel through a series of transmitter-receiver pairs, propagating electromagnetic waves or optical pulses across different media types, such as twisted-pair copper wire, coaxial cable, and fiber optics. Guided media, like fiber-optic and coaxial cables, require a solid medium for wave propagation, while unguided media, such as terrestrial and satellite radio channels, utilize the atmosphere for signal transmission. The cost of physical links often pales in comparison to installation costs, prompting the installation of multiple media types for future adaptability. Overall, twisted-pair copper wire remains a dominant choice for LANs and residential access, while fiber optics excel in long-distance communication due to their high bit rates and low interference.


# Network Core
![[networkcore.jpg]]

## Packet Switching
End systems exchange <span style="color:rgb(255, 0, 0)">messages</span> with each other. Messages can contain anything the application designer wants. Messages may perform a control function (for example, the "Hi" maessages in our handshaking example) or can contain data. To send a message from a source end system to a destination, the source breaks long messages into smaller chunks of data known as <span style="color:rgb(255, 0, 0)">packets</span>. Between source and destination, each packet travels through communication links and <span style="color:rgb(255, 0, 0)">packet switches</span> ( routers and link-layer switches). Packets are transmitted over each communication link at a rate equal to the full transmission rate of the link. So if a source end system or a packet switch is sending a packet of $L$ gits over a link with transmission rate $R$ $bits/sec$, then the time to transmit the packet is $L/R$ seconds. 
### Store-and-Forward Transmission / Transmission delay
Most packet switches use store and forward transmission from inputs to links. The switch must then receive the entire packet before it can begin transmitting the packet to the outbound link. The receiving switch receives at the same time as the sender sends, thus the the time for transmission can be calculated by looking at the amount of hops between switches. So for instance for one switch between 2 computers it would be $2$ $hops\times  L/R$ = $2L/R$ transmission delay.
### Queuing Delays and Packet Loss
For each attached links to a packet switch the switch has an <span style="color:rgb(255, 0, 0)">output buffer</span> or output queue, which stores packets that the router is about to send into that link. If the arriving packet needs to be transmitted onto a link but the links busy the arriving packet must wait in the output buffer. Thus in addition to the store and forward delays packets suffer output buffere <span style="color:rgb(255, 0, 0)">queueing delays</span>. These delays are variable  and depend on the congestion/saturation/metning in the network.
![[Packet switching.jpg]]
If the buffer is completely full with other packets <span style="color:rgb(255, 0, 0)">packet loss</span> will occur. Either for the arriving packet, or one of the already-queued packets will be dropper.

### Forwarding Tables and Routing Protocols
How does a router determine which link it should forward a packet onto?
Different ways for different types of computer networks.
#### Internet
Every end system has a IP Address. Source end systems includes the destination's IP address in the packet's header. Address has a hierearchial structure. When a packet arrives, the router examines a portion of the packet's destination address and forwardds the packet to an adjacent router. Each router has a *forwarding table* that maps destination addresses (or portions of the destination addresses) to that router's outbound links. It searches its forwarding table, using this address, to find the appropriate outbound link. The router then directs the packet to this outbound link.

Analogous to a car driver not using maps but instead asking for directions and being pointed in the direction. 

Router uses a packet's destination address to index a forwarding table and determine the apporpriate outbound link. But how does forwarding tables get set? Are they configured by hand in each and every router, or does it be automated? More about that in [[Chapter 5]]. Internet has a number of special *routing protocols* that are used to automatically set the forwarding tables.  They may for example determine the shortest path from each router to each destination and use the shortest path results to configre the forwarding tables in the routers.

## Circuit Switching
Resources needed along a path is reserved for the duration of the communication session between end systems. On the contrary in packet switching networks they are multiplexed.

Telephone networks are example of circuit-switched networks. Network established connection between sender and receiver. Bona fide connection switches mantains state. This is called circuit When the network establishes the ciruit, it also reserves a constant transmission rate in the networks links (representing a given transmision rate has been reserved for this sender-to-receiver connection, the sender can transfer the data to the receiver at the garenteed constant rate. 
![[2025.01.28.11.10.18.877 firefox.jpg]]
### Multiplexing in Circuit-Switched Networks
ITs either multiplexed with frequency-division multiplexing  (FDM) or time-division multiplexing (TDM)[[#FDM og TDM]].  

## Delay, Loss, and Throughput in Packet-switched networks
### Delay
Most important delays are *Nodal processing delay*, *queuing delay*, *transmission delay*, and *propegation delay*; together, these delay accumulate to give a *total nodal delay*. Performance is greatly affected by network delays. 
![[2025.01.28.11.17.21.845 firefox.jpg]]
#### Processing delay
The time required to examine the packet's header and determine where to direct the packet is part of the processing delay. The processing delay can also include factors such as time needed to check for bit-level errors in the packet that occured in transmitting the packet's bits from the upstream node to router A. Processing delays in high-speed routeres are typicalle on the order of microsecojnds or less. After this nodal processing, the router directs the packet to the queue that precedes the link to royuter B. IN chapter 4 we will see more about this [[Chapter 4]]. 
#### Queuing Delay
Packet experiences a queuing delay  as it waitas to be transmitted onto the link. Queueing delay for a packet will depend on the number of earlier-arriving packets that are queued and waiting for transmission. If its empty then it will be zero, if the traffic is heavy, the queuing delay will be long. Can be in the order of microeconds to milliseconds.
#### Transmission Delay
Assume FCFS, our packet can be transmitted onlty after all the packets that have arrived before it have been transmitted. Denote the lenght of the packet by $L$ bits, and denote the transmission rate of the link from router A to router B by $R$ $bits/sec$. For example, for a $10$ $Mbps$ Ethernet link, the rate is $R=10$ $Mbps$; for a $100$ $Mbps$ Ethernet link the rate is $R = 100$. The transmission delay is $L/R$. This is the amount of time requrired to push (that is transmit) all of th epackets bits into the link. Transmission delays are typically on the order of microseconds to milliseconds.

#### Propagation delay
When it gets to the link its needs to propagate to router B. The time required to go from the beginning of the link to Router B is the propagation delay. It propagates at the propagataion speed of the link. That depends on the physical medium of the links (i.e fiber, TP wire, coax). Usually from $2 \cdot 10^8 m/s$ to $3 \cdot 10^8m/s$ almost speed of light. THe delay is the distance between the routers divided by the speed. So d/s. 

### Queuing Delay and Packet Loss.
Let $a$ denote the avarage rate at which packets arrive at the queue (packets/sec). $R$ is transmission rate, and $L$ is the lenght of packet. Avarage rate of bits arrive at the queue is $La\;bits/sec$ . The ratio $La/R$ 