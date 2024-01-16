<span id="back-to-top"/>
<h1 align="center">Flashcards</h1>


## Chapter 1 - Wireless Communication

### Wireless Signals Propagation
**Question**:
- How is the **wireless signal propagation** influenced?
- What are **channel fading models**?
- Provide some example.

<details><summary><b>Answer: </b></summary>

#### How is the **wireless signal propagation** influenced?
Wireless signals are less reliable than cabled ones, since wireless signals are never 100% guaranteed to be received. When traveling through air, the wireless signal experiences propagation losses, due to the planet/atmosphere and physical phenomena. These losses influences the strength of the signal that, to be received, needs to reach a given threshold.
To understand how wireless signals propagate, researches created 2 propagation models, based on Maxwell's laws:
- **Free-space loss**, according to which, the power of a wireless signal propagating in empty space decrease with its traveled distance (inverse of the square of the distance).
- **Plane earth loss**, according to which, due to Earth's curvature, the power of a wireless signal decreases when traveling along Earth's surface (inverse of the fourth power of the distance).

#### What are **channel fading models**?
In real-world scenarios, the conditions are much more complex, and these are, in fact, just approximated models. In real world there are many phenomena that contribute to the
degradation of the wireless signal. The most important and common are:
- **shadowing**, is due to obstacles along signal path. Causes long-term/slow variation in signal strenght;
- **multipath fading**, is due to signal reaching the receiver through different paths. Causes rapid oscillations in signal strenght;
- **frequency selective fading**, is due to how different ranges in frequencies sprectrum react to noises and other effects. Causes frequency-dependent variations in signal strenght.

![alt](./resources/gfx/channel_fading.png)

Also other phenomena, like rain, magnetic fields, irregular surfaces.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### Ethernet
**Question**:
- How does **Ethernet** try to **avoid collision** on a shared communication medium?

<details><summary><b>Answer: </b></summary>

#### How does **Ethernet** try to **avoid collision** on a shared communication medium?
Ethernet (IEEE 802.3) is an optimistic approach, meaning that try to avoid collisions as bet as it can. There were old Ethernet competitors, such as token-passing ring, that instead avoided collisions by design, but they didn't have so much success as Ethernet.
Ethernet adopts the algorithm called CSMA/CD (which stands for Carrier Sensing Multiple Access with Collision Detection)
- **Carrier Sensing** (CS), means that the devices that participate in the communication, senses the medium (e.g. cable) to check if it's being used it's idle. If idle, the device trasmits immediately, otherwise it waits;
- **Multiple Access** (MA), means that the communication medium is shared between potentially multiple different devices, that could possibly want to use it at the same time;
- **Collision Detection** (CD). When a device transmits, it keeps listening to the medium and, in case it detects a collision, it immediately stops the trasmission and waits. To try again and retransmit, one must wait for a **random time interval**, choosen according to the **exponential backoff**: after each collision, the waiting time increases exponentially, preventing consecutive collision to happen.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### CSMA/CD
**Question**:
- What is **CSMA/CD**?
- Can **CSMA/CD** work correctly over **wireless** medium?
- What are the **most common issues**?

<details><summary><b>Answer: </b></summary>

#### What is **CSMA/CD**?
CSMA/CD is a collision detection algorithm used in Ethernet networks to manage access to a shared communication medium, typically a full-duplex cable in modern environments.

#### Can **CSMA/CD** work correctly over **wireless** medium?
It cannot work correctly in wireless communication, because the communication here is more like a probability: we're never 100% sure a message will be received or not, and there's no easy way to monitor a wireless signal.

#### What are the **most common issues**?
Moreover, there are 2 most common issues
![alt](./resources/gfx/wireless_common_issues.png)
- **Hidden node issue**. It occurs when a node (A) starts transmitting to another one (B), and a third node (C) cannot detect the already ongoing transmission between the other two. Therefore, when it starts transmitting as well, it causes a collision;
- **Exposed node issue**. It occurs when a node (B) transmits to another node (A), and a third node (C) doesn't start transmitting to its peer (D) because it detects the already ongoin transmission between the other nodes, even tough it doesn't interefere with it.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### WiFi
**Question**:
- What is **WiFi** and what are its characteristics?
- What are the primary WiFi **configurations**?

<details><summary><b>Answer: </b></summary>

#### What is **WiFi** and what are its characteristics?
WiFi (IEEE 802.11) is a standard for short range (up to 250m) wireless transmission, up to 866Mbps bandwidth. The standard covers the first two layers (physical and data link/MAC) and provides some security aspects. It doesn't include quality of service specifications.

#### What are the primary WiFi **configurations**?
There are two primary WiFi configurations:
- **Ad hoc mode**, in which nodes communicate directly, peer-to-peer. Each endpoint potentially a mobile node and is connected to the other. Distant node could communicate by using a chain of ad hoc connections. It's more complex, and less used than infrastructure mode.
- **Infrastructure mode** (base station), in which there are some fixed, cabled nodes called Access Points (APs/base stations). A mobile node can obtain a list of the available APs by using the _probe/response_ protocol. Afterwards, it can connect to one (or more, if the mobile node has different WiFi cards) manually or automatically.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### MACA
**Question**:
- Does **MACA** solve hidden node and exposed node issues?

<details><summary><b>Answer: </b></summary>

#### Does **MACA** solve hidden node and exposed node issues?
![alt](./resources/gfx/hidden-node-maca.png)
- **Hidden node issue**: MACA can partially solve this issue, but there are still few cases when it may occurr. For example, C may not hear CTS because it was out of range, but it's moving towards B.
- **Exposed node issue**: is untouched.

However, MACA introduces also some **overhead**, and that's the reason why in modern implementations it's left **optional**.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### Global System for Mobile communications (GSM)
**Question**:
- What is **GSM**?
- How is it **structured**?
- What are Home Location Register (**HLR**) and Visitor Location Register (**VLR**)?

<details><summary><b>Answer: </b></summary>

#### What is **GSM**?
Global System for Mobile communications (GSM) is the most widely used standard for mobile phones globally, and serves as the foundations for 2G mobile networks, and its principles are still used nowadays, in modern technologies. GSM has a hierarchical architecture that follows the locality principle.

#### How is it **structured**?
GSM architecture includes different elements:
- a Mobile System (**MS**), that is composed by:
  - Terminal Equipment (**TE**), associated with SIM card, containing terminal/user specific data;
  - Mobile Terminal (**MT**), that allows to communicate with the BSS;
- a Base Station Subsystem (**BSS**), that is composed by:
  - Base Station Controller (**BSC**), that allocates radio channels and handles handovers. BSC manages many BTS;
  - Base Transceiver Station (**BTS**), that handles connections with MS;
- a Mobile Switching Center (**MSC**), that acts like a gateway to Public Switching Telephone Network (PSTN) and packet data networks (such as Internet).

#### What are Home Location Register (**HLR**) and Visitor Location Register (**VLR**)?
MSC contains 2 registries, needed to perform calls processing, location tracking and mobility management in GSM networks:
- Home Location Register (**HLR**), is a centralized database that stores **permanent** information about subscribed mobile devices. When a user buys a subscription (via SIM card), all the user and subscription info gets registered in HLR (credit, cost, profiles, activated services, etc.). It won't be updated again;
- Visitor Location Register (**VLR**), is a **temporary** database that stores information about mobile devices that are currently within the MSC coverage area (under the BSSs it manages).

When a MS moves to a new MSC (MSC1 -> MSC2), the VLR of MSC2 will add an entry for the MS, by querying the HLR of MSC1. Having information locally is a way to create some sort of load balancing, since once the info are saved in the local VLR, there's no need to keep querying the HLR.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### GSM: Handoff (1)
**Question**:
- What is the **handoff** in in GSM?
- How is it **classified**?

<details><summary><b>Answer:</b></summary>

#### What is the **handoff** in in GSM?
The handoff (or handover) is a procedure in GSM that allows a mobile device to seamlessly switch connection from one cell to another, without interrupting an ongoing call or a data session. It's purpose is to provide service continuity.
It has many advantages, such as:
- always be connected to the BSS with the strongest signal;
- load balancing between different BSS;
The GSM standard doesn't specify when or why the handover should occur, but just the mechanism.

#### How is it **classified**?
Handoff classifications:
- connectivity:
  - horizontal, if same connectivity (GSM);
  - vertical, if different connectivity (WiFi -> 4G);
- node that initiate the procedure:
  - network-initiated (GSM);
  - mobile-initiated (WiFi);
- when it's triggered:
  - proactive, if the handoff is triggered before the connection to previous AP is lost (GSM);
  - reactive, if the handoff is triggered after the connection to previous AP is lost (WiFi);
- management
  - hard, when the old connection breaks before the new one is established (GSM, WiFi);
  - soft, when the old connection is kept until the new one is established (WiFi with 2 cards);

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### GSM: Handoff (2)
**Question**:
- How is the **handoff** handled (distinguish between same and different localities)? TODO
- Can packets be **lost**?
- Does a long call create a chain?
- Is the MSC chain kept?

<details><summary><b>Answer: </b></summary>

#### How is the **handoff** handled (distinguish between same and different localities)?
Steps for the **handoff under the same MSC**:
1. Old BSS decides to perform the handoff process and sends a message to the MSC, provide a list of possible new BSSs.
2. MCS notifies the new BSSs, because they need to allocate resources.
3. (If there is enough space) the new BSS allocates the radio channel for the new visitor. If it doesn't arrive in time, it gets deallocated.
4. New BSS notifies the MSC and old BSS that it's ready.
5. Old BSS informs the mobile device the need to operate handover towards the new BSS.
6. The mobile device signals to the new BSS to activate the new channel.
7. The mobile device signals to MSC that the handoff has been completed, and MSC performs re-routing.
8. The MSC deallocates resources of the old routing path and notifies the old BSS that deallocates the old radio channel not used anymore.

Steps for the **handoff under different MSCs**:
1. Suppose a mobile node S starts a call towards a mobile node D.
2. Through the phone number of D the PSTN reaches the HLR of D.
3. From the HLR it's possible to reach the current MSC to which D is attached: this is the Anchor MSC, and will be the first MSC node, forming a chain. The anchor node also saves all the info needed for the call or data session.
4. When the destination moves, if it switches MSC, the new MSC will be appended at the end of the chain.

#### Can packets be **lost**?
Yes they can, especially with hard handoffs. Actually, it's almost impossible to have avoid packet loss completely, but there are mitigation techniques

#### Does a long call create a chain?
If a node is moving, typically a long call creates a chain of MSC, where newer MSCs gets appended to the latest visited one. The first one is called anchor MSC, is always present and doesn't change for the whole duration of the voice call or data session.

#### Is the MSC chain kept?
The MSC chain can be kept or not, it depends. There is a standard called IS-41, that optimizes the MSCs chain path, linking the anchor MSC directly with the latest MSC visited.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### Bluetooth
**Question**:
- What is Bluetooth and what are its main **characteristics**?
- What are the differences with **WiFi**?
- What is **frequency hopping**?
- What are the differences between **ACL** and **SCO**?
- Is there **retransmission** in SCO? Why?

<details open><summary><b>Answer: </b></summary>

#### What is Bluetooth and what are its main characteristics?
Bluetooth (IEEE 802.15.1) belongs to the family of Personal Area Network (PAN) protocols, which range is quite limited (10-100m). It was created to **replace cables** with a low cost solution that had a decent datarate (at least 1Mbps). The network topology it uses is called piconet, and is formed by a _master_ and up to 7 _slaves_.
Bluetooth standard defines not only the protocol but also the associated software stack, as well as profiles for its usage.

#### What are the differences with **WiFi**?
The main differences with Wi-Fi are:
- uses cases;
- coverage range;
- data transfer rate;
- power consumption;
- in Bluetooth the communication always passes through the master, in Wi-Fi the communication is P2P between AP and MNs;
- Bluetooth needs a preliminar discovery phase;
- Bluetooth has a very limited broadcast mechanism;

#### What is **frequency hopping**?
Bluetooth uses the 2.4GHz ISM band (from 2.4 to 2.4835 GHz), which is also the same range of frequencies used by many wireless technologies/devices (including WiFi), since this band was designated for unlicensed operation. What's the consequence of this? It's that different technologies based on 2.4GHz, may interfere the one with the other.

Bluetooth, to manage its communication over this overcrowded band, uses a mechanism called "**frequency hopping**": the 2.4GHz band can be divided into 79 channels, each of 1MHz width. The bluetooth actively changes communication channel, by hopping between frequencies in a defined sequence (based on master's address): the communication _timeline_ is divided in time slots (625 picoseconds, 1600 times per second), in which only a device can communicate. This prevents interferences and adds a layer of security.

There is also an optimized version, called "adaptive frequency hopping", to better improve this mechanism, marks channels with high interferences as "bad channels" and avoid them.

#### What are the differences between **ACL** and **SCO**?
Bluetooth supports two types of connections:
- **Asynchronous Connection-Less (ACL)**:
  - is used only for data (no voice);
  - packet-switched connections;
  - point-multipoint connections;
  - symmetric/asymmetric connections;
  - retransmission of lost packets;
- **Synchronous Connection-Oriented (SCO)**:
  - is used for multimedia data in real-time;
  - circuit-switched connections;
  - point-point connections;
  - symmetric connections;
  - no retransmission of lost packets;

#### Is there **retransmission** in SCO? Why?
In Bluetooth SCO there is NO retransmission if packets are lost, because in real-time communication the user just wants low latency, it doesn't care about the multimedia content to be completely intact (e.g. think about voice calls).

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### ZigBee
**Question**:
- What is ZigBee and what are its **characteristics**?
- What are the possible **topologies**?
- What are the **roles**?

<details open><summary><b>Answer: TODO</b></summary>

#### What is ZigBee and what are its **characteristics**?
ZigBee (IEEE 802.15.4)

#### What are the possible **topologies**?

#### What are the **roles**?

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

## Chapter 2 - Mobile Ad Hoc NETwork (MANET)

### MANET
**Question**:
- What are MANETs and what are their main **characteristics**?
- What are its main problems?
- What are the **types** of routing protocols?

<details><summary><b>Answer: </b></summary>

#### What are MANETs and what are their main **characteristics**?
Mobile Ad hoc NETworks are networks made by node that communicate in ad hoc mode. Its main characteristics are that they're very dynamic, they can be created and configured quickly, on-the-fly; the involved nodes are typically heterogeneous; each node is a potential router.

#### What are its main problems?
MANETs problems are: limited range, hidden node issue, transmission error, mobility, energetic limits and security. Also, even though it should be obvious in ad-hoc mode, in MANETs the routing is quite complicated.

#### What are the **types** of routing protocols?
Routing protocols in MANETs can be divided into:
- **proactive** protocols, keep valid routes regardless of ongoing traffic;
- **reactive** protocols, keep valid routed only when there's traffic (on communication demand);
- **geographic** protocols, use the destination location to route the messages;
- **hybrid** protocols, that combine other categories.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### Flooding Routing
**Question**:
- How does flooding routing protocol **works**?
- **When** is it used?
- How can it be **optimized**?
- What is the **broadcast storm issue**?

<details><summary><b>Answer: </b></summary>

#### How does flooding routing protocol **works**?
Flooding is the most basic and simple routing protocol, where each node forwards an ingoing packet to each node available in broadcast, except for the sender (the one from who the current node received the packet), until the destination is reached.

#### **When** is it used?
Flooding is the simples, most trivial and straightforward routing protocol. It has some advantages, such as the fact that it doesn't require any storage of information on nodes. It has many problems, mostly efficiency ones, since the number of generated packets grows exponentially with the number of nodes. However, it still finds some uses, for example in emergency scenarios or when there's no way around. Flooding is often used in conjunction with other protocols, for example to deliver control packets.

#### How can it be **optimized**?
Examples:
- to **avoid recursive sends** (sending a packet to a node that already received it), we could add an ID to the packet;
- to **avoid infinite hops** even after the packet is received, we could use a TTL (Time-To-Live);

#### What is the **broadcast storm issue**?
Broadcast storm issue, is something that's often involved in flooding, and occur when a large number of broacast or multicast messages are rapidly propagated and circulated through the network (nothing -> nothing -> spike of traffic -> nothing -> ...). That creates excessive traffic and potentially degrading network performances.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### DSR Routing ([RFC 4728](https://www.rfc-editor.org/rfc/rfc4728.html))
**Question**:
- What is DSR routing and how does it **work**?
- What **problems** there could be?
- How can it be **optimized**?

<details><summary><b>Answer: TODO</b></summary>

#### What is DSR routing and how does it **work**?
Dynamic Source Routing (DSR) is a full reactive routing protocol, where the sender has to find a valid routing path. The steps for Source (S) to find a valid route to reach Destination (D), are the following:
1. S uses **flooding** to send a **control packet RREQ** (Route REQuest) in broadcast;
2. Each node that receives RREQ check if it doesn't have already sent it, and if it did not, it appends its node ID and forwards the packet again in broadcast;
3. This procedure repeats until D is reached;
4. When D receives the packet, it uses the chain of nodes in the header (path S->D), builds a control packet RREP (Route REPly), adding the path to it and sends it back in unicast to S;
5. S receives RREP, retrieves the path to reach D and saves it in its cache;
6. S sends the actual data packets to D, including the path in their headers.

#### What **problems** there could be?
- This protol faces many collisions, due to the fact that the traffic concentrates in small intervals of time (broadcast storm issue).
- Moreover there is the hidden node issue, when for example two nodes are sending to the same destination, a collision is very likely to occur. 

In general, it's a matter of trade-offs.

#### How can it be **optimized**?
For example through **path caching**: any node cache new path that it happens to discover (in any possible ways). Some obvious advantages, but also some disadvantages, such as invalid caches (being a MANET, after some time, the path doesn't work anymore). How can those be invalidated in a MANET? Through Route ERRor (RERR) control packet.

When a node cannot reach the following one in the route chain, it sends back to S a RERR control packet, containing the path tha is not available anymore. Any node that overhears this, can update its cache as well.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### AODV Routing ([RFC 3561](https://www.ietf.org/rfc/rfc3561.txt))
**Question**:
- What is AODV routing protocol?
- What do tables contain?
- What happens if there are link errors?
- How are link errors handled?
- Can loops be formed? How?
- How can loops be solved?
- What happens if nobody has a path towards the destination node, after a fault?

<details><summary><b>Answer: TODO</b></summary>

#### What is AODV routing protocol?
Ad hoc On-demand Distance Vector (AODV) is a reactive routing protocol that consists in [...]
Its main difference with DSR is that AODV doesn't save path information inside packet headers, but instead stores them into the single nodes (similiar to IP routing). That reduces the overhead and allows for more data to be transferred inside the packet payloads.

#### What do tables contain?
AODV exploits routing tables, saved on each MANET node, to save information about routes to reach the nodes. When a node S wants to send a packet to a node D, it first check if its routing table has an entry with the path to reach D. If not, S performs a path discovery, by exploiting flooding (RREQ(ID,src,dst) in broadcast). Each node maintains a route table, where it saves entries about the "known paths", and the hops needed to reach it. Therefore there will be two types of entries (direct path and inverse path entries). To prevent outdated or invalid routing table entries, there is a timeout mechanism (which is longer for direct routes).

Example:
- when receiving a RREQ a node updates its routing table by adding an "inverse path entry"
- inverse paths are the ones to return from D to S (used for RRES);
- direct paths are the ones to reach 

#### Can loops be formed? How?
Routing loops, even if very unlikely, can occur in AODV. For example, a loop can be formed when optimizing the route discovery process: if the protocol allows nodes to reply to RREQ with a path they know (so that the RREQ doesn't have to reach D), then there could be the possibility that the path is invalid due to a lost RERR packet. Visual example:\
![alt](./resources/gfx/routing_loops.png)

#### How can loops be avoided?
Routing loops can be avoided by using a Destination Sequence Number (DSN): each route entry in nodes route tables, has a sequence number field that indicates the freshness of the route. The DSNs are incremented each time the nodes send a message.
During the route discovery phase, the RREQ will be carrying the destination node D as well as a DSN. Upon reaching a node, if the current node has a route to D with an higher DSN (compared to the one in RREQ), it immediately replies with RREP containing the route to D; otherwise, it forwards the RREQ to the next nodes.

#### What happens if nobody has a path towards the destination node, after a fault?
The source starts a new discovery phase, performing RREQ flooding.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### GPSR Routing
**Question**:
- What is **GPSR** routing protocol?
- What are **greedy forwarding** and **perimeter forwarding**?
- How is the perimeter forwarding **graph** built?

<details><summary><b>Answer: </b></summary>

#### What is **GPSR** routing protocol?
Greedy Perimeter Stateless Routing (GSPR) is a geographical routing protocol, that makes two important assumptions:
- the source node S knows the location of the destination node D;
- every node has a list of its neighbor nodes and their locations (collected by periodically exchanging beacons).

#### What are **greedy forwarding** and **perimeter forwarding**?
GPSR performs data fowarding according to 2 schemas, _greedy forwarding_ and _perimeter forwarding_, that are switched the one with the other, when there is a fowarding failure:
- **greedy forwarding**, according to which each node forwards the data packet to the closest neighbor. If the closest neighbor is not reachable (e.g. out of coverage range) there is a forwarding failure;
- **perimeter forwarding**, each node calculates a Relative Neighborhood Graph (RNG) based on the constraint that two nodes are connected only if there isn't a third node that is closer to both. Then the graph is traversed applying the right-hand rule (counter clockwise choice), to select the next hop.

#### How is the perimeter forwarding **graph** built?
The perimeter forwarding graph is called Relative Neighborhood Graph (RNG) and is built by each node based on a constraint: two nodes A and B are connected if and only if there is not a third node C whose distance to both A and B is closer than the one between A and B (C-A < A-B && C-B < A-B).
![alt](./resources/gfx/gpsr_rng.png)

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### TORA Routing
> **NB**: Specific details on TORA won't be asked during the exam.

**Question**:
- What is **TORA** routing protocol and what are its main characteristic?
- What are its main **functions**?

<details><summary><b>Answer: </b></summary>

#### What is **TORA** routing protocol and what are its main characteristic?
Temporally Ordered Routing Algorithm (TORA) is a more recent routing protocol, that is still used nowadays in practical settings. Its main characteristics are the following:
- highly adaptive, efficient and scalable;
- is loop-free by design;
- is highly distributed;

It's based on a graph structure called Directed Acyclic Graph (DAG), organized by an height metric. The data packets flows in this graph towards the bottom, as a liquid. 

#### What are its main **functions**?
TORA is based on 3 main functions:
- Route **creation**, based on a query/reply process, started by the source node, towards the destination. It's performed by flooding the network with a QRY packet and, if a route exists, an UDP packet is returned to source.
- Route **maintenance**, consists of a LOCAL link repair, when a link failuer is detected (reactive repair).
- Route **failure**, a CLR packet is flooded to erase invalid routes.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### Clustering
**Question**:
- What is Clustering in a MANET?
- In what consist Leach and Heed algorithms?

<details><summary><b>Answer: </b></summary>

#### What is Clustering in a MANET?
Clustering is a technique utilized to reduce energy consumption in MANETs. It's very suitable for sensors networks and consists in grouping nodes in clusters, with a clusterhead and some gateway, and in aggregating multiple data in a single packet, that gets forwarded through the gateway.

#### In what consist Leach and Heed algorithms?
Leach and Heed are two algorithms for Clustering in MANETs:
- In **Leach**, the clusterhead is chosen in a compeltely random way, it sends a broadcast message to inform other nodes, and ordinary nodes attach to the closer one. The clusterhead is reassigned every now and then to try performing some load balancing.
- In **Heed**, clusterheads are chosen based on the level of battery, through a probabilistic election. Nodes announce their intention (clusterhead or not) and cost function (based on battery), and other nodes select and attach the best candidate, through aa probabilistic metric.

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

### Wi-Fi Direct
**Question**:
- How does **Wi-Fi Direct** work?
- Provide a **comparison** between **Bluetooth Scatternet** and Wi-Fi Direct groups.
- What are the possible **group formation techniques**?

<details><summary><b>Answer: TODO</b></summary>

#### How does **Wi-Fi Direct** work?
In Wi-Fi Direct nodes communicate by establishing a Peer-to-Peer (P2P) group, through a software based AP. In Wi-Fi P2P groups, there is a P2P Group Owner (GO) and other devices act like clients.

#### Provide a **comparison** between **Bluetooth Scatternet** and Wi-Fi Direct groups.
Wi-Fi Direct groups and  Bluetooth Scatternets are somewhat similiar, for their topology and the fact that only the P2P GO and the master can communicate with external nodes (from other P2P groups or other scatternets).

#### What are the possible **group formation techniques**?

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

## Chapter 3 - Mobile IP and Positioning

### Topic
**Question**:
<details><summary><b>Answer: </b></summary>

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

## Extra

### Template
```
### Topic
**Question**:
<details><summary><b>Answer: </b></summary>

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---
```
roba da chiedere al prof:
ho letto che le implementazioni moderne del WiFi utilizzano CSMA/CA, che praticamente integra MACA, ma in questo caso, viene comunque (solitamente) lasciato opzionale?
