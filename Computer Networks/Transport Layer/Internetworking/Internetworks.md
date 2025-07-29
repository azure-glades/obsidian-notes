When many different and distinct networks are connected together to allow exchange of data between them, it is called inter-networking.

The problem of internetworking:
- Networks have many different physical media
- Networks function differently - connection/connection-oriented
- Some networks may not have features like broadcasting
- Networks have different QoS goals, some may be best-effort services
This makes it difficult to connect different networks together

Solved by:
1. Building devices that translate packets between networks
2. Build a common overhead layer on top of the different networks that makes itself understood to underlying networks - This is now the [[TCP - Transmission Control Protocol]] and [[IP - Internet Protocol]] suite

These two tasks are run by interconnection devices
- **Repeaters, Hubs, Switches, Bridges:**  
    These devices operate at the physical and link layers. Repeaters and hubs simply forward bits and do not interpret higher-level protocols. Switches and bridges work at the link layer and can *only connect similar types of networks*, with limited protocol translation (e.g., between different Ethernet speeds). They are not suitable for connecting fundamentally different networks.
- **Routers:**  
    Routers operate at the network layer. They extract packets from one network’s frame, examine the network (IP) address, and forward the packet to the next network, encapsulating it in the appropriate frame for that network. Routers are the primary devices enabling internetworking between dissimilar networks (e.g., Wi-Fi, MPLS, Ethernet).
- **Multiprotocol Routers:**  
    These routers can handle multiple network protocols (e.g., both IPv4 and IPv6). They may attempt protocol translation, but this is often incomplete or impractical for fundamentally different protocols. More commonly, they forward packets to higher protocol layers for handling, but this restricts interoperability to applications using those higher protocols (like TCP)

How data moves across internetworks
1. **Encapsulation-Decapsulation**
    - At each network boundary, the packet is removed from the current network’s frame, and a new frame suitable for the next network is applied.
    - For example, a packet may start in an 802.11 (Wi-Fi) frame, be extracted by a router, and then encapsulated in an MPLS frame for the next segment, and finally in an Ethernet frame for delivery to the destination. 
    - Effectively, the intermediate network is not known to the source or destination since it is handled by IP. Effectively it creates a [[Tunnelling]], a seamless connection that joins 2 networks (it appears as-though the destination is on the same network as the source)
2. **Addressing:**
    - The network layer (IP) address is used throughout the journey, ensuring the packet can be routed across different underlying networks, each with its own addressing scheme
3. **Handling Differences:**
    - **[[Connected or Connectionless Internetworking]]** If a packet moves from a connectionless network (e.g., Wi-Fi) to a connection-oriented one (e.g., MPLS), a virtual circuit is established for the latter segment
    - **[[Fragmentation during Routing]]:** If the packet size exceeds the maximum allowed by a network (e.g., Ethernet’s smaller MTU compared to Wi-Fi), the packet is fragmented and reassembled at the destination

# Internetwork Routing
Intenetworks have 2 levels of routing algorithms
- To route packets within a network - Intradomain
	- Usually a link-state protocol like [[OSPF -Interior Gateway Routing Protocol]]
- To route packets between networks - Interdomain
	- Handled by [[BGP - Exterior Gateway Routing Protocol]] which follows strict routing policies
All networks in an internetwork run autonomously, as a **Autonomous System (AS)**, like an ISP which manages all devices that connect to it for internet access. The internet consists of many such autonomous systems




