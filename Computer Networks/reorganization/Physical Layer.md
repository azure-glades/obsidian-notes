# Physical layer
The Internet -> Started as ARPANET

Accessing the internet
1. Using telephone network: Dial-up service, DSL service
2. Cable networks: Circuit switching and packet switching

TCP/IP suite ![[Pasted image 20250312093157.png]]
Layered architecture: Physical layer -> Data link layer -> Network Layer -> Transport layer -> Application layer
- Routers, Data links
- Routers are network layer <- Switches are data link layer
- Routers always route the data, switch only forwards the data

1. Physical layer
	- *Smallest unit of data handled by physical layer is bits*
2. Data link layer
	- *Smallest unit of data handled by data link layer is frames*
	- Encapsulation: Bundles the bits from physical layer and sends to network layer
	- Decapsulation: Receives packets from the network layer and breaks them into frames
3. Transport layer
	- ICMP - internet control message protocol - report problems when packet routing
	- IGMP - internet group management protocol - ip multitasking
	- DHCP - dynamic host configuration protocol - get network layer address of host
	- ARP - address resolution protocol - finding link-layer address
4. Application layer

Muticast transmission
Unicast transmission

transport layer
applicaion layer→ uses transport layer to give applications access to network

OSI model: 
![[Pasted image 20250312093222.png]]
application → presentation → session → transport → network → datalink → physical

OSI vs TCP/IP

## 12.03.2025
- Serial transmission
	- synchronous
	- asynchronous
	- isochronous : multimedia transmission (images audio text)
- Parallel transmission