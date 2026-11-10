# Network Types
- WAN(Wide Area Network)
	- tldr WAN=internet
- LAN(Local Area Network)
	- collection of device that connect together in one physical location
	- example: connecting to college ethernet via cable
- WLAN(Wireless Local Area Network)
	- same as lan but can connect via wireless
- VPN(Virtual Private Network)
	- site to site vpn
		a secure connection that can connect to multiple seperate networks to provide a single unified network experience
	- Remote Access VPN
		a tecchnology that allow for a user to connect securely to a private company server and encrypt the traffic so it remain private to snooper
	- SSL VPN
		similar to remote access vpn but it use SSL/TLS to encrypt the connection between users and the internal network
- GAN(Global Area Network)
	a world wide network example: internet
- MAN(Metropolitan Area Network)
	a network that connect several lan in geographical proximity
- WPAN(Wireless Personal Area Network)/PAN(personal area network)
	a network in form of cable or wireless(bluetooth or wireless usb) to onnect multiple modern end device to form a network to enable data exchange
# Network Topology
A `network topology` is a typical arrangement and `physical` or `logical` connection of devices in a network. Computers are `hosts`, such as `clients` and `servers`, that actively use the network. They also include `network components` such as `switches`, `bridges`, and `routers`, which have a distribution function and ensure that all network hosts can establish a logical connection with each other.
In contrast, the `logical topology` is how the signals act on the network media or how the data will be transmitted across the network from one device to the devices' physical connection.
We can divide the entire network topology area into three areas:
1. Connections

| Wired connections    | Wireless connections |
| -------------------- | -------------------- |
| Coaxial cabling      | Wi-Fi                |
| Glass fiber cabling  | Cellular             |
| Twisted-pair cabling | Satellite            |
| and others           | and others           |

2. Nodes - Network Interface Controller (NICs)
	Network nodes are the `transmission medium's connection points` to transmitters and receivers of electrical, optical, or radio signals in the medium.

|  Repeaters   |   Hubs   |  Bridges  | Switches |
| :----------: | :------: | :-------: | :------: |
| Router/Modem | Gateways | Firewalls |          |

3. Classifications
	We can imagine a topology as a virtual form or `structure of a network`. This form does not necessarily correspond to the actual physical arrangement of the devices in the network. Therefore these topologies can be either `physical` or `logical`.
Network topologies are divided into the following eight basic types:

|                |             |
| -------------- | ----------- |
| Point-to-Point | Bus         |
| Star           | Ring        |
| Mesh           | Tree        |
| Hybrid         | Daisy chain |
### Point-to-Point
The simplest network topology with a dedicated connection between two hosts is the `point-to-point` topology. In this topology, a direct and straightforward physical link exists only between `two hosts`. These two devices can use these connections for mutual communication.

`Point-to-point` topologies are the basic model of traditional telephony and must not be confused with `P2P` (`Peer-to-Peer` architecture).
	Point-To-Point Topology
![image](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_p2p.png)
### Bus

All hosts are connected via a transmission medium in the bus topology. Every host has access to the transmission medium and the signals that are transmitted over it. There is no central network component that controls the processes on it. The transmission medium for this can be, for example, a `coaxial cable`.

Since the medium is shared with all the others, only `one host can send`, and all the others can only receive and evaluate the data and see whether it is intended for itself.

#### Bus Topology

![Diagram showing a connection between Host A and Host B.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_bus.png)

---

### Star

The star topology is a network component that maintains a connection to all hosts. Each host is connected to the `central network component` via a separate link. This is usually a router, a hub, or a switch. These handle the `forwarding function` for the data packets. To do this, the data packets are received and forwarded to the destination. The data traffic on the central network component can be very high since all data and connections go through it.

#### Star Topology

![Diagram showing connections between Hosts A, B, C, D, E, and F.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_star.png)

---

### Ring

The `physical` ring topology is such that each host or node is connected to the ring with two cables:

- One for the `incoming` signals and
- another for the `outgoing` ones.

This means that one cable arrives at each host and one cable leaves. The ring topology typically does not require an active network component. The control and access to the transmission medium are regulated by a protocol to which all stations adhere.

A `logical` ring topology is based on a physical star topology, where a distributor at the node simulates the ring by forwarding from one port to the next.

The information is transmitted in a predetermined transmission direction. Typically, the transmission medium is accessed sequentially from station to station using a retrieval system from the central station or a `token`. A token is a bit pattern that continually passes through a ring network in one direction, which works according to the `claim token process`.

#### Ring Topology

![Diagram showing a router connecting Hosts A, B, C, and D.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_ring.png)

---

### Mesh

Many nodes decide about the connections on a `physical` level and the routing on a `logical` level in meshed networks. Therefore, meshed structures have no fixed topology. There are two basic structures from the basic concept: the `fully meshed` and the `partially meshed` structure.

Each host is connected to every other host in the network in a `fully meshed structure`. This means that the hosts are meshed with each other. This technique is primarily used in `WAN` or `MAN` to ensure high reliability and bandwidth.

In this setup, important network nodes such as routers could be networked together. If one router fails, the others can continue to work without problems, and the network can absorb the failure due to the many connections.

Each node of a fully meshed topology has the same routing functions and knows the neighboring nodes it can communicate with proximity to the network gateway and traffic loads.

In the `partially meshed structure`, the endpoints are connected by only one connection. In this type of network topology, specific nodes are connected to exactly one other node, and some other nodes are connected to two or more other nodes with a point-to-point connection.

#### Mesh Topology

![Network diagram showing Hosts A, B, C, and D connected through Routers A, B, C, and D.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_mesh.png)

---

### Tree

The tree topology is an extended star topology that more extensive local networks have in this structure. This is especially useful when several topologies are combined. This topology is often used, for example, in larger company buildings.

There are both logical tree structures according to the `spanning tree` and physical ones. Modular modern networks, based on structured cabling with a hub hierarchy, also have a tree structure. Tree topologies are also used for `broadband networks` and `city networks` (`MAN`).

#### Tree Topology

![Network diagram showing a server connected to two Ethernet switches, each linking to Hosts A, B, C, D, E, and F.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_tree.png)

---

### Hybrid

Hybrid networks combine two or more topologies so that the resulting network does not present any standard topologies. For example, a tree network can represent a hybrid topology in which star networks are connected via interconnected bus networks. However, a tree network that is linked to another tree network is still topologically a tree network. A hybrid topology is always created when `two different` basic network topologies are interconnected.

#### Hybrid Topology

![Network diagram showing Hosts A, B, C, D, E, and F connected through Routers A, B, and C.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_hybrid.png)

---

### Daisy Chain

In the daisy chain topology, multiple hosts are connected by placing a cable from one node to another.

Since this creates a chain of connections, it is also known as a daisy-chain configuration in which multiple hardware components are connected in a series. This type of networking is often found in automation technology (`CAN`).

Daisy chaining is based on the physical arrangement of the nodes, in contrast to token procedures, which are structural but can be made independent of the physical layout. The signal is sent to and from a component via its previous nodes to the computer system.

#### Daisy Chain Topology

![Network diagram showing Hosts A, B, D, and E connected to Host C.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_daisy-chain.png)

# Proxies
Proxies is when a device or service sits in the middle of a connection and acts as a mediator.
mediator is an important piece of information that mean the device must be able to inspect the content of the traffic.without mediator ability a device is just a gateway not a proxy.
proxies will almost always operate at Layer 7 of the OSI Model. There are many types of proxy services, but the key ones are:

- `Dedicated Proxy` / `Forward Proxy`
- `Reverse Proxy`
- `Transparent Proxy`
### Dedicated Proxy / Forward Proxy
A Forward Proxy is when a client makes a request to a computer, and that computer carries out the request.
	For example, in a corporate network, sensitive computers may not have direct access to the Internet. To access a website, they must go through a proxy (or web filter). This can be an incredibly powerful line of defense against malware, as not only does it need to bypass the web filter (easy), but it would also need to be `proxy aware` or use a non-traditional C2 (a way for malware to receive tasking information). If the organization only utilizes `FireFox`, the likelihood of getting proxy-aware malware is improbable.
Web Browsers like Internet Explorer, Edge, or Chrome all obey the "System Proxy" settings by default. If the malware utilizes WinSock (Native Windows API), it will likely be proxy aware without any additional code. Firefox does not use `WinSock` and instead uses `libcurl`, which enables it to use the same code on any operating system. This means that the malware would need to look for Firefox and pull the proxy settings, which malware is highly unlikely to do.

Alternatively, malware could use DNS as a c2 mechanism, but if an organization is monitoring DNS (which is easily done using [Sysmon](https://medium.com/falconforce/sysmon-11-dns-improvements-and-filedelete-events-7a74f17ca842) ), this type of traffic should get caught quickly.

Another example of a Forward Proxy is Burp Suite, as most people utilize it to forward HTTP Requests. However, this application is the swiss army knife of HTTP Proxies and can be configured to be a reverse proxy or transparent!

#### Forward Proxy

![Diagram showing Host A sending an HTTP request through a Forward Proxy to the Internet, reaching a Webserver. Host B is also connected.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/forward_proxy.png)

### Reverse Proxy
a `reverse proxy`, is the reverse of a `Forward Proxy`. Instead of being designed to filter outgoing requests, it filters incoming ones. The most common goal with a `Reverse Proxy`, is to listen on an address and forward it to a closed-off network.

Penetration Testers will configure reverse proxies on infected endpoints. The infected endpoint will listen on a port and send any client that connects to the port back to the attacker through the infected endpoint. This is useful to bypass firewalls or evade logging. Organizations may have `IDS` (`Intrusion Detection Systems`), watching external web requests. If the attacker gains access to the organization over SSH, a reverse proxy can send web requests through the SSH Tunnel and evade the IDS.

Another common Reverse Proxy is `ModSecurity`, a `Web Application Firewall` (`WAF`). Web Application Firewalls inspect web requests for malicious content and block the request if it is malicious. If you want to learn more about this, we recommend reading into the [ModSecurity Core Rule Set](https://owasp.org/www-project-modsecurity-core-rule-set/), as its a great starting point. Cloudflare, also can act as a WAF but doing so requires letting them decrypt HTTPS Traffic, which some organizations may not want.

#### Reverse Proxy

![Diagram showing Host A sending an HTTP request through the Internet, passing firewalls, a Reverse Proxy, and reaching a Webserver. Host B is also connected.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/reverse_proxy.png)

### (Non-) Transparent Proxy

All these proxy services act either `transparently` or `non-transparently`.

With a `transparent proxy`, the client doesn't know about its existence. The transparent proxy intercepts the client's communication requests to the Internet and acts as a substitute instance. To the outside, the transparent proxy, like the non-transparent proxy, acts as a communication partner.

If it is a `non-transparent proxy`, we must be informed about its existence. For this purpose, we and the software we want to use are given a special proxy configuration that ensures that traffic to the Internet is first addressed to the proxy. If this configuration does not exist, we cannot communicate via the proxy. However, since the proxy usually provides the only communication path to other networks, communication to the Internet is generally cut off without a corresponding proxy configuration.

# Networking Models

Two networking models describe the communication and transfer of data from one host to another, called `ISO/OSI model` and the `TCP/IP model`. This is a simplified representation of the so-called `layers` representing transferred Bits in readable contents for us.

![Comparison of OSI and TCP/IP models: OSI has 7 layers including Application, Presentation, Session, Transport, Network, Data-Link, and Physical. TCP/IP has 4 layers: Application, Transport, Internet, and Link.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/net_models4_updated.png)
## The OSI Model

The `OSI` model, often referred to as `ISO/OSI` layer model, is a reference model that can be used to describe and define the communication between systems. The reference model has `seven` individual layers, each with clearly separated tasks.

The term `OSI` stands for `Open Systems Interconnection` model, published by the `International Telecommunication Union` (`ITU`) and the `International Organization for Standardization` (`ISO`). Therefore, the `OSI` model is often referred to as the `ISO/OSI` layer model.
## The TCP/IP Model

`TCP/IP` (`Transmission Control Protocol`/`Internet Protocol`) is a generic term for many network protocols. The protocols are responsible for the switching and transport of data packets on the Internet. The Internet is entirely based on the `TCP/IP` protocol family. However, `TCP/IP` does not only refer to these two protocols but is usually used as a generic term for an entire protocol family.

For example, `ICMP` (`Internet Control Message Protocol`) or `UDP` (`User Datagram Protocol`) belongs to the protocol family. The protocol family provides the necessary functions for transporting and switching data packets in a private or public network.
## ISO/OSI vs. TCP/IP

`TCP/IP` is a communication protocol that allows hosts to connect to the Internet. It refers to the `Transmission Control Protocol` used in and by applications on the Internet. In contrast to `OSI`, it allows a lightening of the rules that must be followed, provided that general guidelines are followed.

`OSI`, on the other hand, is a communication gateway between the network and end-users. The OSI model is usually referred to as the reference model because it is newer and more widely used. It is also known for its strict protocol and limitations.
## Packet Transfers

In a layered system, devices in a layer exchange data in a different format called a `protocol data unit` (`PDU`). For example, when we want to browse a website on the computer, the remote server software first passes the requested data to the application layer. It is processed layer by layer, each layer performing its assigned functions. The data is then transferred through the network's physical layer until the destination server or another device receives it. The data is routed through the layers again, with each layer performing its assigned operations until the receiving software uses the data.

![Comparison of OSI and TCP/IP models with PDUs: OSI has 7 layers including Application, Presentation, Session, Transport, Network, Data-Link, and Physical. TCP/IP has 4 layers: Application, Transport, Internet, and Link. PDUs are Data, Segment/Datagram, Packet, Frame, and Bit.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/net_models_pdu2_updated.png)

During the transmission, each layer adds a `header` to the `PDU` from the upper layer, which controls and identifies the packet. This process is called `encapsulation`. The header and the data together form the PDU for the next layer. The process continues to the `Physical Layer` or `Network Layer`, where the data is transmitted to the receiver. The receiver reverses the process and unpacks the data on each layer with the header information. After that, the application finally uses the data. This process continues until all data has been sent and received.

![Diagram of packet transfer showing data encapsulation from sender to receiver through layers: Data, TCP, IP, MAC, and Binary Transmission, with corresponding headers and sequence.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/packet_transfer.png)

For us, as penetration testers, both reference models are useful. With `TCP/IP`, we can quickly understand how the entire connection is established, and with `ISO`, we can take it apart piece by piece and analyze it in detail. This often happens when we can listen to and intercept specific network traffic. We then have to analyze this traffic accordingly, going into more detail in the `Network Traffic Analysis` module. Therefore, we should familiarize ourselves with both reference models and understand and internalize them in the best possible way.

# The OSI Model
The goal in defining the `ISO/OSI` standard was to create a reference model that enables the communication of different technical systems via various devices and technologies and provides compatibility. The `OSI` model uses `seven` different layers, which are hierarchically based on each other to achieve this goal. These layers represent phases in the establishment of each connection through which the sent packets pass. In this way, the standard was created to trace how a connection is structured and established visually.

|**Layer**|**Function**|
|---|---|
|`7.Application`|Among other things, this layer controls the input and output of data and provides the application functions.|
|`6.Presentation`|The presentation layer's task is to transfer the system-dependent presentation of data into a form independent of the application.|
|`5.Session`|The session layer controls the logical connection between two systems and prevents, for example, connection breakdowns or other problems.|
|`4.Transport`|Layer 4 is used for end-to-end control of the transferred data. The Transport Layer can detect and avoid congestion situations and segment data streams.|
|`3.Network`|On the networking layer, connections are established in circuit-switched networks, and data packets are forwarded in packet-switched networks. Data is transmitted over the entire network from the sender to the receiver.|
|`2.Data Link`|The central task of layer 2 is to enable reliable and error-free transmissions on the respective medium. For this purpose, the bitstreams from layer 1 are divided into blocks or frames.|
|`1.Physical`|The transmission techniques used are, for example, electrical signals, optical signals, or electromagnetic waves. Through layer 1, the transmission takes place on wired or wireless transmission lines.|

---

The layers `2-4` are `transport oriented`, and the layers `5-7` are `application oriented` layers. In each layer, precisely defined tasks are performed, and the interfaces to the neighboring layers are precisely described. Each layer offers services for use to the layer directly above it. To make these services available, the layer uses the services of the layer below it and performs the tasks of its layer.

If two systems communicate, all seven layers of the `OSI` model are run through at least `twice`, since both the sender and the receiver must take the layer model into account. Therefore, a large number of different tasks must be performed in the individual layers to ensure the communication's security, reliability, and performance.

When an application sends a packet to the other system, the system works the layers shown above from layer `7` down to layer `1`, and the receiving system unpacks the received packet from layer `1` up to layer `7`.