***The MAC (Media Access Control) sublayer is responsible for managing access to the physical transmission medium and facilitating communication between devices in a network.***
# Services
- Determines which device can access the shared transmission medium at any given time.  
- Prevents collisions in shared network topologies using methods like ALOHA and [[CSMA]].
- Detects collisions in shared media and initiates retransmission when required.  
	- Uses techniques such as backoff algorithms to resolve collisions. 
- Supports multiple logical connections over a single physical medium by managing frame addressing and delivery.  
- Uses *MAC addresses* to uniquely identify devices on a network, enabling unicast, multicast, or broadcast communication.
	- Provides abstraction of physical layer complexities by interfacing through a media-independent interface.  
	- Ensures compatibility between different physical layer implementations.  
	- Maps higher-layer logical addresses to physical MAC addresses for accurate data delivery within a local network.

# Media Access
There are many ways in which access to media can be handed over to stations. When stations compete for access to the medium, it is called *Contention*
1. Random access: Any station that wants to transmit can access and transmit. The biggest issue is collisions when multiple stations transmit together and the data gets corrupted
2. Controlled access: The stations have to communicate with each other and decide who gets authority to transmit when. Usually done when there is an overseer (primary) station to manage access
- Channelization: When the available bandwidth of a link is shared in time,frequency and code allowing the stations to transmit across different times/frequencies without interfering