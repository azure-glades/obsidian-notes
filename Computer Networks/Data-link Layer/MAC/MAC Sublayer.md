***The MAC (Media Access Control) sublayer is responsible for managing access to the physical transmission medium and facilitating communication between devices in a network.***

The MAC sublayer controls the NIC and other hardware that is responsible for sending and receiving data on the wired or wireless LAN/MAN medium.
# Services
- The MAC sublayer provides data encapsulation:
	- **Frame delimiting** - The framing process provides important delimiters to identify fields within a frame. These delimiting bits provide synchronization between the transmitting and receiving nodes.
	- **Addressing** - Provides source and destination addressing for transporting the Layer 2 frame between devices on the same shared medium.
	- **Error detection** - Includes a trailer used to detect transmission errors.
- The MAC sublayer also provides media access control through [[CSMA]], allowing multiple devices to communicate over a shared (half-duplex) medium. Full-duplex communications do not require access control.


# Access Control Methods
A *multiaccess network* is a network that can have two or more end devices attempting to access the network simultaneously (Ex: Ethernet LAN/WAN)
1. **Contention-based access:** In contention-based multiaccess networks, all nodes are operating in half-duplex, competing for the use of the medium (only 1 device can send at a time). Uses [[CSMA]]
	- CSMA/CD (Collision detection) → bus ethernet LAN
	- CSMA/CA (Collision Avoidance) → Wireless LAN
2. **Controlled access:** Each node has its own time to use the medium. These deterministic types of legacy networks are inefficient because a device must wait its turn to access the medium.
	- Legacy Token Ring
	- Legacy ARCNET
> These are no longer used because networks are now full-duplex