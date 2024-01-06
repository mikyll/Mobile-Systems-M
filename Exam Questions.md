## Chapter 1

**==Question==**: How is the **wireless signal propagation** influenced? What are **channel fading models**? Provide some example.
**==Answer==**: when traveling through air, the wireless signal experiences propagation losses, due to the planet/atmosphere and physical phenomena. These losses influences the strength of the signal.
Channel fading models are mathematical representations that help describe signal propagation losses.
Generic propagation losses, according to Maxwell's laws:
- Free-space loss, is due to air resistance. Without any obstacles, the signal strenght decreases when distance and/or frequency increases.
- Plane earth loss, is due to Earth's curvature. The signal strenght decreases when traveling along Earth's surface, proportionally to distance.
Physical phenomena (approximated through channel fading models):
- shadowing, is due to obstacles along signal path. Causes long-term/slow variation in signal strenght;
- multipath fading, is due to signal reaching the receiver through different paths. Causes rapid oscillations in signal strenght;
- frequency selective fading, is due to how different ranges in frequencies sprectrum react to noises and other effects. Causes frequency-dependent variations in signal strenght.

**==Question==**: How does Ethernet try to avoid collision on a shared communication medium?
==**Answer**==:  CSMA/CD (Carrier Sensing Multiple Access / Collision Detection)
- Carrier Sensing (i.e on the cable there is a carrier - always powered - so the nodes can allign themselves around this carrier)
- Collision Detection - there is smth at layer2 that makes nodes able to detect if someone is already using that channel.

**==Question==**:
**==Answer==**: