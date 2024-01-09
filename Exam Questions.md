## Chapter 1

**==Question==**: How is the **wireless signal propagation** influenced? What are **channel fading models**? Provide some example.
**==Answer==**: when traveling through air, the wireless signal experiences propagation losses, due to the planet/atmosphere and physical phenomena. These losses influences the strength of the signal.
Channel fading models are mathematical representations that help describe signal propagation losses.
Generic propagation losses, according to Maxwell's laws:
- **Free-space loss**, is due to air resistance. Without any obstacles, the signal strenght decreases when distance and/or frequency increases.
- **Plane earth loss**, is due to Earth's curvature. The signal strenght decreases when traveling along Earth's surface, proportionally to distance.
Physical phenomena (approximated through channel fading models):
- **shadowing**, is due to obstacles along signal path. Causes long-term/slow variation in signal strenght;
- **multipath fading**, is due to signal reaching the receiver through different paths. Causes rapid oscillations in signal strenght;
- **frequency selective fading**, is due to how different ranges in frequencies sprectrum react to noises and other effects. Causes frequency-dependent variations in signal strenght.

---

**==Question==**: How does **Ethernet** try to **avoid collision** on a shared communication medium?
==**Answer**==: Ethernet is an optimistic approach, meaning that try to avoid collisions as bet as it can. There were old Ethernet competitors, such as token-passing ring, that instead avoided collisions by design, but they didn't have so much success as Ethernet.
Ethernet adopts the algorithm called CSMA/CD (which stands for Carrier Sensing Multiple Access with Collision Detection)
- **Carrier Sensing** (CS), means that the devices that participate in the communication, senses the medium (e.g. cable) to check if it's being used it's idle. If idle, the device trasmits immediately, otherwise it waits;
- **Multiple Access** (MA), means that the communication medium is shared between potentially multiple different devices, that could possibly want to use it at the same time;
- **Collision Detection** (CD). When a device transmits, it keeps listening to the medium and, in case it detects a collision, it immediately stops the trasmission and waits. To try again and retransmit, one must wait for a **random time interval**, choosen according to the **exponential backoff**: after each collision, the waiting time increases exponentially, preventing consecutive collision to happen.

---

**==Question==**: Can **CSMA/CD** work correctly over **wireless** medium? What are the **most common issues**?
**==Answer==**: TODO

---

**==Question==**: What are hidden node and exposed node issues?
**==Answer==**: TODO

---

**==Question==**: Does **MACA** solve hidden node and exposed node issues?
**==Answer==**:
- Hidden node issue: MACA can partially solve this issue, but there are still few cases when it may occurr. For example, C may not hear CTS because it was out of range, but it's moving towards B.
![[hidden-node-maca.png]]

- Exposed node issue: is untouched
However, MACA introduces also some overhead, and that's the reason why in modern implementations it's left optional.

---

**==Question==**:
**==Answer==**:

---

**==Question==**:
**==Answer==**:


roba da chiedere al prof:
ho letto che le implementazioni moderne del WiFi utilizzano CSMA/CA, che praticamente integra MACA, ma in questo caso, viene comunque (solitamente) lasciato opzionale?


Domande esami:

Chapter 1
- hidden node and exposed node issues
- MACA
- GSM: handoff handling
- GSM: handoff classification
- Bluetooth: main characteristics
- Bluetooth: differences between ACL and SCO? Is there retransmission in SCO? Why?
- ZigBee: topologies and roles?


CH1
- parlare di hidden/exposed node issues
- MACA caratteristiche 
- MACA risolve hidden/exposed node?
- Bluetooth: differenze SCO e ACL

Comunicazioni wireless
a. Si parli dei problemi dell’hidden node e exposed node

b. Maca per WiFi risolve questi problemi?
c. Caratteristiche del protocollo MACA
d. Per quanto tempo i nodi stanno in silenzio?
e. Il problema dell’exposed node è risolto da MACA?
f. Come può in nodo mobile interagire con questo protocollo?

Differenze tra SCO e ACL in bluetooth

GSM wireless communication
a. Come avviene la gestion dell’handoff in GSM?
b. Reattivo o proattivi?
c. Ci possono essere perdite di pacchetti?
d. Durante una chiamata lunga si crea una catena?

Wireless communication
a. GSM come viene gestito l’handoff nella stessa località?
b. Come viene gestito tra località diverse?
c. Viene mantenuta la catena di msc?
d. Può esservi la perdita di pacchetti nell’handoff?

Wireless communication bluetooth
a. Differenze tra SCO e ACL

Wireless communication
a. Zigbee quali sono le topologie?
b. Quali sono i ruoli?