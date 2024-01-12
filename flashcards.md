<div align="center">
  <h1>Flashcards</h1>
</div>

## Chapter 1 - Wireless Communication

### Wireless Signals Propagation
**Question**:
- How is the **wireless signal propagation** influenced?
- What are **channel fading models**?
- Provide some example.

<details><summary><b>Answer: </b></summary>

Wireless signals are less reliable than cabled ones, sincew ireless signals are never 100% guaranteed to be received.
When traveling through air, the wireless signal experiences propagation losses, due to the planet/atmosphere and physical phenomena. These losses influences the strength of the signal that, to
be received, needs to reach a given threshold.
To understand how wireless signals propagate, researches created 2 propagation models, based on Maxwell's laws:
- **Free-space loss**, according to which, the power of a wireless signal propagating in empty space decrease with its traveled distance (inverse of the square of the distance).
- **Plane earth loss**, according to which, due to Earth's curvature, the power of a wireless signal decreases when traveling along Earth's surface (inverse of the fourth power of the distance).

In real-world scenarios, the conditions are much more complex, and these are, in fact, just approximated models. In real world there are many phenomena that contribute to the
degradation of the wireless signal. The most important and common are:
- **shadowing**, is due to obstacles along signal path. Causes long-term/slow variation in signal strenght;
- **multipath fading**, is due to signal reaching the receiver through different paths. Causes rapid oscillations in signal strenght;
- **frequency selective fading**, is due to how different ranges in frequencies sprectrum react to noises and other effects. Causes frequency-dependent variations in signal strenght.

![alt](./resources/gfx/channel_fading.png)

Also other phenomena, like rain, magnetic fields, irregular surfaces.

</details>

---

### Ethernet
**Question**:
- How does **Ethernet** try to **avoid collision** on a shared communication medium?

<details><summary><b>Answer: </b></summary>
  
Ethernet is an optimistic approach, meaning that try to avoid collisions as bet as it can. There were old Ethernet competitors, such as token-passing ring, that instead avoided collisions by design, but they didn't have so much success as Ethernet.
Ethernet adopts the algorithm called CSMA/CD (which stands for Carrier Sensing Multiple Access with Collision Detection)
- **Carrier Sensing** (CS), means that the devices that participate in the communication, senses the medium (e.g. cable) to check if it's being used it's idle. If idle, the device trasmits immediately, otherwise it waits;
- **Multiple Access** (MA), means that the communication medium is shared between potentially multiple different devices, that could possibly want to use it at the same time;
- **Collision Detection** (CD). When a device transmits, it keeps listening to the medium and, in case it detects a collision, it immediately stops the trasmission and waits. To try again and retransmit, one must wait for a **random time interval**, choosen according to the **exponential backoff**: after each collision, the waiting time increases exponentially, preventing consecutive collision to happen.

</details>

---

### CSMA/CD
**Question**:
- What is **CSMA/CD**?
- Can **CSMA/CD** work correctly over **wireless** medium?
- What are the **most common issues**?

<details><summary><b>Answer: </b></summary>
  
CSMA/CD is a collision detection algorithm used in Ethernet networks to manage access to a shared communication medium, typically a full-duplex cable in modern environments. It cannot work correctly in wireless communication, because the communication here is more like a probability: we're never 100% sure a message will be received or not, and there's no easy way to monitor a wireless signal.

Moreover, there are 2 most common issues
![alt](./resources/gfx/wireless_common_issues.png)
- **Hidden node issue**. It occurs when a node (A) starts transmitting to another one (B), and a third node (C) cannot detect the already ongoing transmission between the other two. Therefore, when it starts transmitting as well, it causes a collision;
- **Exposed node issue**. It occurs when a node (B) transmits to another node (A), and a third node (C) doesn't start transmitting to its peer (D) because it detects the already ongoin transmission between the other nodes, even tough it doesn't interefere with it.

</details>

---

### MACA
**Question**:
- Does **MACA** solve hidden node and exposed node issues?

<details><summary><b>Answer: </b></summary>

![alt](./resources/gfx/hidden-node-maca.png)
  
- Hidden node issue: MACA can partially solve this issue, but there are still few cases when it may occurr. For example, C may not hear CTS because it was out of range, but it's moving towards B.
- Exposed node issue: is untouched.

However, MACA introduces also some overhead, and that's the reason why in modern implementations it's left optional.

</details>

---

### Global System for Mobile communications (GSM)
**Question**:
- What is **GSM**?
- How is it **structured**?
- What are Home Location Register (**HLR**) and Visitor Location Register (**VLR**)?

<details><summary><b>Answer: </b></summary>

What is **GSM**?
Global System for Mobile communications (GSM) is the most widely used standard for mobile phones globally, and serves as the foundations for 2G mobile networks, and its principles are still used nowadays, in modern technologies. GSM has a hierarchical architecture that follows the locality principle.

How is it **structured**?
GSM architecture includes different elements:
- a Mobile System (**MS**), that is composed by:
  - Terminal Equipment (**TE**), associated with SIM card, containing terminal/user specific data;
  - Mobile Terminal (**MT**), that allows to communicate with the BSS;
- a Base Station Subsystem (**BSS**), that is composed by:
  - Base Station Controller (**BSC**), that allocates radio channels and handles handovers. BSC manages many BTS;
  - Base Transceiver Station (**BTS**), that handles connections with MS;
- a Mobile Switching Center (**MSC**), that acts like a gateway to Public Switching Telephone Network (PSTN) and packet data networks (such as Internet).

What are Home Location Register (**HLR**) and Visitor Location Register (**VLR**)?
MSC contains 2 registries:
- Home Location Register (**HLR**), is a centralized database that stores permanent information about subscribed mobile devices. When a user buys a subscription (via SIM card), all the subscription info gets registered in HLR;
- Visitor Location Register (**VLR**), is a temporary database that stores information about mobile devices that are currently within the MSC coverage area (under the BSSs it manages)

</details>

---

### GSM: Handoff (1)
**Question**:
- What is the **handoff** in in GSM?
- How is it **classified**?

<details><summary><b>Answer:</b></summary>

The handoff (or handover) is a procedure in GSM that allows a mobile device to seamlessly switch connection from one cell to another, without interrupting an ongoing call or a data session. It's purpose is to provide service continuity.
It has many advantages, such as:
- always be connected to the BSS with the strongest signal;
- load balancing between different BSS;
The GSM standard doesn't specify when or why the handover should occur, but just the mechanism.

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
  - hard, when the old connection breaks before the new one is enstablished (GSM, WiFi);
  - soft, when the old connection is kept until the new one is enstablished (WiFi with 2 cards);

</details>

---

### GSM: Handoff (2)
**Question**:
- How is the **handoff** handled (distinguish between same and different localities)? TODO
- Can packets be **lost**?
- Does a long call create a chain?
- Is the MSC chain kept?

<details><summary><b>Answer: TODO</b></summary>

How is the **handoff** handled (distinguish between same and different localities)?
Steps for the handoff under the same MSC:
1. Old BSS decides to perform the handoff process and sends a message to the MSC, provide a list of possible new BSSs.
2. MCS notifies the new BSSs, because they need to allocate resources.
3. (If there is enough space) the new BSS allocates the radio channel for the new visitor. If it doesn't arrive in time, it gets deallocated.
4. New BSS notifies the MSC and old BSS that it's ready.
5. Old BSS informs the mobile device the need to operate handover towards the new BSS.
6. The mobile device signals to the new BSS to activate the new channel.
7. The mobile device signals to MSC that the handoff has been completed, and MSC performs re-routing.
8. The MSC deallocates resources of the old routing path and notifies the old BSS that deallocates the old radio channel not used anymore.

Steps for the handoff under different MSCs:
1. TODO

Can packets be **lost**?
Yes they can, especially with hard handoffs. Actually, it's almost impossible to have avoid packet loss completely, but there are mitigation techniques

Does a long call create a chain?
If a node is moving, typically a long call creates a chain of MSC, where newer MSCs gets appended to the latest visited one. The first one is called anchor MSC, is always present and doesn't change for the whole duration of the voice call or data session.

Is the MSC chain kept?
The MSC chain can be kept or not, it depends. There is a standard called IS-41, that optimizes the MSCs chain path, linking the anchor MSC directly with the latest MSC visited.

</details>

---

### Bluetooth
**Question**:
- What is Bluetooth and what are its main characteristics?
- 

<details><summary><b>Answer: TODO</b></summary>

</details>

---

**Question**:

<details><summary><b>Answer: TODO</b></summary>

</details>

---

## Chapter 2 - Mobile Ad Hoc NETwork (MANET)

**Question**:

<details><summary><b>Answer: </b></summary>

</details>

---

**Question**:
<details><summary><b>Answer: </b></summary>

</details>


roba da chiedere al prof:
ho letto che le implementazioni moderne del WiFi utilizzano CSMA/CA, che praticamente integra MACA, ma in questo caso, viene comunque (solitamente) lasciato opzionale?

## Extra

Domande esami:

Chapter 1
- Bluetooth: main characteristics
- Bluetooth: differences between ACL and SCO? Is there retransmission in SCO? Why?
- Bluetooth: differenze SCO e ACL
- ZigBee: topologies and roles?
a. Zigbee quali sono le topologie?
b. Quali sono i ruoli?
