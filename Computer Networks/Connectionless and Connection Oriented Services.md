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

