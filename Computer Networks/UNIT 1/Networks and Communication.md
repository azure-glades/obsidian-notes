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
5. [[Protocol Suite]]: A set of rules that govern data communication. It is an agreement between communicating devices.
Data can be text (unicode, ASCII), numbers, images (encoded in RGB or YCM), audio or video

## Data Flow
Communication between devices varies based on task and type of device.
1. **Simplex mode:** Unidirectional communication where one devices is sender and other is receiver. Ex: Keyboard-computer, Monitor-computer. 
2. **Half-duplex:** Each device can receive and transmit but not both at the same time. When one is transmitting the other has to wait and receive. Ex: Walkie-talkie
3. **Full-duplex:** Both devices can send and receive simultaneously. Ex: Telephone
![[Pasted image 20250324124124.png]]

## Network structure
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
![[Pasted image 20250324191605.png]]
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
![[Pasted image 20250324191623.png]]
3. **Bus topology:** All devices are connected to a single central cable (the *bus* or *backbone*). hence they have multi-point communication with all devices.
	- Each device connects to the bus using a *tap/drop line* which connects to the core.
	- Only one device can transmit data at a time (requires collision detection or token passing).
	- Terminators are required at both ends of the bus to prevent signal reflection.
	- *Number of links:* `n` taps with 1 backbone
	- *Advantage:*
		- Easy to install
		- Backbone can be laid on the shortest path to all devices and the tap can be small
	- *Disadvantage:*
		- ==Backbone is single point of failure==—if the backbone breaks, the entire network fails because of reflection at the breakpoint make. this prevents devices on the same side from also communicating
		- Adding more devices is hard. Backbone may need to be relaid
		- Adding more taps causes *signal reflection* which drops quality
		- There’s a limit to the length of the bus since signal strength drops over long distances
![[Pasted image 20250324191635.png]]
4. **Ring topology:** Each device has a dedicated p2p communication with the devices. Signals move in 1 direction in a link from neighbour to neighbour until it reaches its destination
	- *Unidirectional traffic* so each device has 1 sender neighbour and 1 receiver neighbour
	- Each device has a repeater to boost signal strength
	- `n` repeater-device links and 1 ring
	- *Advantage:*
		- Easy to install and add/remove new devices
		- Easy to isolate faults since it is possible to know between what two devices a fault sits.
	- *Disadvantage:*
		- ==Ring is a single point of failure== which can bring down the network. Mitigated with dual-ring topology
![[Pasted image 20250324191649.png]]
## Network types
Distinguished based on size
### LAN
Private network restricted to a company or a campus with its own set of rules and a common firewall. Usually bus or star topology with a common central switch that connects to all devices and to the internet. Most LANs are connected to other LANs and WANs
![[Pasted image 20250324191926.png]]

### WAN
WAN connects larger geographical areas and includes many LANs within it
1. **Point to point WAN:** 2 communicating devices of WANs(router/switch) are connect by a p2p link allowing the 2 WANs to share data
![[Pasted image 20250324192733.png]]
2. **Switched WAN:** Several p2p WANs connected by switches
![[Pasted image 20250324192722.png]]
3. **Internetwork:** When multiple LANs and WANs are connected they’re called an Internetwork since it allows for inter-network communication (i.e between different types of networks). Ex: Multiple offices in a company (with their own LAN, and sometimes regional clusters with WANs) can be set-up to have a network completely isolated from the world wide web. This is a private internet network where computers from the world wide web cannot access this internetwork.

| WAN                                                                                       | LAN                                                                 |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Wider geographical area                                                                   | Small area like a campus or company                                 |
| Run by ISPs which give service to people and companies                                    | Managed by the organization                                         |
| WAN interconnects hosts and also connecting devices (like *switches, modems and routers*) | LAN interconnects host devices within a campus/company              |
| Has to adhere to privacy laws and legislation                                             | Companies have complete control on the usage and rules within a LAN |

## Switching
A switch forwards data from one network to another network. ISPs manage switches. The forwarding of data between networks is called switching.
1. **Circuit switching:** When a dedicated p2p link (called a *circuit*) is available between 2 networks but access is controlled by a switch. The switch hence turns the link on/off allowing signals to be sent/received and does not store/read the signal. 
	- Communication is directly between the host devices
2. **Packet switching:** No direct link exists between the devices of network. Instead they communicate with the router/switch which has to send the data itself to the other network.
	- The router/switch stores/buffers the packets and forwards them to routers/switches.
	- More common since it enables full use of network capacity.