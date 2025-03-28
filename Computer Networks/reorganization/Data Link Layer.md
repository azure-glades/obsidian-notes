In the **TCP/IP model**, the **link layer** (also called the network access layer) is responsible for maintaining connection to hosts and connecting devices. Routers and switches in this layer are responsible for finding the best link to send packets (called *frames*) between devices.
1. **Local Network Communication**: It ensures data is transmitted between devices on the same physical network (e.g., Ethernet or Wi-Fi).
2. **Framing**: Encapsulates data into frames for transmission.
3. **Addressing**: Uses hardware (MAC) addresses to identify devices on the network.
4. **Error Detection**: Identifies errors in transmitted frames but does not always correct them.
5. **Media Access Control (MAC)**: Manages how devices share access to the physical medium to avoid collisions.
![[Pasted image 20250312093623.png]]
> how are data link address layers identified? how does a router/switch know which device to send the frames to?

Data link layer manages 3 different types of links, i.e point-to-point links, multi-point links and broadcast links

Data link layer has 2 sublayers:
- [[Data Link Control (DLC) Layer]] → Upper layer
- [[Media Access Control (MAC) Layer]] → Lower layer
broadcast links have both DLC and MAC![[Pasted image 20250312095549.png]]

IP address stores the destination address of a datagram (network packet) → another addressing mechanism needs to be used » this is *link address/physical address/MAC address*