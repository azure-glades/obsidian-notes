Store and forward packet switching → how a packet travels from one router to the other
Network layer abstracts the underlying complexity of routers, topology and type of network.
- Network layer is the post-office that takes in letters with addresses and sends them. The sender does not see the vans and trucks that carry letters (data link and physical layer) because they happen behind the post-office doors
Most commonly used address in TCP/[IP] → [[Network Layer/Addressing/IPv4]]
# Network layer services
Network layer acts as an abstraction layer that hides and provides interconnectivity between diverse network topologies and structures. It’s responsible for sending packets to the destination using logical addresses, routing the packets and ensuring they reach, error and flow control and to manage traffic and secure transmission.
## 1. Packetization
Encapsulates payload (message) from transport layer into *packets* which are the mode of data transmission in network layer.
- *Source host* receives payload from upper layer and adds a header which contains the source and destination addresses + other info and sends it to the data-link layer. If the message is too big it is fragmented to multiple packets and transmitted
- *Destination host* receives frame from data-link layer and decapsulates the packet to send it to upper layer. If the message is fragmented to multiple packets, it waits to collect all packets, arranges them and then sends it to higher layer.
Routers cannot change addresses or decapsulate the packet unless it is for fragmentation

## 2. Routing and Forwarding
1. **Routing:** Responsible for finding an efficient route to send the packet from source to destination. Uses many routing algos/protocols that are run before transmission, to accomplish this. Routing creates the decision tables/routing tables for a router.
	- Depending on the type of connection, there is [[Unicast Routing]] and [[Multicast Routing]] and [[Broadcast Routing]]
2. **Forwarding:** Forwarding is the decision done by each router to send the packet. This forwarding is done by consulting the decision table/routing table.![[Pasted image 20250408102742.png]]
## 3. Other services
1. **Error control**
2. **Flow control**
3. **Congestion control**
4. **Quality of Service**
5. **Security**

# Performance
Delay, throughput, packet loss and [[congestion]]
# Packet Switching
##  Datagram: Connectionless service
- Packets are routed independently of each other, each packet finds its own way through the network
- Ex: *UDP*
- forwarding decision is based only on destination of packet
- called datagram → datagram network. hence it is called datagram packet switching
![[Pasted image 20250402194046.png]]
![[Pasted image 20250402194055.png]]



## Virtual Network: Connection-oriented service
- A set of links/logical path is set up and all packets travel this route (VLAN)
- Ex: *TCP*
- similar to circuit switching but no physical link is actually set and reserved. It behaves like a virtual circuit which abstracts some underlying stuff.
- forwarding decision is based on flow label. A flow label identifies the virtual path/circuit that a packet must follow (it is a virtual circuit identifier)
- There are 4 phases
	- Setup phase → send a request and ack packet to tell all routers to setup a virtual circuit
	- Data transfer phase
	- Teardown phase → teardown packet is sent along with a confirmation packet received that tells routers to delete the circuit entries
![[Pasted image 20250402194114.png]]
![[Pasted image 20250402194126.png]]

> Difference between connection and connection-less switching
> ![[Pasted image 20250422112418.png]]

