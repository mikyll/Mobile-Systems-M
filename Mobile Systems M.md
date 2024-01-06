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

**Question**: How does Ethernet try to avoid collision on a shared communication medium?
**Answer**:  CSMA/CD (Carrier Sensing Multiple Access / Collision Detection)
- Carrier Sensing (i.e on the cable there is a carrier - always powered - so the nodes can allign themselves around this carrier)
- Collision Detection - there is smth at layer2 that makes nodes able to detect if someone is already using that channel.

#### CSMA/CD Algorithm
Ethernet (IEEE 802.3) is based on CSMA/CD (Carrier Sense Multiple Access with Collision Detection ~ *il portatore del segnale percepisce gli accessi multipli e rileva le collisioni*) algorithm. It's an **optimistic approach**, that:
- performs **==channel sensing==**, to detect if someone is already using it:
	- if not (idle), transmit immediately;
	- otherwise (occupied), wait until the channel becomes idle;
- ==**collision detection**==:
	- immediate abortion of a transmission if collision is detected;
	- the following transmission try will occur after waiting for a ==random== time interval.
	- ==**exponential backoff**==: the backoff time is chosen in an interval that grows exponentially over time, to minimize the probability of repeated collisions.
The exponential backoff and randomization prevents the device backoff synchronization (that is when devices keep trying to retransmit at the same interval of time).

**NB**: That's possible due to the transmission medium characteristics in Ethernet (cable), which doesn't cause signal degradation or propagation problems of any kind! We'll see that in wireless it's not so trivial to detect that (due to signal degradation, but also to other factors).



How ethernet works: How ethernet puts packets at layer 2 on the bus trying to avoid collisions (at layer2 the classical problem is if ur using a shared medium transmission - in case of ethernet is the cable, in wifi is the space/air in which the signal travels - where different nodes can decide to transmit packets at the same time)

Ethernet: shared bus (single cable) connecting many different PCs, how does ethernet avoid collisions? 

## Chapter 2 - MANET and Routing (ISO/OSI Layer 3)

## Chapter 3 - Mobile IP and Positioning

### 2.1 MANET and Routing

### 2.2 Mobile IP and Positioning

## Chapter 3 - IoT and Related Applications

## Chapter 4 - Android

## Chapter 5 - 

## Chapter 6 - 