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
# The TCP/IP Model
The `TCP/IP` model is also a layered reference model, often referred to as the `Internet Protocol Suite`. The term `TCP/IP` stands for the two protocols `Transmission Control Protocol` (`TCP`) and `Internet Protocol` (`IP`). `IP` is located within the `network layer` (`Layer 3`) and `TCP` is located within the `transport layer` (`Layer 4`) of the `OSI` layer model.

|**Layer**|**Function**|
|---|---|
|`4.Application`|The Application Layer allows applications to access the other layers' services and defines the protocols applications use to exchange data.|
|`3.Transport`|The Transport Layer is responsible for providing (TCP) session and (UDP) datagram services for the Application Layer.|
|`2.Internet`|The Internet Layer is responsible for host addressing, packaging, and routing functions.|
|`1.Link`|The Link layer is responsible for placing the TCP/IP packets on the network medium and receiving corresponding packets from the network medium. TCP/IP is designed to work independently of the network access method, frame format, and medium.|

With `TCP/IP`, every application can transfer and exchange data over any network, and it does not matter where the receiver is located. `IP` ensures that the data packet reaches its destination, and `TCP` controls the data transfer and ensures the connection between data stream and application. The main difference between `TCP/IP` and `OSI` is the number of layers, some of which have been combined.

![Comparison of OSI and TCP/IP models: OSI has 7 layers including Application, Presentation, Session, Transport, Network, Data-Link, and Physical. TCP/IP has 4 layers: Application, Transport, Internet, and Link.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/net_models4.png)

The most important tasks of `TCP/IP` are:

|**Task**|**Protocol**|**Description**|
|---|---|---|
|`Logical Addressing`|`IP`|Due to many hosts in different networks, there is a need to structure the network topology and logical addressing. Within TCP/IP, IP takes over the logical addressing of networks and nodes. Data packets only reach the network where they are supposed to be. The methods to do so are `network classes`, `subnetting`, and `CIDR`.|
|`Routing`|`IP`|For each data packet, the next node is determined in each node on the way from the sender to the receiver. This way, a data packet is routed to its receiver, even if its location is unknown to the sender.|
|`Error & Control Flow`|`TCP`|The sender and receiver are frequently in touch with each other via a virtual connection. Therefore control messages are sent continuously to check if the connection is still established.|
|`Application Support`|`TCP`|TCP and UDP ports form a software abstraction to distinguish specific applications and their communication links.|
|`Name Resolution`|`DNS`|DNS provides name resolution through Fully Qualified Domain Names (FQDN) in IP addresses, enabling us to reach the desired host with the specified name on the internet.|
# Network Layer
The `network layer` (`Layer 3`) of `OSI` controls the exchange of data packets, as these cannot be directly routed to the receiver and therefore have to be provided with routing nodes. The data packets are then transferred from node to node until they reach their target. To implement this, the `network layer` identifies the individual network nodes, sets up and clears connection channels, and takes care of routing and data flow control. When sending the packets, addresses are evaluated, and the data is routed through the network from node to node. There is usually no processing of the data in the layers above the `L3` in the nodes. Based on the addresses, the routing and the construction of routing tables are done.

In short, it is responsible for the following functions:

- `Logical Addressing`
- `Routing`

Protocols are defined in each layer of `OSI`, and these protocols represent a collection of rules for communication in the respective layer. They are transparent to the protocols of the layers above or below. Some protocols fulfill tasks of several layers and extend over two or more layers. The most used protocols on this layer are:

- `IPv4` / `IPv6`
- `IPsec`
- `ICMP`
- `IGMP`
- `RIP`
- `OSPF`

It ensures the routing of packets from source to destination within or outside a subnet. These two subnets may have different addressing schemes or incompatible addressing types. In both cases, the data transmission in each case goes through the entire communication network and includes routing between the network nodes. Since direct communication between the sender and the receiver is not always possible due to the different subnets, packets must be forwarded from nodes (routers) that are on the way. Forwarded packets do not reach the higher layers but are assigned a new intermediate destination and sent to the next node.
# IP Addresses

Each host in the network located can be identified by the so-called `Media Access Control` address (`MAC`). This would allow data exchange within this one network. If the remote host is located in another network, knowledge of the `MAC` address is not enough to establish a connection. Addressing on the Internet is done via the `IPv4` and/or `IPv6` address, which is made up of the `network address` and the `host address`.

It does not matter whether it is a smaller network, such as a home computer network, or the entire Internet. The IP address ensures the delivery of data to the correct receiver. We can imagine the representation of `MAC` and `IPv4` / `IPv6` addresses as follows:

- `IPv4` / `IPv6` - describes the unique postal address and district of the receiver's building.
- `MAC` - describes the exact floor and apartment of the receiver.

It is possible for a single IP address to address multiple receivers (broadcasting) or for a device to respond to multiple IP addresses. However, it must be ensured that each IP address is assigned only once within the network.
## IPv4 Structure

The most common method of assigning IP addresses is `IPv4`, which consists of a `32`-bit binary number combined into `4 bytes` consisting of `8`-bit groups (`octets`) ranging from `0-255`. These are converted into more easily readable decimal numbers, separated by dots and represented as dotted-decimal notation.

Thus an IPv4 address can look like this:

|**Notation**|**Presentation**|
|---|---|
|Binary|0111 1111.0000 0000.0000 0000.0000 0001|
|Decimal|127.0.0.1|

Each network interface (network cards, network printers, or routers) is assigned a unique IP address.

The `IPv4` format allows 4,294,967,296 unique addresses. The IP address is divided into a `host part` and a `network part`. The `router` assigns the `host part` of the IP address at home or by an administrator. The respective `network administrator` assigns the `network part`. On the Internet, this is `IANA`, which allocates and manages the unique IPs.

In the past, further classification took place here. The IP network blocks were divided into `classes A - E`. The different classes differed in the host and network shares' respective lengths.

|**`Class`**|**Network Address**|**First Address**|**Last Address**|**Subnetmask**|**CIDR**|**Subnets**|**IPs**|
|---|---|---|---|---|---|---|---|
|`A`|1.0.0.0|1.0.0.1|127.255.255.255|255.0.0.0|/8|127|16,777,214 + 2|
|`B`|128.0.0.0|128.0.0.1|191.255.255.255|255.255.0.0|/16|16,384|65,534 + 2|
|`C`|192.0.0.0|192.0.0.1|223.255.255.255|255.255.255.0|/24|2,097,152|254 + 2|
|`D`|224.0.0.0|224.0.0.1|239.255.255.255|Multicast|Multicast|Multicast|Multicast|
|`E`|240.0.0.0|240.0.0.1|255.255.255.255|reserved|reserved|reserved|reserved|

## Subnet Mask

A further separation of these classes into small networks is done with the help of `subnetting`. This separation is done using the `netmasks`, which is as long as an IPv4 address. As with classes, it describes which bit positions within the IP address act as `network part` or `host part`.

|**Class**|**Network Address**|**First Address**|**Last Address**|**`Subnetmask`**|**CIDR**|**Subnets**|**IPs**|
|---|---|---|---|---|---|---|---|
|**A**|1.0.0.0|1.0.0.1|127.255.255.255|`255.0.0.0`|/8|127|16,777,214 + 2|
|**B**|128.0.0.0|128.0.0.1|191.255.255.255|`255.255.0.0`|/16|16,384|65,534 + 2|
|**C**|192.0.0.0|192.0.0.1|223.255.255.255|`255.255.255.0`|/24|2,097,152|254 + 2|
|**D**|224.0.0.0|224.0.0.1|239.255.255.255|`Multicast`|Multicast|Multicast|Multicast|
|**E**|240.0.0.0|240.0.0.1|255.255.255.255|`reserved`|reserved|reserved|reserved|

## Network and Gateway Addresses

The `two` additional `IPs` added in the `IPs column` are reserved for the so-called `network address` and the `broadcast address`. Another important role plays the `default gateway`, which is the name for the IPv4 address of the `router` that couples networks and systems with different protocols and manages addresses and transmission methods. It is common for the `default gateway` to be assigned the first or last assignable IPv4 address in a subnet. This is not a technical requirement, but has become a de-facto standard in network environments of all sizes.

|**Class**|**Network Address**|**`First Address`**|**Last Address**|**Subnetmask**|**CIDR**|**Subnets**|**`IPs`**|
|---|---|---|---|---|---|---|---|
|A|1.0.0.0|`1.0.0.1`|127.255.255.255|255.0.0.0|/8|127|16,777,214 `+ 2`|
|B|128.0.0.0|`128.0.0.1`|191.255.255.255|255.255.0.0|/16|16,384|65,534 `+ 2`|
|C|192.0.0.0|`192.0.0.1`|223.255.255.255|255.255.255.0|/24|2,097,152|254 `+ 2`|
|D|224.0.0.0|`224.0.0.1`|239.255.255.255|Multicast|Multicast|Multicast|Multicast|
|E|240.0.0.0|`240.0.0.1`|255.255.255.255|reserved|reserved|reserved|reserved|

## Broadcast Address

The `broadcast` IP address's task is to connect all devices in a network with each other. `Broadcast` in a network is a message that is transmitted to all participants of a network and does not require any response. In this way, a host sends a data packet to all other participants of the network simultaneously and, in doing so, communicates its `IP address`, which the receivers can use to contact it. This is the `last IPv4` address that is used for the `broadcast`.

|**Class**|**Network Address**|**First Address**|**`Last Address`**|**Subnetmask**|**CIDR**|**Subnets**|**IPs**|
|---|---|---|---|---|---|---|---|
|A|1.0.0.0|1.0.0.1|`127.255.255.255`|255.0.0.0|/8|127|16,777,214 + 2|
|B|128.0.0.0|128.0.0.1|`191.255.255.255`|255.255.0.0|/16|16,384|65,534 + 2|
|C|192.0.0.0|192.0.0.1|`223.255.255.255`|255.255.255.0|/24|2,097,152|254 + 2|
|D|224.0.0.0|224.0.0.1|`239.255.255.255`|Multicast|Multicast|Multicast|Multicast|
|E|240.0.0.0|240.0.0.1|`255.255.255.255`|reserved|reserved|reserved|reserved|

## Binary system

The binary system is a number system that uses only two different states that are represented into two numbers (`0` and `1`) opposite to the decimal-system (0 to 9).

An IPv4 address is divided into 4 octets, as we have already seen. Each `octet` consists of `8 bits`. Each position of a bit in an octet has a specific decimal value. Let's take the following IPv4 address as an example:

- IPv4 Address: `192.168.10.39`

Here is an example of how the `first octet` looks like:

#### 1st Octet - Value: 192

        shellsession
`Values:         128  64  32  16  8  4  2  1 Binary:           1   1   0   0  0  0  0  0`

If we calculate the sum of all these values for each octet where the bit is set to `1`, we get the sum:

|**Octet**|**Values**|**Sum**|
|---|---|---|
|1st|128 + 64 + 0 + 0 + 0 + 0 + 0 + 0|= `192`|
|2nd|128 + 0 + 32 + 0 + 8 + 0 + 0 + 0|= `168`|
|3rd|0 + 0 + 0 + 0 + 8 + 0 + 2 + 0|= `10`|
|4th|0 + 0 + 32 + 0 + 0 + 4 + 2 + 1|= `39`|

The entire representation from binary to decimal would look like this:

#### IPv4 - Binary Notation

        shellsession
`Octet:             1st         2nd         3rd         4th Binary:         1100 0000 . 1010 1000 . 0000 1010 . 0010 0111 Decimal:           192    .    168    .     10    .     39`

- IPv4 Address: `192.168.10.39`

This addition takes place for each octet, which results in a decimal representation of the `IPv4 address`. The subnet mask is calculated in the same way.

#### IPv4 - Decimal to Binary

        shellsession
`Values:         128  64  32  16  8  4  2  1 Binary:           1   1   1   1  1  1  1  1`

|**Octet**|**Values**|**Sum**|
|---|---|---|
|1st|128 + 64 + 32 + 16 + 8 + 4 + 2 + 1|= `255`|
|2nd|128 + 64 + 32 + 16 + 8 + 4 + 2 + 1|= `255`|
|3rd|128 + 64 + 32 + 16 + 8 + 4 + 2 + 1|= `255`|
|4th|0 + 0 + 0 + 0 + 0 + 0 + 0 + 0|= `0`|

#### Subnet Mask

        shellsession
`Octet:             1st         2nd         3rd         4th Binary:         1111 1111 . 1111 1111 . 1111 1111 . 0000 0000 Decimal:           255    .    255    .    255    .     0`

- IPv4 Address: `192.168.10.39`
- Subnet mask: `255.255.255.0`

## CIDR

`Classless Inter-Domain Routing` (`CIDR`) is a method of representation and replaces the fixed assignment between IPv4 address and network classes (A, B, C, D, E). The division is based on the subnet mask or the so-called `CIDR suffix`, which allows the bitwise division of the IPv4 address space and thus into `subnets` of any size. The `CIDR suffix` indicates how many bits from the beginning of the IPv4 address belong to the network. It is a notation that represents the `subnet mask` by specifying the number of `1`-bits in the subnet mask.

Let us stick to the following IPv4 address and subnet mask as an example:

- IPv4 Address: `192.168.10.39`
- Subnet mask: `255.255.255.0`

Now the whole representation of the IPv4 address and the subnet mask would look like this:

- CIDR: `192.168.10.39/24`

The CIDR suffix is, therefore, the sum of all ones in the subnet mask.

        shellsession
`Octet:             1st         2nd         3rd         4th Binary:         1111 1111 . 1111 1111 . 1111 1111 . 0000 0000 (/24) Decimal:           255    .    255    .    255    .     0`
# Subnetting

The division of an address range of IPv4 addresses into several smaller address ranges is called `subnetting`.

A subnet is a logical segment of a network that uses IP addresses with the same network address. We can think of a subnet as a labeled entrance on a large building corridor. For example, this could be a glass door that separates various departments of a company building. With the help of subnetting, we can create a specific subnet by ourselves or find out the following outline of the respective network:

- `Network address`
- `Broadcast address`
- `First host`
- `Last host`
- `Number of hosts`

Let us take the following IPv4 address and subnet mask as an example:

- IPv4 Address: `192.168.12.160`
- Subnet Mask: `255.255.255.192`
- CIDR: `192.168.12.160/26`

We already know that an IP address is divided into the `network part` and the `host part`.

#### Network Part

|**Details of**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**Decimal**|
|---|---|---|---|---|---|
|IPv4|`1100 0000`|`1010 1000`|`0000 1100`|`10`10 0000|192.168.12.160`/26`|
|Subnet mask|`1111 1111`|`1111 1111`|`1111 1111`|`11`00 0000|`255.255.255.192`|
|Bits|/8|/16|/24|/32||

In subnetting, we use the subnet mask as a template for the IPv4 address. From the `1`-bits in the subnet mask, we know which bits in the IPv4 address `cannot` be changed. These are `fixed` and therefore determine the "main network" in which the subnet is located.

#### Host Part

|**Details of**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**Decimal**|
|---|---|---|---|---|---|
|IPv4|1100 0000|1010 1000|0000 1100|10`10 0000`|192.168.12.160/26|
|Subnet mask|1111 1111|1111 1111|1111 1111|11`00 0000`|255.255.255.192|
|Bits|/8|/16|/24|/32||

The bits in the `host part` can be changed to the `first` and `last` address. The first address is the `network address`, and the last address is the `broadcast address` for the respective subnet.

The `network address` is vital for the delivery of a data packet. If the `network address` is the same for the source and destination address, the data packet is delivered within the same subnet. If the network addresses are different, the data packet must be routed to another subnet via the `default gateway`.

The `subnet mask` determines where this separation occurs.

#### Separation Of Network & Host Parts

|**Details of**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**Decimal**|
|---|---|---|---|---|---|
|IPv4|1100 0000|1010 1000|0000 1100|10`\|`10 0000|192.168.12.160/26|
|Subnet mask|`1111 1111`|`1111 1111`|`1111 1111`|`11\|`00 0000|255.255.255.192|
|Bits|/8|/16|/24|/32||

#### Network Address

So if we now set all bits to `0` in the `host part` of the IPv4 address, we get the respective subnet's `network address`.

|**Details of**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**Decimal**|
|---|---|---|---|---|---|
|IPv4|1100 0000|1010 1000|0000 1100|10`\|00 0000`|`192.168.12.128`/26|
|Subnet mask|`1111 1111`|`1111 1111`|`1111 1111`|`11\|`00 0000|255.255.255.192|
|Bits|/8|/16|/24|/32||

#### Broadcast Address

If we set all bits in the `host part` of the IPv4 address to `1`, we get the `broadcast address`.

| **Details of** | **1st Octet** | **2nd Octet** | **3rd Octet** | **4th Octet** | **Decimal**         |
| -------------- | ------------- | ------------- | ------------- | ------------- | ------------------- |
| IPv4           | 1100 0000     | 1010 1000     | 0000 1100     | 10`\|11 1111` | `192.168.12.191`/26 |
| Subnet mask    | `1111 1111`   | `1111 1111`   | `1111 1111`   | `11\|`00 0000 | 255.255.255.192     |
| Bits           | /8            | /16           | /24           | /32           |                     |

Since we now know that the IPv4 addresses `192.168.12.128` and `192.168.12.191` are assigned, all other IPv4 addresses are accordingly between `192.168.12.129-190`. Now we know that this subnet offers us a total of `64 - 2` (network address & broadcast address) or `62` IPv4 addresses that we can assign to our hosts.

|**Hosts**|**IPv4**|
|---|---|
|Network Address|`192.168.12.128`|
|First Host|`192.168.12.129`|
|Other Hosts|`...`|
|Last Host|`192.168.12.190`|
|Broadcast Address|`192.168.12.191`|

## Subnetting Into Smaller Networks

Let us now assume that we, as administrators, have been given the task of dividing the subnet assigned to us into 4 additional subnets. Thus, it is essential to know that we can only divide the subnets based on the binary system.

|**Exponent**|**Value**|
|---|---|
|2`^0`|= 1|
|2`^1`|= 2|
|2`^2`|= 4|
|2`^3`|= 8|
|2`^4`|= 16|
|2`^5`|= 32|
|2`^6`|= 64|
|2`^7`|= 128|
|2`^8`|= 256|

Therefore we can divide the `64 hosts` we know by `4`. The `4` is equal to the exponent 2`^2` in the binary system, so we find out the number of bits for the subnet mask by which we have to extend it. So we know the following parameters:

- Subnet: `192.168.12.128/26`
- Required Subnets: `4`

Now we increase/expand our subnet mask by `2 bits` from `/26` to `/28`, and it looks like this:

|**Details of**|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|**Decimal**|
|---|---|---|---|---|---|
|IPv4|1100 0000|1010 1000|0000 1100|1000`\|` 0000|192.168.12.128`/28`|
|Subnet mask|`1111 1111`|`1111 1111`|`1111 1111`|`1111\|` 0000|`255.255.255.240`|
|Bits|/8|/16|/24|/32||

Next, we can divide the `64` IPv4 addresses that are available to us into `4 parts`:

|**Hosts**|**Math**|**Subnets**|**Host range for each subnet**|
|---|---|---|---|
|64|/|4|= `16`|

So we know how big each subnet will be. From now on, we start from the network address given to us (192.168.12.128) and add the `16` hosts `4` times:

|**Subnet No.**|**Network Address**|**First Host**|**Last Host**|**Broadcast Address**|**CIDR**|
|---|---|---|---|---|---|
|1|`192.168.12.128`|192.168.12.129|192.168.12.142|`192.168.12.143`|192.168.12.128/28|
|2|`192.168.12.144`|192.168.12.145|192.168.12.158|`192.168.12.159`|192.168.12.144/28|
|3|`192.168.12.160`|192.168.12.161|192.168.12.174|`192.168.12.175`|192.168.12.160/28|
|4|`192.168.12.176`|192.168.12.177|192.168.12.190|`192.168.12.191`|192.168.12.176/28|

## Mental Subnetting

It may seem like there is a lot of math involved in subnetting, but each octet repeats itself, and everything is a power of two, so there doesn't have to be a lot of memorization. The first thing to do is identify what octet changes.

|**1st Octet**|**2nd Octet**|**3rd Octet**|**4th Octet**|
|---|---|---|---|
|/8|/16|/24|/32|

It is possible to identify what octet of the IP Address may change by remembering those four numbers. Given the Network Address: `192.168.1.1/25`, it is immediately apparent that 192.168.2.4 would not be in the same network because the `/25` subnet means only the fourth octet may change.

The next part identifies how big each subnet can be but by dividing eight by the network and looking at the `remainder`. This is also called `Modulo Operation (%)` and is heavily utilized in cryptology. Given our previous example of `/25`, `(25 % 8)` would be 1. This is because eight goes into 25 three times (8 * 3 = 24). There is a 1 leftover, which is the network bit reserved for the network mask. There is a total of eight bits in each octet of an IP Address. If one is used for the network mask, the equation becomes 2^(8-1) or 2^7, 128. The table below contains all the numbers.

|**Remainder**|**Number**|**Exponential Form**|**Division Form**|
|---|---|---|---|
|0|256|2^8|256|
|1|128|2^7|256/2|
|2|64|2^6|256/2/2|
|3|32|2^5|256/2/2/2|
|4|16|2^4|256/2/2/2/2|
|5|8|2^3|256/2/2/2/2/2|
|6|4|2^2|256/2/2/2/2/2/2|
|7|2|2^1|256/2/2/2/2/2/2/2|

By remembering the powers of two up to eight, it can become an instant calculation. However, if forgotten, it may be quicker to remember to divide 256 in half the number of times of the remainder.

The tricky part of this is getting the actual IP Address range because 0 is a number and not null in networking. So in our `/25` with 128 IP Addresses, the first range is `192.168.1.0-127`. The first address is the network, and the last is the broadcast address, which means the usable IP Space would become `192.168.1.1-126`. If our IP Address fell above 128, then the `usable ip space` would be 192.168.1.129-254 (128 is the network and 255 is the broadcast).
### question 1
Submit the decimal representation of the subnet mask from the following CIDR: 10.200.20.0/27
answer: 255.255.255.224
tips: 27 mean the first 27 bit is valued 1(network bits) and that left 5 host bit valued 0.
best method (256- the block size)
	find how many bit host left=32-27=5.
	count the block size(total ip)=2<sup>5</sup>=32.
	256-32=<u>224</u>.
### question 2
Submit the broadcast address of the following CIDR: 10.200.20.0/27
answer=10.200.20.31
tips: use the leftover bit method(2<sup>32-cidr</sup>).
/27=32-27=5=2<sup></sup>