



### Positioning Systems
**Question**:
- How can positioning systems be **classified**?
- What are the **basic techniques** to calculate devices distance? 
- What are the main **error sources**?

<details><summary><b>Answer: </b></summary>

#### How can positioning systems be **classified**?
Positioning systems can be classified in the following categories:
- **physical**/**symbolic** systems:
- **absolute**/**relative** systems:
- **centralized**/**decentralized** systems:

Other factors:
- **accuracy**;
- **precision**;
- **privacy**;
- **scalability**;
- **technology costraints** and **costs**;

#### What are the **basic techniques** to calculate devices distance?
**Lateration**

There are different ways to calculate the distance:
- Based on **signal propagation**.
- Based on **signal strength**.

**Time Difference of Arrival**

**Angulation**

**Proximity**

**Scene Analysis**

#### What are the main **error sources**?
The most common error sources are the following:
- non line of sight (**NLoS**);
- **shadowing** and **multipath** fading;
- **clock skew**, which is due to wrong clock synchronization;

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

## Chapter 4 - Internet of Things (IoT)

### Data Exchange Protocols
**Question**:
- Who **starts** the communication in IoT data exchange? What are the two **main protocol models**?
- Describe **CoAP** protocol.
- Describe **MQTT** protocol.

<details><summary><b>Answer: </b></summary>

#### What are the two main models for data exchange protocols?
IoT data exchange typically involves gateways and servers and communication can be initiated in two ways:
- **push**, gateways autonomously decide to send messages to servers (proactive);
- **pull**, servers ask gateways to send messages (reactive);

The two main models are:
- **Request**/**response** (both push and pull): a client sends a request and a server replies. The client knows the server and the communication can be started only from the client, not viceversa. 
- **Publish**/**subscribe** (typically only push), involves 3 entities: **publisher(s)** sends  messages, **subscriber(s)** receives the messages it's interested in (through topics), the **broker(s)** is a central component that receives messages from publishers and forwards them to subscribers, according to the message topics. The broker forwards messages based on their **_topic_**, _type_, _header_ and _content_. This model promotes space, time and synchronization decoupling.

#### Describe **CoAP** protocol.
Constrained Application Protocol (CoAP, [RFC 7252](https://datatracker.ietf.org/doc/html/rfc7252)) is a request/response protocol designed for M2M/IoT applications, involving constrained devices and limited networks. It's main characteristics are the following:
- Web RESTful compliant;
- HTTP-based (level 7);
- URI and content-type support;
- low header overhead;
- based on UDP (level 4), with optional reliability and support for both unicast and multicast;
- can utilize different protocols than IP (level 3), for example a more lightweight protocol such as 6LoWPAN;
- asynchronous messages;
- supports also publish/subscribe (with push notifications);
- simple caching with max-age parameter.

Typically the gateway has a complete IP stack so that it can convert CoAP messages in HTTP request to interact with the cloud.

#### Describe **MQTT** protocol.
Message Queue Telemetry Transport (MQTT, [RFC 9431](https://datatracker.ietf.org/doc/html/rfc9431)) is a publish/subscribe messaging protocol. It's main characteristics/features are:
- publish/subscribe to provide one-to-many message distribution;
- open standard (but strongly supported by IBM);
- based on TCP/IP to provide basic network connectivity;
- low transport (level 4) overhead;
- simple and easy to use;
- retained messages (an MQTT broker can retain a message so that it can be sent also to new subscribers);
- 3 delivery message semantics with increasing reliability and cost to guarantee QoS (Quality of Service): at least once, at most once, exactly once;
- durable connections (client subscriptions are kept even in case of disconnections);
- wills (messages to be sent in case the client disconnects unexpectedly, like an alarm);

</details>
<p align="right">(<a href="#back-to-top">back to top</a>)</p>

---

## Chapter 5 - Android