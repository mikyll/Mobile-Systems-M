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
![[Pasted image 20231210014023.png]]

#### Channel Fading Models
The signal is also ==influenced by physical phenomena== that affects its ==propagation==. The most relevant and dominant ones are shadowing, Raileigh fading, and frequency-selective fading.

NB: large-scale VS small-scale fading. Slow fading implies that the changes in signal strength occur over larger distances or longer periods, making them more predictable and manageable.

![[Pasted image 20231210012429_edited.png]]

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
![[Pasted image 20240106171425.png]]
Example:
1. A starts transmittig to B;
2. C cannot be aware of A's communication, because it's out of range, therefore C starts transmitting to B;
3. Collision between the two communication instances;

Occurs when two or more nodes (A and C in the example) are within the range of a central access point AP (B in the example), but they are out of range or unable to sense each other's transmissions.

Is this problem solvable by CSMA? No, but it's not usefull at all.

###### Exposed Node Issue
![[Pasted image 20240106172055.png]]
Example:
1. B starts transmitting to A;
2. C detects this transmission and does NOT send any communication towards D;
3. Error: the communication is prevented even if it would not have interfered with A and B.

Occurs when one node refrains from transmitting, even though it could, because it incorrectly believes it might interfere with ongoing communications between other nodes.

###### Multiple Access Collision Avoidance
To solve hidden node and exposed node issues, CSMA/CD is not suitable. Traditionally it was coupled with an additional algorithm, called ==**MACA** (Multiple Access with Collision Avoidance)==.

![[Pasted image 20240106173355.png]]
How does it work? Suppose that B wants to transmit to C;
1. B transmits a first RTS (Ready To Send) frame towards C, which includes the length of the message;
2. C replies with a CTS (Clear to Send) frame, that also includes information about the length of the message;
3. other nodes overhear the RTS and have to remain inactive, in silence, for sufficient time to allow C to reply with CTS;
4. other nodes overhear the CTS and remain silent for the whole duration of the transmission.

Collisions may occur anyway (e.g. RTS frame collisions), but at least data frames (which is the important part of the communication) can NOT.

Current situation? WiFi uses CSMA/CA, which basically integrates MACA, but MACA is still left optional. Even if it's not perfect for WiFi, it was adopted because it's simple and therefore allows the usage of more bandwidth.

### WiFi (IEEE 802.11) Configurations
![[Pasted image 20240106190124.png]]
There are two primary WiFi configurations:
- ==**ad-hoc mode**==: there are **no access points** between wireless devices and they connect directly;
- ==**base station**== (or infrastructure mode): there is **one AP** that acts like a gateway to reach the Internet and each device connects to it;

In base station mode, there are no "new" routing problems. Some of the small ones could be:
- what happens if a mobile node moves to another Access Point?
- what happens to our possibility of using the network connection?
Typically in these 2 scenarios (e.g. when using a service which is continuous in time), the connection must be restarted, because the mobile node changes IP address, when it connects to a different Access Point. In fact, when changing IP address, in a client/server model, the TCP connection breaks, and it has to be re-enstablished, by building a new one. Sometimes there are middlewares that handle this to improve the user experience, for example Unibo Almawifi automatically detects when a user disconnects from an Access Point and connects to another, and the framework automatically handles this situation.

In ad-hoc mode, there is a routing problem that was not present in infrastructure mode (base station): trying to use traditional IP routing (i.e. the one for fixed nodes, often based on Dijkstra's algorithm), it may not always work, but most certainly it's not efficient. A path that might be optimal at a certain time interval t1, might not be optimal anymore at a t2.
Considerations: 
- a "scarsly mobile" node could be better to be used as part of the path;
- if a node has low battery probably is not so good to be used, since it might go offline.
#### WiFi Direct
WiFi Direct (or WiFi P2P) is a sort of masked "infrastructure mode", since it allows 2 nodes to connect directly. However, what actually happens is that one node acts as an Access Point for the other, but it's a software implementation.
The interesting aspect is that only one of the two nodes participating in the communication has to be compliant with WiFi Direct standard to enstablish a peer-to-peer connection.

#### WiMAX (IEEE 802.16)









## Chapter 2 - MANET and Routing (ISO/OSI Layer 3)

## Chapter 3 - Mobile IP and Positioning

### 2.1 MANET and Routing

### 2.2 Mobile IP and Positioning

## Chapter 3 - IoT and Related Applications

## Chapter 4 - Android

## Chapter 5 - 

## Chapter 6 - 