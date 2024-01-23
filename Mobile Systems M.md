Notes for the course [Mobile Systems M](https://www.unibo.it/it/didattica/insegnamenti/insegnamento/2022/468026) held by professor [Paolo Bellavista](https://www.unibo.it/sitoweb/paolo.bellavista), at Alma Mater Studiorum - University of Bologna. Edited by [Michele Righi](https://github.com/mikyll).

## Index

## Chapter 0 - Introduction

IP addresses assignment: IANA (Internet Assigned Numbers Authority) is responsible for thhe global coordination of IP addresses allocations.

Standard procedure: IANA -> RIRs (Regional Internet Registries) -> ISP (Internet Service Providers) -> my device that needs an IP address.

However, there is the concept of "Non-coordinated IP addressing spaces": IP addresses allocations that are not centrally managed or coordinated by a central standard authority (IANA for the Internet).

==**Bandwidth** (measured in multiple of bps - bits per second): *theoretical* maximum capacity of a network or communication channel;
**Throughput** (measured in multiple of bps): *actual* amount of data thata can be successfully transmitted over a network or communication channel, in real-world conditions.==

Mobile devices are expected to move in most cases, and that has many consequences.


## Chapter 1 - Wireless (ISO/OSI Layer 2)

When dealing with mobile systems, the nodes are almost always connected through a wireless connectivity medium.

One of the ==main differencies from the wired connections==, is that in wired ones (e.g. Ethernet) the signal cannot be lost before being received, due to its distance (at least in local networks, it can happen in bigger ones). Generally speaking, that's due to the fact that after X length, there's something that regenerates the signal.

What's for sure, is that in cabled connections, there are NEVER propagation problems.
On the contrary, in wireless communication, you'll always (more or less) have propagation problems: the signal power decreases in space moving further away, at least directly, since you can always repeat the signal.

When you're too far from an AP (Access Point) you'll not be able to associate to it anymore and you have to move near or change it.

### Wireless Propagation Models
The signal decreases while traveling along distances, and that physical behaviour is described by ==Maxwell's laws==.

Wireless propagation models are mathematical representations used to describe how radio frequency (RF) ==signals travel and **attenuate as they propagate** through air and other mediums==. Those help researchers and engineers understand and predict the behaviour of wireless communication systems.

#### Signal Propagation Losses
There are some kind of losses in power received (Pr) by the receiver, from the transmitter. In fact, two important concepts in **wireless propagation** are the following, related to Maxwell's equations:
- ==**Free-space loss**== (~path loss), `Pr(d) ~ Pt * Gt * Gr (λ / 4 Π d)²
	is the reduction in signal strenght, as a radio wave travels through free space **without any obstacles** or reflections. 2 times inversely proportional to distance (`d²`).
	**NB**: it increases with distance and frequency 
- ==**Plane earth loss**== (~groud reflection loss), `Pr(d) ~ Pt * Gt * Gr (ht * hr / d² )²
	is **due to Earth's curvature** and affects signals that travel along its surface. Earth is a "curve reflector". 4 times inversely proportional to distance (`d⁴`).
	**NB**: it impacts the coverage area of a wireless system, especially when direct line-of-sight communication is not possible.

==In real life scenarios, the signal tends to be a fluctuation influenced by both of these two laws== (which can be thought of as 2 straight lines):
![[signal_propagation.png]]

#### Channel Fading Models
The signal is also ==influenced by physical phenomena== that affects its ==propagation==. The most relevant and dominant ones are shadowing, Raileigh fading, and frequency-selective fading.

NB: large-scale VS small-scale fading. Slow fading implies that the changes in signal strength occur over larger distances or longer periods, making them more predictable and manageable.

![[channel_fading.png]]

==The combination of all these effects produces the so called `Pr`== which is the Power Received, which usually fluctuates depending on the distance.
##### Shadowing
==Occurs when the signal encounters **obstacles** along its path, causing **long-term strenght variations**.==
Also called slow-fading, refers to the long-term variations in signal strenght caused by obstacles and environmental features in the propagation path. It's a type of large-scale or "slow" fading phenomenon that affects the received signal strength, leading to signal fluctuations over distance and time. It's caused by the partial/total absorption and partia/total reflection due to objects (trees, buildings, mobile vehicles, ...) and causes a decrease of the received power strength in a wide spectrum of frequencies. This kind of fading can be calculated for smaller objects, but usually, under a mathematical point of view, we tend to refer to pdf (probability distribution functions): considerations about shadowing usually lead to approximations of the probability of being in the coverage area of the signal.
##### Multipath Rayleigh Fading
==Occurs when the signal reaches the receiver through **multiple paths**, causing **rapid oscillations** in signal strength (constructive/destructive interferences).==
It's a type of fast-fading/small-scale fading. When traveling, usually an electromagnetic signal never go through one single path, but gets scattered many times and what is received is the sum of the "bits" of signal that reaches it, coming from multiple different paths.
##### Frequency-Selective Fading
==**Different frequency** components of the signal experience varying levels of fading, causing **frequency-dependent strength variations**.==
It's a kind of fading similiar to shadowing, that happens when the signal travels through a channel with varying characteristics across its frequency spectrum (for example there could be some obstacles that interfere more at lower frequencies, and cause the signal propagation to fade the most, while at higher frequencies that's not an issue).
##### Other Effects
Scattering due to rough surfaces; rain-associated attenuation; gas-associated attenuation; ...

### Wireless Space
Many heterogeneous wireless connectivity technologies (we'll continue having them in future and the set will expand). They usually classify based on different elements:
- **Coverage rage**, the distance up to which the signal can be transmitted using that kind of technology (the more the better);
- **Data rate**, the largest bandwidth reachable using that technology;
- **Energy consumption**, since battery is also important in mobile devices;
- **Economic cost**;

Typically the variation of one aspect impacts on the others, and that's why the research will keep going on (because it's impossible to reach the perfect value for each parameter). For example, an increase in data rate is obtained through an increase in frequency, but that leads to a physical signal that gets more easily absorbed by surrounding objects and therefore the coverage decreases.

### Communication Standards
IEEE 802.x standards defines physical layer and dataling layer protocols.

| OSI model           | 802.3 (Ethernet) | 802.5 (Token Ring) | 802.11 (Wi-Fi) |
| ------------------- | ---------------- | ------------------ | -------------- |
| Data Link Layer (2) |  |  |  |
| Physical Layer (1)  | CSMA/CD bus | token-passing ring | CSMA radio | 

#### Ethernet (IEEE 802.3)
Ethernet (IEEE 802.3) is based on CSMA/CD (Carrier Sense Multiple Access with Collision Detection ~ *il portatore del segnale percepisce gli accessi multipli con rilevamento delle collisioni*) algorithm. It's an **optimistic approach**, that allows multiple access (MA), i.e. allows multiple devices to share the same communication medium:
- performs **==channel sensing==** (CS), to detect if someone is already using it:
	- if not (idle), transmit immediately, but keep listening to the channel;
	- otherwise (occupied), wait until the channel becomes idle;
- ==**collision detection**== (CD):
	- immediate abortion of a transmission if collision is detected;
	- the following transmission try will occur after waiting for a ==**random time interval**==.
	- ==**exponential backoff**==: the backoff time is chosen in an interval that grows exponentially over time, to minimize the probability of **repeated collisions**.
The exponential backoff and randomization prevents the device backoff synchronization (that is when devices keep trying to retransmit at the same interval of time).

**NB**: That's possible due to the transmission medium characteristics in Ethernet (cable), which doesn't cause signal degradation or propagation problems of any kind! We'll see that in wireless it's not so trivial to detect that (due to signal degradation, but also to other factors).

How ethernet works: How ethernet puts packets at layer 2 on the bus trying to avoid collisions (at layer2 the classical problem is if you're using a shared medium transmission - in case of ethernet is the cable, in wifi is the space/air in which the signal travels - where different nodes can decide to transmit packets at the same time)

#### Wireless LAN (IEEE 802.11)
It's the wireless communications for "short-range" (<250m), bandwidth up to 866 Mbps. The standard covers layers 1 and 2, and some security aspects, but doesn't provide any details about Quality of Service.
802.11 is similiar to Ethernet but there are more problems, due to the fact that the cable doesn't degradate the signal, therefore CSMA/CD cannot work correctly:
- collision detection is not always possible nor accurate;
- carrier sensing is not always possible, since not all the nodes are in coverage range;
- mobility considerations;

##### Wireless LAN Issues
The following problems are 802.11 issues, that doesn't happen in Ethernet.
###### Hidden Node Issue
![[hidden_node_issue.png]]
Example:
1. A starts transmittig to B;
2. C cannot be aware of A's communication, because it's out of range, therefore C starts transmitting to B;
3. Collision between the two communication instances;

Occurs when two or more nodes (A and C in the example) are within the range of a central access point AP (B in the example), but they are out of range or unable to sense each other's transmissions.

Is this problem solvable by CSMA? No, but it's not useless at all.

###### Exposed Node Issue
![[exposed_node_issue.png]]
Example:
1. B starts transmitting to A;
2. C detects this transmission and does NOT send any communication towards D;
3. Error: the communication is prevented even if it would not have interfered with A and B.

Occurs when one node refrains from transmitting, even though it could, because it incorrectly believes it might interfere with ongoing communications between other nodes.

###### Multiple Access Collision Avoidance
To solve hidden node and exposed node issues, CSMA/CD is not suitable. Traditionally it was coupled with an additional algorithm, called ==**MACA** (Multiple Access with Collision Avoidance)==.

![[maca.png]]
How does it work? Suppose that B wants to transmit to C;
1. B transmits a first RTS (Ready To Send) frame towards C, which includes the length of the message;
2. C replies with a CTS (Clear to Send) frame, that also includes information about the length of the message;
3. other nodes overhear the RTS and have to remain inactive, in silence, for sufficient time to allow C to reply with CTS;
4. other nodes overhear the CTS and remain silent for the whole duration of the transmission.

Collisions may occur anyway (e.g. RTS frame collisions), but at least data frames (which is the important part of the communication) can NOT.

Current situation? WiFi uses CSMA/CA, which basically integrates MACA, but MACA is still left optional. Even if it's not perfect for WiFi, it was adopted because it's simple and therefore allows the usage of more bandwidth.
### WiFi (IEEE 802.11) Configurations
![[wifi_configurations.png]]
There are two primary WiFi configurations:
- ==**ad hoc mode**==: there are **no access points** between wireless devices and they connect directly;
- ==**base station**== (or infrastructure mode): there is **one AP** that acts like a gateway to reach the Internet and each device connects to it;

In **base station** mode uses the protocol probe/response: a mobile node sends a "probe broadcast message" and Access Points that receive that message respond with a "response message" to signal their presence. Then the mobile node will have a list of available APs to connect to (manually or automatically).
In base station mode, there are no "new" routing problems. Some of the small ones could be:
- what happens if a mobile node moves to another Access Point?
- what happens to our possibility of using the network connection?
Typically in these 2 scenarios (e.g. when using a service which is continuous in time), the connection must be restarted, because the mobile node changes IP address, when it connects to a different Access Point. In fact, when changing IP address, in a client/server model, the TCP connection breaks, and it has to be re-established, by building a new one. Sometimes there are middlewares that handle this to improve the user experience, for example Unibo Almawifi automatically detects when a user disconnects from an Access Point and connects to another, and the framework automatically handles this situation.


In **ad-hoc** mode, there is a routing problem that was not present in infrastructure mode (base station): trying to use traditional IP routing (i.e. the one for fixed nodes, often based on Dijkstra's algorithm), it may not always work, but most certainly it's not efficient. A path that might be optimal at a certain time interval t1, might not be optimal anymore at a t2.
Considerations: 
- a "scarsly mobile" node could be better to be used as part of the path;
- if a node has low battery probably is not so good to be used, since it might go offline.
#### WiFi Direct
WiFi Direct (or WiFi P2P) is a sort of **masked "infrastructure mode"**, since it allows 2 nodes to connect directly. However, what actually happens is that one node acts as an Access Point for the other, but it's a **software** implementation.
The interesting aspect is that only one of the two nodes participating in the communication has to be compliant with WiFi Direct standard to establish a peer-to-peer connection.
> NB: it's different from the hotspot setting! This is a peer-to-peer connection between 2 nodes.

#### WiMAX (IEEE 802.16)
To cover big areas, WiFi 
Goal: grant access to high bandwidth (70Mbps) in metropolitan areas, covering the last mile, since WiFi didn't have enough coverage range (at most 250m). 2 types of stations:
- base stations, installed by Internet Service Providers, and connected via cable to the Internet;
- subscriber stations, installed by users, which acts like modem.

#### WiFi Mesh (IEEE 802.11s)
WiFi alone cannot be used to cover metropolitan areas. Therefore a variant specific for this task was introduced: IEEE 802.11s, WiFi Mesh, is a WiFi variant that exploits access points (base stations) to create a mesh network. In WiFi mesh, connections can be transfered from one base station to another, granting mobility support.
Pros:
- reduced costs;
- robustness;
Cons:
- routing complexity;
- implementation difficulties;
- introduced overhead.
WiFi Mesh didn't have much success, due to the fact that, in order to reach robustness, there was the need to check APs (if one broke for some reason, it would have been necessary to change all the routing paths utilizing the node),

#### MBWA (IEEE 802.11p)
Mobile Broadband Wireless Access (MBWA) is a standard, which was abandoned quite early, that allowed connections of devices moving at over 250 km/h. WiFi wouldn't allow this, since the association time is too long (several hundreds of ms, compared to 5ms of MBWA).
MBWA didn't have much success, because of WiFi variant IEEE 802.11p.

#### Vehicular Mobility (IEEE 802.11p)
WiFi standard variant proper for vehicular mobility. Includes the exchange of data between vehicles at high velocity and road infrastructures (connected to Internet). This technology is used by some car models.

### Cellular Networks
Cellular networks are called this way, due to the implementation concept: geographical areas are divided in adjacent **cells**. Each cell is coveder by an antenna called **Base Station** (BS), as Access Points in base mode.
Each BS is connected to a **Mobile Switching Center** (MSC), that is a fixed station connected to Internet via cable, that connects cells to the Wide Area Network (WAN).
![[cellular_network_architecture.png]]

Suppose we have two nodes A and B, each one referencing a different BSs (BSa and BSb) both belonging to different MSCs (MSCa and MSCb).
A wants to communicate with B, therefore:
1. Node A sends a request to BSa;
2. BSa forwards the message to MSCa;
3. MSCa, passing through Internet, locates MSCb and sends it the message;
4. MSCb forwards the message to BSb;
5. BSb sends the message to node B.

MSCs task is to handle mobility of cellular devices, so that the final user doesn't even notice the cell switching.
Initially it wasn't used Internet, but a proprietary cabled network belonging to telecom companies. 

#### Standard Generations
- **1G**, full **analogic** communication (circuit switching);
- **2G**, only **voice channels**, with communication implemented through **digital** circuit switching (NB: before it was analogic). Example: Global System for Mobile communications (GSM) standard. 2G is the generation where GSM started to gain popularity;
- **2.5G**, channels for **voice and data**. Still relatively ridiculous datarate (384Kbps). Examples: 
	- General Packet Radio Service (GPRS) standard, which is an evolution of GSM;
	- Enhanced Data rates for Global Evolution (EDGE), also an evolution of GSM;
- **3G**, channels for **voice and data**. Basically the same as 2.5G but with increased datarate. Reduction of cells size. Example: Universal Mobile Telecommunications Service (UMTS);
- **4G**, channels for **voice and data**. Increased datarate (up to 1000Mbps download, 500Mbps upload). NB: it's interesting noting that typically in wired connections download and upload datarate are the same, but it's up to the protocol designer to specify it (maybe have greater download, since it is the mostly used);
- **5G**

### GSM (Global System for Mobile communications)
Global System for Mobile communications (GSM) is a standard developed for mobile communication systems. It's the most widely used standard for mobile phones globally and serves as the foundaton for 2G mobile networks.
GSM architecture is hierarchical and follows locality principle.

![[gsm_architecture.png]]

A Mobile Station (mobile node, e.g. a smartphone) is composed by:
- one **Terminal Equipment (TE)**, containing terminal/user-specific data (associated with SIM card)
- one **Mobile Terminal (MT)**, that allows to communicate with the BSS.
A Base Subsystem Station (BSS) is composed by:
- many **Base Transceiver Station (BTS)**, that is responsible for radio communication with mobile devices;
- one **Base Station Controller (BSC)**, that manages and controls multiple (co-located) BTSs. It's responsible for the allocation of radio channels on BTS, and also coordinates the handover process between different cells;

##### BTS (Base Transceiver Station)
BTS are distributed accross the country and provide coverage to mobile devices.
![[gsm_bts.png]]


##### BSC (Base Station Controller)
BSC are located in centralized sites and manages many BTS.
![[gsm_bsc.png]]

##### MSC (Mobile Switching Center)
MSC is used to setup and clear calls and deliver text messages. It also tracks the location of mobile devices under its management.
![[gsm_msc.png]]

MSC acts like a **gateway** to:
- **Public Switching Telephone Network (PSTN)**, which is the traditional and circuit-switched network used prior to Internet;
- **packet data networks** (like Internet) which are more recent.

MSC contains 2 registries:
- **Home Location Register (HLR)** is a centralized database that stores permanent info about subscribed (literally "abbonati", via a telephonic/Internet contract) mobile devices. These info includes and identifier, some location data, service that the user activated, etc. When a mobile node - subscribed to that HLR - starts a call or data session, the MSC queries the HLR to get the needed info.
- **Visitor Location Register (VLR)** is a temporary database associated with each MSC and stores info about mobile devices currently within the coverage range of that MSC (i.e. under one or more of the BSS referencing that MSC). When a mobile device enters the coverage area of a MSC, its VLR is updated by querying the HLR of the MSC where it was initially registered. It also help in load balancing, since it reduces the overall query load to the centralized HLR.
MSC, HLR and VLR serve to provide seamless mobile communication services, ensuring that subscriber information is efficiently managed, and calls can be set up regardless of the mobile device's current location, within the network.

#### GSM Handoff (or Handover)
Motivations:
- stronger signal
- load balancing
- GSM only specifies how (mechanisms) to operate handoff, not why

![[gsm_handoff_same_msc.png]]
==**Handoff steps**== (same MSC):
1. Old BSS decides to perform the handoff process, and send a message to the MSC, providing a list of possible desinations (one or more new BSSs).
2. MSC notifies the new BSS, because it needs to allocate resources.
3. (If there is enough space) the new BSS alloactes the radio channel that the mobile visitor will use. If it doens't arrive in a given time interval, the radio channel is deallocated. NB: that's proactive, because the channel is allocated before receiving the actual connection.
4. New BSS signals the MSC and old BSS it's readiness.
5. Old BSS informs the mobile device the need to operate handover towards the new BSS.
6. The mobile device signals to the new BSS to activate the new channel.
7. Mobile device signals to MSC (through the new BSS) that the handoff has been completed, and MSC performs a re-routing.
8. MSC deallocates resources of the old routing path and notify the old BSS that deallocates the old radio channel associated with the mobile node.

> That's how handoff works in cellular networks. These terms refer to 2G, but the concepts are valid for any later generation).

In crowded areas, typically you can still get connected, due to the fact that an area can be covered by multiple antennas.

One BSS has N radio channel slots to be allocated for N different users (different frequencies, each for a different visitor).
Among these, a quota is always maintained for moving users. The actual amount is not defined in the standard, but usually around 25%.
That's a static reservation, which has a cost and is not optimal, but cannot be predicted apriori.
In fact, when a BSS predicts the new BSS the mobile node can connect to, the prediction MAY be wrong. Therefore resources need to be allocated, even if not always used.
Common goal: achieve service continuity at max at any time. Target is to perform handoff in less than 30ms (main supported service was voice, and it's proven that humans do not notice delays under 30ms).

**Handoff** (different MSC):
![[gsm_handoff_different_cells.png]]

1. The correspondent mobile node starts a call (or data session) towards another mobile node.
2. The request passes through the PSTN that identifies, given the number of the receiver, the corresponding HLR (of the receiver).
3. From the receiver HLR it's possible to obtain the current location of the receiver node and its MSC (the MSC that it's currently connected to).
4. The connection is established.

If the receiver moves, the new MSCs are appended at the end of the chain, but the anchor will always be present.

Anchor MSC is important because in case the mobile phone changes, at runtime, the cell to other MSC, it's the anchor that maintains the link with the currently visited MSC. Independently from your position, you have an anchor MSC (the point where the conversation started), if you or the receiver change position, there's still a link to it. The anchor MSC also keeps information about the call (duration and cost, for example).

Obviously it's possible to have a "direct link" or a chain of links for all the visited MSC during the service. Both options are possible according to the standard. 

There's an optional feature (IS-41) that optimize the path, by minimizing it. However, what's not changed is the anchor MSC.

**IS-41** example:
![[gsm_handoff_different_cells_is-41.png]]

Handoff classification:
- connectivity:
	- **horizontal**, if the connectivity is homogeneous (e.g. handoff between two GSM BSS);
	- **vertical**, if the connectivity is heterogeneous (e.g. handoff passing from 4G connectivity to WiFi);
- node that initiate the procedure:
	- **mobile-initiated** (e.g. WiFi);
	- **network-initiated** (e.g. GSM);
- when it's triggered:
	- **reactive**, if the handoff is triggered only after (as a consequence, as a reaction) a node loses connectivy to the previous AP (e.g. WiFi);
	- **proactive**, if the handoff is triggered before that happens (e.g. GSM);
- management:
	- **hard**, if the mobile device disconnects from the old BSS (e.g. GSM, WiFi);
	- **soft**, if during time interval of the handoff the mobile device stays connected both to the old BSS and the new one (not possible in GSM, nor WiFi, but one could have 2 WiFi cards);
### Bluetooth (IEEE 802.15)
Bluetooth belongs to wireless Personal Area Network (PAN) family, with relatively small range: ~10-100m, low cost (~5/10$ per interface) and that manages both voice and data. It was designed as a technology for cable replacement. 
Bluetooth standard defines specs of protocols for wireless communication, how to use them, and the corresponding software stack.

Main characteristics:
- works in 2.4GHz frequencies (same as WiFi), exploiting ***frequency hopping***;
- initial bandwidth of ~1Mbps;
- low consumption: 1mW-10mW;
- **piconet**, network "star" topology with a master and 7 slaves at most;

Main differences with WiFi:
- In Bluetooth the communication always passes through the master, while in WiFi there is a point-to-point communication between master (AP) and slave (MN).
- Bluetooth needs a preliminar discovery phase, while in WiFi a mobile node simply sends a probe message to all near APs.
- Very limited broadcast mechanism.

#### Bluetooth Topology Formation
Bluetooth topology is the piconet, that consists of a star network formed by a master and up to 7 slaves. Actually nodes can be up to 256 if set to "parked"/"standby" state, i.e. they're part of the network but they're inactive and cannot communicate. Each slave communicate through a single channel in frequency hopping.
The piconet formation occurs in 2 phases:
1. Inquiry phase, to discover the participant and who'll be the master (stupidly/simple enough, the one who started this phase).
2. Page phase, where the master establish a bidirectional channel to the slaves.
##### Inquiry Phase
Goal: collect sufficient info and nodes to establish a piconet.
A node that wants to communicate enters the "inquiry mode": it sends its ID and waits for an answer from its neighbours (containing their IDs). At the end, the node will have a list of the IDs that participate to the piconet. To save energy, other nodes can switch between "inquiry scan mode" and "standby mode".
The node that starts the inquiry becomes the master, and the other will be the slaves. After a time interval, if it received at least one answer, the master enters the page mode.
![[bluetooth_inquiry_phase.png]]
Example:
- purple starts inquiry mode;
- blue is outsite, therefore doesn't receive the inquiry message (and won't be able to join further on);
- red is in range but doesn't respond because it's in standby mode;
- yellows respond because are in "inquiry scan mode" and the connection with them is established.
##### Page Phase
The master establish a bidirectional communication channel with its slaves.
Then it sends the value of its logical clock to the slaves, in order to make them synchronize with it, and requires the slaves to send their estimated clocks and their bluetooth addresses. Another info that is exchanged is the frequency sequence.
The clock synchronization is necessary because in Bluetooth, contrary to WiFi, the communication is split in time slots to prevent collisions *by design*.
One piconet disadvantage is that it requires some time to be built (in seconds). That's tollerable for the devices that Bluetooth is thought for (printers, headphones, etc.).
Once the connection is established, it remains so until the end of the usage.
![[bluetooth_page_phase.png]]
#### Frequency hopping
Bluetooth exploits frequency hopping in 2.4GHz band (79 hop frequencies, at 1 MHz distance). Since piconet members have successfully passed the page phase, we know their clocks are synchronized.
The hopping sequence is determined based on the master address. Each piconet member has to follow the same sequence.
Master and slaves communicate alternating in periodic slots (called rounds). In each slot only a device can communicate: master can communicate using odd slots, while slaves even ones. That prevents collisions.
Pros:
- tends to be more robust to distrubs;
- harder to attack a node if it continuously changes frequency;
Cons:
- the slot usage is not optimized, since not always a device has something to send/receive.

NB: the master can use its slot to send messages but also 
#### Timing and clock
Any bluetooth device has its own native logical clock CLKN. The piconet has a clock, that coincides with the CLKN of the master. 
#### Connections
There are 2 types of connections:
- ==**Asynchronous Connection-Less (ACL)**==: used for **data** traffic (not voice or multimedia) and best-effort service (simplicity over guarantees). Supports:
	- best-effort service;
	- packet-switch connections;
	- point-multipoint connections;
	- symmetric (max ~400Kbit/s) or asymmetric (max ~700Kbit/s downlink and ~60Kbit/s uplink) connections.
	NB: a slave can transmit only if it received the permission from the master in the previous slot.
- ==**Synchronous Connection-Oriented (SCO)**==: used for real-time and **multimedia** traffic. Guaranteed bandwidth (64Kbit/s). Support:
	- circuit-switched connections;
	- point-point connections;
	- symmetric connections;
	**Max 3 connections SCO** towards the same or different slaves, to avoid consume the already little bandwidth for BT. There is no retransmission of packets if they're lost. Why? Because in real-time communication the user just wants a low latency, it doesn't care about the multimedial content to be completely intact. A potential retransmission would do more damage than otherwise (think of it as for UDP).

In SCO connections, a channel is reserved for 2 time slots for communication between master and one specific slave. The reservation periodicity is decided by the master, independently by the need of transmission. ACL communication can only occur in pause intervals between SCO reserved slots. That's also why there is a limit to 3 SCO connections, otherwise every slot could be reserved, not leaving any space for ACLs. 
![[bluetooth_connections.png]]

#### Device States
Bluetooth is not only a 2 layers protocol, but much more (e.g. how devices communicate).
Different states:
- active
- hold (low consumption)
- park (low consumption)
- sniff (low consumption)
![[bluetooth_device_states.png]]
#### Service Discovery Protocol
Since it was created to replace cables, a user would also need to discover what service a particular node offers.
#### Scatternet
Piconets are the classical way to use Bluetooth, but it's not the only topology available.
A scatternet is a combination of more piconets where at least one node participate in both of 2 of the piconets (that for 2 piconets forming a scatternet): they can have a common master but also a common slave.
![[bluetooth_scatternet.png]]
Performance in a scatternet is absolutely not optimal, since the communication becomes multi-hop and the cost of creating a connection increases. Moreover to coordinate all these nodes become much complex, with inquiry and page phases requiring a lot more time.
#### Bluetooth Low Energy (BLE)
Bluetooth variant that allows to significantly reduce battery consumption, by keeping a great communication range. It was included in Bluetooth 4.0.
The main difference with classic Bluetooth is that BLE has a different set of frequencies (40 instead of 79), but wider (2MHz instead of 1MHz).
To avoid interferences and reduce power consumption, BLE uses 3 channels.
Nodes can send advertising packets (advertising node) in broadcast or listen for offered services (scanner node). But since any node (both advertising and scanner) can use all the channels indiscriminately, there's only 1 probability on 9 that a scanner will detect an advertising packet. Therefore BLE has the disadvantage of having a long and variable discovery time.
### ZigBee (IEEE 802.15.4)
Another wireless PAN standard, but specifically designed for sensors and actuators networks, with the following requirements:
- reliability;
- cost-effectiveness;
- low power;
While Bluetooth is designed for domestic environments (replace cables at home), ZigBee is designed for industrial ones (monitoring).
Bluetooth was not suitable for industrial environments, due to its topologies beeing too complex to manage with increasing sizes.
ZigBee supports up to 64k nodes. As BT, ZigBee provides profiles for higher layers of the support/application stack.
It's optimized for topology formation time, especially for when a new node connects (<30ms compared to BT's several seconds).
Support to full mesh networking.
> NB: in ZigBee there's nothing that automatically decides a network topology or how to access a channel. Those choices must be done by the network administrator that programs the PAM coordinator.
#### Topologies
3 different topologies:
- **star**, same as piconet, is the simplest one;
- **mesh**, similiar to WiFi mesh. Each node can have an arbitrary number of connections towards other nodes in its neighborhood. It's very resilient, since each node can have multiple connections. Disadvantage: Overhead;
- **cluster tree**, tree hierarchical topology, with PAN coordinator as the root node. RFD can only be the leaves. The root node has global visibility. Great for scalability and low coordination costs but it's not robust to failures.

 ![[zigbee_topologies.png]]
#### Devices Different Roles
There are different roles for ZigBee devices:
- **PAN coordinator** (~master), one for each ZigBee network. It activates the network formation and acts like a router once the network is functioning. The PAN coordinator must be a reliable node (high battery level, possibly fixed or with limited mobility, etc.);
- **Full Function Device (FFD)**, participates in messages routing;
- **Reduced Function Device (RFD)**, executes only sensing and actuating operations, no routing.

#### Channel Access Options
To access the channel, the nodes can choose between 2 networks types:
- **non-beaconed network**, the nodes will start communicating by basically exploiting MACA and sending positive ACKs for successful reception of packets;
- **beacon-enabled network**, similiar to SCO channels in Bluetooth, the PAN coordinator transmits the permission to transmit (as beacons) at regular time intervals.

Summary on ZigBee: is a sort of combination of the previously seen protocols. It's pretty much domain-specific and it's rare to see (even more rare on a smartphone).

## Chapter 2 - MANET and Routing (ISO/OSI Layer 3)

### MANET
Not all mobile systems operate in infrastructure mode. A Mobile Ad hoc NETwork is a network that is created dynamically, on-the-fly, by nodes that operate in ad-hoc mode.
Main characteristics:
- dynamic creation, (to satisfy immediate necessities);
- quick deployment, highly configurable (no infrastructure needed);
- highly volatile resources (time-dependant resources, that may not be available in time continuity);
- heterogeneous nodes;
- battery nodes;
- each node is a potential router.

Problems:

#### Dynamic Source Routing (DSR)

Main differences between AODV and DSR:
- DSR stores path in headers -> lower space for data;
- AODV stores path in nodes -> much more space for data;

both have 2 discovery phases:
1. RREQ phase (in broadcast), to reach the destination node
2. RREP phase (in unicast), to go back to the source node, with a valid path to the destination.


### Ad hoc On-demand Distance Vector (AODV)
Ad hoc On-demand Distance Vector (AODV) is a reactive routing protocol. Let's break down its name:
- **ad hoc**, because its for MANET, where nodes communicate in ad hoc mode, without access points (not infrastructure mode);
- **on-demand**, because routes are only established and maintained when needed;
- **distance vector**, refers to the routing algorithm used. In networking, a "distance" vector routing algorithm, is a type of algorithm where each "router node" maintains a table that contains distance (cost) to every other router in the network. "Vector" refers to the direction/path to reach a destination. In fact, AODV uses route tables, where each entry has information about the destination node of the route entry (vector), and the number of hops needed to reach it (distance).

AODV steps:
1. S wants to send a packet to D;
2. S checks if it has a route to D;
3. If it doesnt, it starts a route discovery process (**flooding** in broadcast with RREQ);
4. Each node receiving RREQ, if it doesn't have a valid route to D, rebroadcast the message and updates its own ***route table***. A route table includes entries with the following information:
	- seq (sequence number), is used to track the freshness of routing information;
	- dest (destination node), identifies a destination node;
	- next (next-hop), contains the address of the next node of the route, to forward packets towards the destination node;
	- hop (hop count), the number of hops to reach the destination node;
5. When RREQ reaches D or a node with a valid route to D, a RREP is generated and sent back to S (in unicast);
6. When RREP travels back towards S, each node it passes by updates its route table, adding another entry. 

After the discovery phase, nodes will have cached route tables containing both direct and inverse paths. S will choose the table entry with the lowest number of hops, to reach the destination.

#### Timeout
To prevent nodes from maintaining invalid or obsolete entries in routing tables, each route expires after a given timeout. Timeout must be sufficiently long to allow RRES packets to return back from the destination.
Also, forward routes are removed after a certain amount of time (active_route_timeout) if not used. Since we are in MANET, the network is highly variable and mobile, so it's unlikely for a route to be valid during a long period of time. If that route is not used, it could just sit there wasting storage.

#### Link Failure Detection
Failure detection is performed both in reactive and proactive ways:
- **reactive**, when a forward towards an active node (towards which there was a route) fails. In this case all neighbours are informed, through a RERR packet and they invalidate their entry. When S receives RERR, it starts a new route discovery process towards D (NB: there's no certainty that there will be a node with a route to S, in this case typically it performs a flooding, hoping it will reach);
- **proactive**, by periodically sending hello messages to active nodes.

#### Optimizations
1) To limit flooding during route discovery phase, it's possible to perform flooding by using increasingly growing (over time) TTL, until a RREP is received.
2) If during the route discovery phase, a node receiving RREQ for a destination, already has a path towards it, it can instantly reply with RREP. But this can generate ***routing loops***, if RRER of the broken link is lost and the sender doesn't know it.
![[routing_loops.png]]
To solve Loops problem, it's possible to adopt a **Destination Sequence Number (DSN)**: RREQ carries a DSN, that is incremented at each hop. If a node has a route to the RREQ destination, with an higher DSN than the one from RREQ, then it replies with the route, otherwise it forwards the RREQ packet.

### Greedy Perimeter Stateless Routing (GPSR)
Greedy Perimeter Stateless Routing (GPSR) is a routing protocol that didn't have the same historic success than DSR and AODV (those two had a great success due to their simplicity), but is still an interesting approach.
It's a **geographical** routing protocol, that takes into account 2 important assumption, to reach the destination node:
- source node knows the location of the destination node;
- every node has a list of neighbor nodes and their locations (they achieve that by periodically exchanging location beacons).

There are 2 schemas for data forwarding:
- greedy forwarding
- perimeter forwarding;

#### Greedy Forwarding
In greedy forwarding, data is sent to the neighbor node that is estimated as the closes towards the destination, using only the location info of the neighbors of the current node.
![[gpsr_greedy_forwarding.png]]
In the example above, E is not in the coverage range of D, and no other E's neighbor is closer to E, therefore there is a forwarding failure.
When this happens, typically the algorithm switchs to perimeter forwarding.

#### Perimeter Forwarding
It tries to find a route around the "holes" (in the previous example, the hole was between E and D). Each node calculates a Relative Neighborhood ***Graph*** (RNG). This graph is defined by a simple constraint: two nodes A and B are connected only if there is not a third node C whose distance is less than A **and** B.
![[gpsr_perimeter_forwarding_rng.png]]
RNG then traverses the graph following the right-hand rule (counter clockwise), so in the previous example, it would reach S, then A, ...

Problem: there can still be loops, but they can be avoided by using sequence numbers in route tables, as in AODV.

[Comparative analysis paper](https://www.researchgate.net/publication/349377283_Comparative_analysis_of_AODV_DSDV_and_GPSR_routing_protocols_in_MANET_scenarios_of_real_urban_area#fullTextFileContent)

### Temporally Ordered Routing Algorithm (TORA)
Temporally Ordered Routing Algorithm (TORA) is a more recent, proactive, protocol, still used nowadays in practical settings. Main **characteristics**:
- highly adaptive, efficient and scalable;
- loop-free by design;
- highly distributed;

Key **design** concepts:
- control messages are exchanged by a very small set of nodes locally close to each other;
- nodes maintain routing info about their neighbors;
- a **height metric** is used to model the state of the network (the lower the height, the closer to the destination);

During route creation and maintenance nodes establish Directed Acyclic Graphs (DAGs). The data should follow the path that minimizes the height, like a liquid.

![[tora_routing_scheme.png]]

Basic functions:
- **Rroute creation**, based on a *query/reply* process, started by source S, towards destination D. It's performed by flooding a QRY packet. If a route exists, an UDP packet is returned.
- **Route maintenance**, link-reversal algorithm, that activates only when necessary (reacts when there is a link failure). NB: TORA reacts to link failures with **local** repairs.
- **Route erasure**, a CLR packet is flooded to erase invalid routes.

Route creation:
![[tora_route_creation.png]]

TORA has low overhead for control packets, since the reconfigurations are localized; TORA is also faster to respond to failures than DSR or AODV; 
However, each protocol/algorithm has its own usage/field, and usually it depends on the domain of the application and the aspects that it wants to optimize.

Consider that energy consumption typically is a big matter in mobile systems, and the power needed to transmit a packet is proportional to the packet size, but also proportional to distance².

NB: having a large per-hops distance (less nodes but very distanced), typically has more disadvantages than advantages.
- usually to increase the coverage area you have to repeat the signal in space;
- if you increase the frequency of the carrier => more bandwidth, but less distance;
- higher frequencies experience more absorption, more energy consumption and possibly even human health issues (since due to more transmission power);
- higher power => less antennas but less possibility of retransmission.
### Clustering
Clustering is a technique utilized to reduce resource consumption (especially power). It consists in dividing the network in groups of nodes (clusters) and sending to the cluster, a single dense packet that contains information for all the nodes included in the cluster: data aggregator.
It's particularly useful for sensors networks.

Nodes have different **types**:
- clusterhead, fundamental for forwarding of packets inside the cluster. It aggregates data from ordinary nodes which then sends to the gateway;
- gateway, allows to forward packets outside the cluster (to other clusters);
- ordinary nodes, typically are sensors.
![[clustering_node_types.png]]
#### Some Clustering Algorithms
- **Leach**, some local nodes are **randomly** chosen to be clusterhead, then each node chooses its most close one to aggregate. Clusterhead is periodically re-assigned;
- **Heed**, clusterheads are choosen by the **energy level** (cost function) of nodes, by a probabilistic election poll;
- Weighted Clustering Algorithm (WCA), similiar to Heed but takes into account different weights for the cost function.

### Wi-Fi Direct
In a Wi-Fi Direct network, nodes communicate by establishing a Peer-To-Peer (P2P) group, through a software Access Point. The device implementing the AP functionality, is called P2P Group Owner GO, and other devices acts like clients.
A device can also be both client and P2P GO, alternating the two roles by time-sharing the Wi-Fi interface.

#### Comparison Bluetooth Scatternet vs Wi-Fi Direct P2P Group
|  | Bluetooth Scatternet | Wi-Fi Direct P2P Group |
| ---- | ---- | ---- |
| **Communication towards extern** | Only the master can communicate with nodes from other scatternets | Only the P2P GO can communicate with clients from other P2P groups |
| **Leader substitution** | If the master goes offline, a new one is elected | If the P2P GO goes offline, the P2P group needs to be recreated. |
| **Communication** | Only between master and slave | Full P2P (also between client and another client) |
#### Wi-Fi Direct Group Formation
In Wi-Fi Direct, the group formation procedure involves 2 phases:
1. **Determination of P2P GO**, which can be:
	- **negotiated**, two P2P devices negotiates for P2P GO based on their desires and capabilities;
	- **selected**, during the formation or for example at application level;
2. **Provisioning of P2P Group**, that involves the creation of a P2P group session with credentials that are provisioned through simple Wi-Fi configuration.

There are 3 group formation techniques, and the protocol includes all of them:
- **Standard**, involves a discovery phase to find existing groups and Wi-Fi networks (by probe/response). Then they negotiate: the nodes interested in becoming P2P GO declare it and include a random tie-breaker bit to prevent conflicts (the one with bigger bit will become the GO);
- **Autonomous**, a P2P devices autonomously creates a P2P group where it assumes the P2P GO role. Other devices can detect the group and connect.
- **Persistent**, similar to Standard, but after discovery phase, the P2P GO maintains the group info. Those can be used to re-establish the group (accelerating the process).
#### Power Saving Protocols
Wi-Fi Direct defines two power saving mechanisms:
- **Opportunistic Power Save  (OPS)** protocol, basically the P2P GO can go in power save mode, when it knows all the other nodes are sleeping;
- **Notice of Absence (NoA)** protocol, enables the P2P GO to announce "absence periods", which are time intervals where clients are not allowed ro access the channel. The schedule is defined based on 4 parameters (duration, interval, time, count);
#### Security
Wi-Fi Direct compliant devices must implement Wi-Fi Protected Setup (WPS) to support a secure connection with minimal user intervention (PIN or pushing a button).
### Dense MANET
A dense MANET is based on 2 assumptions:
- large number of devices co-located in a physical area relatively small;
- the node density is almost invariant over long time intervals.
There are some non-functional requirements: low overhead, high scalability, sufficient accuracy.

#### REDMAN
REplication in Dense MANet (REDMAN), is a protocol developed by unibo research group of Paolo Bellavista in 2005, to address the Olympics of Torino of 2006.

Basic idea: disseminate replicas of resources of common interest, within the Dense MANET, and maintain the desired replication degree, considering nodes mobility.
Entities involved:
- Delegates, host replicas and reply to retrieval requests;
- Managers, are responsible for maintaining the proper and desired replication degree.

Problems:
- how to identify a Dense MANET;
- Manager election;
- delegate disconnection;


## Chapter 3 - Mobile IP and Positioning
In infrastructured networks, the routing problem is already almost solved: the mobile node connects to an Access Point and the rest is managed through traditional routing.

However, when a node moves, it could change AP and the IP address (node identifier) as well, aborting any ongoing active connection. In GSM/3G/4G networks, there is a proactive resource acquisition for channel allocation to obtain service continuity. The solution would be to keep the same IP address for a mobile user even when it moves, but is it possible?

In basic Internet Protocol (IP), if the mobile node moves without changing its address, it loses routing; but if it does change its address, it loses connections.

### Position Management
2 approaches to know mobile nodes position:
- **location update**, nodes share their position to the infrastructure;
- **location search**, the infrastructure collects location information of mobile nodes;

In Wi-Fi typically the approach is location update, because it's not the purpose of Wi-Fi to discover position of mobile nodes; on the other hand, in cellular networks (GSM, etc.) the approach is usually location search.

#### Location Update
Mobile nodes update their position by notifying the infrastructure (nodes -> infrastructure).
Can be:
- **static**, updates are triggered when exiting a predefined area;
- **dynamic**, triggering depends on user communications and mobility patterns (e.g. data based on time, movement, distance, which are values that can change dynamically in time);

#### Location Search
The infrastructure collects location information of mobile nodes present under its coverage area (infrastructure -> nodes).
Different approaches:
- **blanket polling**, asking in local broadcast all the cells of an area (e.g. all the cells under the control of the MSC where the call arrives);
- **expanding ring search**, starting from the last known location of the device, incrementally expanding the search range (similar to *flooding* with increasing TTL);
- **sequential paging**, based estimation of location *probability* (sequentially from the most probable to the least one). 

### Host Identity Protocol
It was a network-level protocol that proposed to separate the identity and locality information of hosts:
- **Host Identity Tag (HIT)**, for the host identification;
- **IP address**, for the host location;
When Internet was born, it was designed for static network infrastructure "star-like", completely ignoring mobility and security.

To not change the TCP/IP stack (i.e. to not touch existing layers), it introduces a new intermediate layer (~2.5 layer) between network and transport layers.

**Main disadvantage**: compliant devices must implement HIP at kernel level, since they must change their TCP/IP stack.

### Mobile IP
Useful reference: [Oracle Docs on Mobile IP](https://docs.oracle.com/cd/E18752_01/html/816-4554/miptm-1.html)

Mobile IP is the only one level 3 standard that gained success in solving mobility issues in infrastructured networks. 

**Problem**: the IP address associated with a mobile node, depends on the network it's attached to. When it changes the network, the IP typically changes and packets belonging to currently active connections have to be delivered towards the new IP address.

**Intuitive solution**: ~**location update** approach. To handle it as if you were moving in a new apartment. You leave a new *forwarding address* to the old post-office, which then is delegated to send the messages to your new location.

#### Main Idea
Consider two nodes:
- **Mobile Node (MH)** (or Mobile Node MN), can move and receives data;
- **Correspondent Host (CH)**, can be fixed or mobile, and sends data (packets) to MH.
According to Mobile IP, the information about MH location, is always maintained in a third node called **Home Agent (HA)**. Therefore, when CH wants to send packets to MH, it doesn't send them directly to MH (CH doesn't know its position), but sends them to HA, which acts like an intermediary node. 
Actually, HA doesn't forward them directly to MH, but to another intermediary node called **Foreign Agent (FA)**.
![[mobile_ip_basic_idea.png]]

Basically:
- **Home Agent (HA)** is the old post office (intermediary sender);
- **Forward Agent (FA)** is the new post office (intermediary receiver);

**Triangular routing problem**: when the HA is located far but MH and CH are close. In this situation the protocol is very inefficient.

##### Home Agent
It plays the role of **router** and is positioned inside the home network of MH. It's purpose is to **maintain the mobility binding** of MH's **IP address** with its **Care-of Address (CoA)**, which is an IP address that identifies the current location of MH (~basically the AP it's currently attached).

##### Foreign Agent
It's a router as well. When MH is not in the same network of HA, the FA is used to send/receive data to/from HA.
To associate MH to the FA in a certain area:
- **FA** periodically sends ***advertising* messages**, containing a set of available CoAs, to discover the MH in his own locality;
- **MH** can also not wait for advertising and send ***solicitation* messages** to receive a CoA from FA;

Once the MH is associated with the FA, it will receive from it a CoA (temporary IP), and the MH will register it at its HA, passing through the FA.

![[mobile_ip_address_management.png]]

Example:
1. CH wants to communicate with MH (it knows its HoA - Home Address, MH's permanent IP). 
2. CH uses the permanent home IP address of MH as the destination address of the packets to send. 
3. But this IP address belongs to the HA, which instead of forwarding the packets to a node that is physically inside its network, it redirects them towards the CoA through an IP tunnel ([RFC 2003](https://datatracker.ietf.org/doc/html/rfc2003)). That's done by encapsulating the packet in a new IP packet, but with a different destination IP address in its header: the CoA.
![[mip_workflow.png]]

#### Care-of Address
CoA is typically implemented through a normal IP address, used only by Mobile IP (hidden from upper layers).
There are two types of CoA (the network admin can decide which one to use):
- **Foreign Agent CoA**, it is the FA IP address itself and is provided to the MH through advertising messages. To distinguish between different MH under the same FA network, FA also registers the MH's **MAC** addresses. This way there's o waste of IP addresses.
- **Co-Located CoA**, is a temporary standard IP address, allocated by the FA for a single MH (e.g. through DHCP). This way, the HA packets can reach *directly* the MH (via tunneling) but, if there are too many, FA risks to run out of available local addresses.

#### Tunneling
The CH packet is encapsulated from HA in the payload of another packet that contains the CoA of the destination (MH) in its header. This mechanism is called **IP-withing-IP** ([RFC 2003](https://datatracker.ietf.org/doc/html/rfc2003) standard).

##### Practical Example
Suppose we buy a new laptop (MH) and we wanna use Mobile IP. We inform our network administrator, so it provides us a permanent Mobile IP (HoA): 10.0.8.5. This address binds us permanently to the HA, which is the gateway of the network to which our HoA belongs (10.0.8.0/24).
Then we move to a new FA (10.4.5.43) and we receive from it a new CoA (the address of the FA, 10.4.5.43). MH register it in the home HA, passing through FA.

A new node CH wants to communicate with us: it knows the IP of our laptop (10.0.8.5), and will send packets setting 10.0.8.5 as the destination address. Those packets will reach the HA, that will incapsulate them in a new IP packet with FA CoA destination (10.4.5.43).

When these packets reach FA, FA will decapsulate them and will route them towards our node, using the MAC address of our laptop.

To send packets back to CH, instead, we can use direct communication exploiting the node IP address, since it's contained in the packet's header source field.

> **NB**: if a MH leaves the FA network, and meanwhile it receives packets for the MH, those packets are dropped: there's no recovery mechanism in Mobile IP. However, upper layers could implement something to solve this issue (e.g. ACK in TCP).

#### Issues in Ingress/Egress Filtering
Suppose there's this unusual scenario: the CH is attached to the home network.
![[ingress_egress_filtering.png]]

When CH sends a message to MH, it passes through HA, and it gets encapsulated to be sent to FA. The packet's header in this case would have "strange" values, that sometimes router's firewalls may filter automatically.

Routers may **drop MH packets** (due to security configurations) because the addresses don't match:
- **source address** not belonging to the HA internal network;
- **destination address** not belonging to an external network, but the HA's one;

These problems can be avoided by properly configuring the firewall to not discard those kind of packets. But isn't the idea of Mobile IP: Mobile IP doesn't want to impose any kind of extra configuration!
The only way to avoid these problems, directly in Mobile IP (without extra config), is to use the tunnel between HA and FA in both directions. 

Unfortunately, this solution generates another source of inefficiency, making the triangular routing even worse: quadrilateral routing. For this reason, typically this is left optional in Mobile IP, because not all routers have this kind of firewall.
![[quadrilateral_routing.png]]

#### Triangular Routing Optimization
Idea: make CH know the CoA of MH. After the first packet, the HA sends back to CH the CoA of MH, in a message called "CoA update". Afterwards, CH and MH can communicate directly, through tunneling.
Included in Mobile IPv6 standard: in IPv6 it was included the possibility, for a CH, to have direct visibility of the CoA of MH.
Those optimizations are critical in overhead reduction (to solve triangular routing), when CH and MH are under the same foreign network, but HA is far away (on the other side of the planet).

#### Hierarchical Mobile IPv6
Hierarchical Mobile IPv6 (HMIPv6) is a Mobile IP variant/extension to reduce signaling overhead and handover latency, by minimizing the tunneling reconstruction.
![[hierarchical_mobile_ip_v6.png]]
The space is divided in regions, each one managed by a sort of FA gateway, called **Mobile Anchor Point (MAP)**, that handles all the FAs under its management.
When a MH moves under the same MAP, there's no need to rebuild the tunnel between the FA and HA.

There are two main handoff models:
- local subnet handoff, if the handoff occurs between FAs under the same local MAP, the CoA will be registered in the MAP;
- MAP domain handoff, if the handoff occurs between FAs belonging to different MAPs, the regional CoA (RCoA) is registered at both HA and CH.

#### Wireless Mesh Network Management Mechanism
Wireless Mesh Network Management Mechanism (WMM) mixes HMIP and Mesh networks. The idea is to reduce global band consumption by locally handling handovers, without reaching HA. Basically this works by keeping distributed caches (replicated with weak consistency) of location information.
This improves scalability.
NB: you don't need the CoA to go everytime to the HA:
1. search in caches, if not found -> 2.
2. ask the mesh infrastructure, if not found -> 3.
3. flooding

#### Proxy MIPv6
One of the main issues of Mobile IPv6 is that nodes must implement it at kernel level.
To solve this, **Proxy Mobile IPv6 (PMIPv6)** introduces a proxy node, called Mobile Access Gateway (MAG) that implements MIPv6, making it almost completely transparent for mobile nodes.

##### PMIPv6 VS Mobile IP
The main comparison between PMIPv6 and Mobile IP is that:
- in IPMIPv6 the CH sends packets to the LMA (~similiar to the HA in MIP), that creates a tunnel towards MAG (~client in MIP) of the MN.
The difference is that, in PMIPv6, when a node moves from a MAG to another, the tunnel change occurs through a binding update, while in MIP, MHs are forced to be involved

### I-TCP
Mobile infrastructured networks at layer 4. Is TCP suitable? Not at all.
Wireless links in mobile systems are characterized by frequent disconnections and reconnections (high Bit Error Rate - BER). Since TCP treats any problem as a congestion problem, those mobile systems problems causes a degenerative reduction in transmission speed (due to how TCP handles congestions, by incrementally increasing/decreasing the traffic speed).

I-TCP tries to solve this problem: it's a patch to TCP (transport level). The main idea is to **split the connection in segments**:
- we leave standard TCP where it doesn't cause problems, such as in cabled links (e.g. from Base Station MSR to Fixed Host);
- we adopt Wireless-TCP where there could be problems that traditional TCP would handle inefficiently, such as in wireless links.
![[i-tcp.png]]


The main disadvantages are that the end-to-end semantic is violated, and if a MSR breaks, there is a spike of latency and probable connection lost.
### Recap
==TODO==

### Positioning Systems
Positioning systems can be classified in:
- **physical** systems, give specific numeric data that identify a location, such as latitude, longitude and ellipsoid height (altitude) (e.g. GPS); 
- **symbolic** systems, give symbolic positions, higher level of abstraction, such as "Italy", "University of Bologna", etc. Higher privacy because the position obtained doesn't allow to detect exactly where the device is located;
- **absolute** systems, the location refers to only one localization system;
- **relative** systems, the location depends on the position of another device.
- **centralized** systems, exploit a centralized system that collects info for each considered device;
- **distributed** systems, each device auto-detects its own location.

**Accuracy**: is the error range (radius of the "coverage range").
**Privacy**: is the confidence (probability) or trust degree, associated with the accuracy.

#### Basic Techniques

##### Lateration
![[lateration.png]]

==TODO==
#### GPS
Global Positioning System

#### D-GPS
Differential GPS (D-GPS)

#### Indoor Environments

##### Active Badge

##### Active BAT

#### Without Dedicated Hardware

##### GSM-based

##### Bluetooth-based


#### Wi-Fi Fingerprinting

##### PlaceLab

##### RADAR

##### Ekahau

#### Sensor Fusion and VTT

##### JSR-179 

##### PoSIM



## Chapter 4 - Internet of Things (IoT)
Before IoT: Supervisory Control And Data Acquisition (SCADA), implemented remote monitoring and control for sensors/actuators, controllers, communication equipment and software. There were the "things", but they were connected in a completely ad hoc way, without the possibility to be open to the extern: not reachable through Internet!

Many problems (expensive, difficult to extend, lack of standards). For example, if we wanted to include a prediction model, we would have need to implement everything or pay someone to do it, while for IoT there are platform service providers (AWS, Azure, etc.).

---

**IoT Use cases**: smart wearables, smart home, smart city, smart agriculture, connected car, health care, industry automation, smart energy.

General idea: to extend Internet protocols to Wireless Sensors Networks (WSNs), composed of sensors and actuators.

![[iot_general_idea.png]]
IoT main tasks:
- gather information from things and send commands to things (*monitoring/control*);
- send information back and forth remote locations (*cloud*);
- store and aggregate information;
- analyze information to improve system knowledge;
- take decisions, autonomously or human-assisted.

**IoT Small Environment Scenario**: a network that connects uniquely identifiable "Things" to the Internet. The Things have sensing/actuation and potential programmability capabilities. It's possible to collect information about the Things and change their state, from anywhere, anytime, by anything.

**IoT Large Environment Scenario**: self-configuring, adaptive network that interconnects Things to the Internet through standard communication protocols.

### Cloud IoT
In cloud-based IoT architectures, there are heterogeneous devices (e.g. sensors, actuators, etc.) and multiple gateways, geographically close to these devices and can send/receive data to/from Internet. Gateways are the point of convergence of the things ad can also host some software-based functionality. Server-side remote applications are stored in the Cloud ("over the Internet layer").

![[iot_cloud_layered_structure.png]]
Layered structure:
- **analytics**, complex analysis on data to infer new knowledge;
- **IoT platform**, provides services to store, process and manage data; 
- **Data exchange protocol**, software protocol to standardize how information are transmitted;
- **communication protocol**, cabled/wireless technology to effectively send bytes;
- **gateway**, located near one or more things, it capable of interacting with them and the Internet;
- **things**, any physical or digital device that must be monitored or controlled;

==TODO==

#### Cloud Architecture

![[cloud_architecture.png]]

==TODO==

#### Wireless Communication Protocols
![[iot_wireless_communication_protocols_range.png]]


==TODO==




### Data Exchange Protocols

#### Request/Response Model

##### REST
REpresentational State Transfer (REST) is not a real protocol, but more like an architectural style, based on request/response model. It promotes client/server stateless interaction. It supports caches and code-on-demand. Typically is based on HTTP.
- URI (Uniform Resource Identifier) to identify the remote resource;
- HTTP methods to interact: GET, PUT, POST, DELETE.
- JSON to format/serialize data;

##### CoAP
Constrained Application Protocol (CoAP) is a request/response protocol designed for M2M/IoT applications, involving constrained devices and limited networks. It's a RESTful protocol, based on HTTP and has very low overhead.


##### MQTT
Message Queue Telemetry Transport (MQTT)

## Chapter 5 - Android

### Mobile Middleware

Typically hourglass model in mobile application: heterogeneous lower layers, convergence at transport layer (TCP/IP), and again different upper layers related to different needs and requirements of applications.


Cross-layering: different types of interaction for different ways of cross-layering in a protocol stack

- upward information flow
	example: could be useful to propagate location information from hardware (e.g. GPS) to upper layer, cause maybe an application needs them.
- downward information flow
	typically used to configure parameters and settings of lower levels.

#### Architectural Patterns

#### Mobile Computing Patterns
3 main categories:
- for distribution
- for resource management and synchronization
- for communication



### Android

Linux Kernel (95% the same, with some more features, for example for shared memory, communication between processes by using shared memory, power management, etc.)

extra useless Linux features have been removed (compilers, commands and programs)

Only expected to use Java (or Kotlin, still on JVM).

The core system of Android is a special JVM (now called Andoird RunTime - ART, once it was the Dalvik Virtual Machine). It's not the standard Java, it has a lot of differencies, in some classes have been removed, some have been added.
E.g. no support to create processes, cause in Android you are not supposed to do it, for security reasons.
Android bytecode won't work on a standard JVM, and a standard bytecode compiled from a standard Java program won't work on ART.

ART is **registry based**, compared to stack based traditional JVM, since it was decided that the most common processor architecture for Android phone was ARM. Stack-based, on the contrary, is more portable, because it can work on different architecture.

ART is also highly optimized for mobile devices, and the **bytecode** compiled for it is also very optimized (much important in mobile devices).
**Garbage collector** was also changed to not have visible spikes of low performances, because compared to a Desktop app, in a smartphone that's not acceptable

![[android_upper_layer.png]]

The higher layer is the one that developers can use, and it includes a Package Manager to install and manage APKs, and other interesting components.


#### Lifecycle of Activities

##### States
- Running
- Paused
- Stopped
- Inactive
- Killed



#### Task
a Task is an entity that models a "conversation" with the user. It's associated with each application in execution and contains a stack LIFO of Activities. Only the one on top of it is the running one, (state running). The Activities in the task can also be from other applications!

When an activity starts it's pushed on top of the stack.


#### Intent and IntentFilter
Intent is used to specify a "control passing".

Implicit intent vs explicit intent:
- explicit (known at compile time) is less used and already specify the destination of the intent;
- implicit (not known at compile time) doesn't specify the destination, and it's the Android middleware that handles it (it searches if there is a default app set to handle that type of Intent, e.g. add new contact, and if there's not, it asks the user which app it would like to use);
3 cases:
- Android finds only one Activity match for the intent => pass the control to the Activity;
- Android doesn't find any Activity match => the intent is not delivered (lost intent);
- Android finds more than one Activity (no default option specified) => it prompts the user to choose which one to use.
NB: that's because Intents are one-to-one triggers, not multicast! So there can be only one receiver that handles it and takes control.


### Threading Model
Each application has a single thread by default.
Possibility to save the state into Bundle.
Main loop for each thread, with message queue management.


Basically 2 models:
- 1 DVM for each application
- DVM shared (different apps with same UserID) - with this must pay attention to security issues.

NB: each DVM runs in its own process!
#### Scheduling
The runtime handles it and there are 4 process level:
1. foreground
2. visibile
3. service
4. background

Foreground app typically has about 90% of the CPU assigned.

### Asynchronous Techniques

Thread
Executor
HandlerThread
AsyncTask
Service
IntentService
AsyncQueryHandler
Loader

#### Service
Runs in background and doesn't provide any UI nor can it modify the UI directly.
They're typically started by the receiving of an Intent and they run on the main thread.

Examples: music playing in background, file download, etc.

3 types of service:
- started
- bounded
- foreground

##### Started Service
Started with `startService(myIntent);`

`onStartCommand(){}`

##### Bound Service
Special type of Service that offers a client-service interface: it'll run in background and act as a server, while other clients (activities) on the same device can bind and use the features it provides.

Started with `bindService(myIntent);` (e.g. called by an Activity).

`onBind(Intent intent){}` returns an IBinder object that allows clients to communicate with the service.

Bound services are destroyed when there's no clients bound to them.

Question: if the service cannot directly access the UI, how do you update its component to show the results?
You use a broadcast receiver!

##### Foreground Service
Foreground services runs in background but require the user to be aware that they exist and are running. They have higher priority and are unlikely to be killed by the system. They must provide a notification which the user cannot dismiss while it's running.


NB: a service can use worker threads to perform the workload. That's important because if the thread blocks, the UI freezes too.


#### IntentService
They use worker threads to perform an operation, cannot be interrupted, and are automatically destroyed once the operation terminates.
They're particularly useful for things like downloading a file

#### Thread
Very similar to traditional Java threads, cannot directly work on UI (not thread safe).
Launched with `start()`
#### Handler
Used to create a communication channel between main thread of an app and a new thread.
[...]

#### AsyncTask
Services cannot interact directly with UI, therefore, we can use AsyncTask: they're created on UI thread and can be executed only once, in a background thread. After their execution, they can update the UI to show results. 
They are especially useful to perform something inside an Activity, directly related to the Activity itself.

- `onPreExecute()` invoked immediately after the AsyncTask to prepare it (e.g. it can show a loading bar);
- `doInBackground()` to perform the operations (executed in a separated thread);
- `onProgressUpdate(Progress...)` updates the progreess of the AsyncTask (e.g. can update the loading bar);
- `onPostExecute()` typically to update the UI by showing the results and release AsyncTask resources;

This class was deprecated with Android 30 and now it's expected that we use Kotlin concurrency.

Example: download a file.
```
// AsyncTask parameters are:
// 1. Type of parameters (e.g. URL/list of URLs)
// 2. Type of progress unit (e.g. Integer -> 5, 10, ...)
// 3. Type of result (e.g. Image)
public class MyDownloader extends AsyncTask<Params, ProgressUnit, Result> {
	
	// executed on main thread (UI)
	@Override
	protected void onPreExecute () {
		// show a loading bar (main thread -> edit UI)
	}


	@Override
	protected Image doInBackground() {
		// Download image from Repository
	}


	@Override
	protected void onProgressUpdate(Progress...) {
		// Progressively update loading bar (main thread -> edit UI)
	}


	@Override
	protected void onPostExecute(Item response) {
		// Remove loading bar and show result (main thread -> edit UI)
	}
}

// Then to use it
class MyActivity extends Activity {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		mPrefs = getSharedPreferences(getLocalClassName(), MODE_PRIVATE);
		
		// Run the AsyncTask
		MyDownloader myDownloader = new MyDownloader();
		myDownloader.execute();
	}
}
```

#### Broadcast




## Chapter 6 - Discovery

