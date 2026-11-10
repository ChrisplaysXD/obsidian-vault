### Network Types
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
## Network Topology
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
## Point-to-Point

 The simplest network topology with a dedicated connection between two hosts is the `point-to-point` topology. In this topology, a direct and straightforward physical link exists only between `two hosts`. These two devices can use these connections for mutual communication.

`Point-to-point` topologies are the basic model of traditional telephony and must not be confused with `P2P` (`Peer-to-Peer` architecture).

#### Point-To-Point Topology

![image](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/34/redesigned/topo_p2p.png)