***Data communications are the exchange of data between two devices via some***
***form of transmission medium.*** Effectiveness depends on
1. Delivery - System must deliver data to the correct destination
2. Accuracy - System must deliver data accurately and must be unaltered
3. Timeliness - Data must be delivered on time without big delays
4. Jitter - Jitter is the variation in packet arrival time. The delivery of packets must be regular without big gaps between to prevent audio/video buffering

A data communication network has 5 components
1. Message
2. Sender
3. Receiver
4. Transmission medium
5. Protocol: A set of rules that govern data communication. It is an agreement between communicating devices.
Data can be text (unicode, ASCII), numbers, images (encoded in RGB or YCM), audio or video

## Data Flow
Communication between devices varies based on task and type of device.
1. **Simplex mode:** Unidirectional communication where one devices is sender and other is receiver. Ex: Keyboard-computer, Monitor-computer. 
2. **Half-duplex:** Each device can receive and transmit but not both at the same time. When one is transmitting the other has to wait and receive. Ex: Walkie-talkie
3. **Full-duplex:** Both devices can send and receive simultaneously. Ex: Telephone
![[Pasted image 20250324124124.png]]

## Networks
***A network is the interconnection of a set of devices capable of communication.*** Normal devices are called **hosts** while routers, switches and modems are called **connecting devices.**
Network criteria tells quality of network
1. **Performance:** The capability of a network to send and receive packets, the volume of packets it can handle, etc.
	- *Transit time:* the time required for a packet to reach its destination
	- *Response time:* the time between sending a packet and receiving a reply
	- *Throughput:* amount of data that can be sent in a network
	- *Delay:* the time taken for packets to reach destination. More throughput increases congestion which increases delay
2. **Reliability:** Tendency of a network to fail, and the time it takes to recover
3. **Security:** If the network can protect data from unauthorized access and damage

### Type of Connection
1. **Point to point connection (p2p):** A dedicated link between 2 devices that allows communication only between them
2. **Multipoint connection:** Multiple devices share a link
![[Pasted image 20250324124112.png]]
### Network topology
***The way a network is laid out physically is called network topology***
1. **Mesh topology:** Every device is connected to every other device. 
	- Each device should have `n-1` ports to connect to the other devices
	- number of simplex links needed `n(n-1)`
	- number of duplex links is `n(n-1)/2`
	- *Advantage:* 
		- No traffic problems since device-pair has its own link to communicate from
		- If a link breaks, other links can be used to reroute traffic
		- Easy to identify a broken link and fix it. Makes it more robust
		- High privacy since each device has its own isolated link that cannot be accessed. Compromised links can also be avoided by rerouting
	- *Disadvantage:* High amount of cabling and i/o ports make it expensive and sometimes physically not possible. 
2. **Star topology:** All devices connect to a *central hub* through a p2p link
	- Each device requires 1 port (connected only to the hub).  
	- The hub/switch needs `n` ports (one per device).  
	- **Number of links:** `n` (one per device).  
	- *Advantage:*  
		- Easy to install, manage, and expand (just add new connections to the hub).  
		- Failure of one link does not affect others (isolated faults).  
		- Centralized control simplifies monitoring & troubleshooting.  
	- *Disadvantage:*  
		- ==Hub/switch is a single point of failure== —if it fails, the whole network goes down.  
		- Higher cabling cost than bus (each device needs a separate cable to the hub).  
		- Performance depends on the hub/switch capacity (can become a bottleneck).  
3. **Bus topology:** All devices are connected to a single central cable (the *bus* or *backbone*). hence they have multi-point communication with all devices.
	- Each device connects to the bus using a *tap/drop line* which connects to the core.
	- Only one device can transmit data at a time (requires collision detection or token passing).
	- Terminators are required at both ends of the bus to prevent signal reflection.
	- *Number of links:* `n` taps with 1 backbone
	- *Advantage:*
		- Easy to install
		- Backbone can be laid on the shortest path to all devices and the tap can be small
	- *Disadvantage:*
		- ==Single point of failure==—if the backbone breaks, the entire network fails because of reflection at the breakpoint make. this prevents devices on the same side from also communicating
		- Adding more devices is hard. Backbone may need to be relaid
		- Adding more taps causes *signal reflection* which drops quality
		- There’s a limit to the length of the bus since signal strength drops over long distances
4. **Ring topology:** Each device has a dedicated p2p communication with the devices. Signals move in 1 direction in a link from neighbour to neighbour until it reaches its destination