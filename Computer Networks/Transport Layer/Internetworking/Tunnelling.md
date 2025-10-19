A special case of internetworking where the source and destination are on the same type of network but there is a different network inbetween. This is solved by tunnelling


![[Pasted image 20250619164002.png]]
Ex:
Packets are transferred from IPv6 to IPv4 and back to IPv6.
Basically packets are transferred in IPv4 form.
Packets cannot be accessed by any device on the IPv4 network since its data is an IPv6.

Steps: Encapsulation → Transmission → Decapsulation

Ends up acting as if the destination is on the source network itself
This tunnel can be maintained for long durations of time depending on the necessity

The resulting network is called an *overlay* because it is overlaid on the base network

Characteristics:
- The source/destination networks operate identically, oblivious to the intermediary network's protocols
- Encapsulated data is inaccessible to devices on the intermediary network
- Tunnels can persist indefinitely (VPNs)