***Data link layer controls how the medium is used***
In the **TCP/IP model**, the **link layer** (also called the network access layer) is responsible for maintaining connection to hosts and connecting devices. Routers and switches in this layer are responsible for finding the best link to send packets (called *frames*) between devices.
1. **Local Network Communication**: It ensures data is transmitted between devices on the same physical network (e.g., Ethernet or Wi-Fi).
2. **Framing**: Encapsulates data into frames for transmission.
3. **Addressing**: Uses hardware (MAC) addresses to identify devices on the network.
4. **Error Detection**: Identifies errors in transmitted frames but does not always correct them.
5. **Media Access Control (MAC)**: Manages how devices share access to the physical medium to avoid collisions.
Called **Layer 2** in the **OSI model**
![[Pasted image 20250312093623.png]]
> how are data link address layers identified? how does a router/switch know which device to send the frames to?

Data link layer manages 3 different types of links, i.e point-to-point links, multi-point links and broadcast links

Data link layer has 2 sublayers: (Follows IEEE 802.2 standards)
- [[DLC Sublayer]] → Upper sublayer → Called LLC (Logical Link Control) in OSI model
- [[MAC Sublayer]] → Lower sublayer
broadcast links have both DLC and MAC![[Pasted image 20250312095549.png]]

IP address stores the destination address of a datagram (network packet) → another addressing mechanism needs to be used » this is *link address/physical address/MAC address*
# DLL Services
The data link layer provides four essential services to ensure reliable and efficient data transmission across a network: framing, flow control, error control, and congestion control.
## 1. Framing  
Framing involves encapsulating raw data bits from the physical layer into structured units called frames. These frames include headers, trailers, and delimiters to manage data transmission.  
- Frame Structure:  
	- **Heade**r: Contains source/destination addresses and control information
	- **Payload:** The actual data being transmitted
	- **Trailer**: Includes error-detection bits (e.g., CRC checksum
	- **Flags:** Mark the start and end of a frame (e.g., using bit/byte stuffing)
- Types of Framing:  
	- **Fixed-Size Framing:** Uses predefined frame sizes (e.g., ATM cells)
	- **Variable-Size Framing**: Employs delimiters (e.g., Ethernet's length field or Token Ring's end delimiter)
## 2. Flow Control  
Flow control regulates data transmission rates to prevent a fast sender from overwhelming a slow receiver.  
- Techniques:  
	- **Stop-and-Wait:** The sender transmits one frame and waits for acknowledgment (ACK) before sending the next
	- **Sliding Window**: Allows multiple frames in transit, improving efficiency by dynamically adjusting the window size based on ACKs
- Purpose: Ensures receivers can process incoming data without buffer overflows
## 3. Error Control  
Error control detects and corrects data corruption during transmission.  
- Error Detection: Uses checksums, parity bits, or CRC in the frame trailer
- Automatic Repeat Request (ARQ): Retransmits lost/corrupted frames:  
    - Stop-and-Wait ARQ: Retransmits after timeout or negative ACK (NACK)
    - Go-Back-N ARQ: Retransmits all unacknowledged frames after an error
    - Selective Repeat ARQ: Retransmits only corrupted frames
- Types of Errors: Single-bit, multiple-bit, and burst errors
## 4. Congestion Control  
While primarily managed at higher layers (e.g., transport layer), the data link layer contributes indirectly:  
- Access Control: Prevents collisions in shared media (e.g., Ethernet CSMA/CD)
- Flow Control Overlap: By limiting transmission rates, it reduces local congestion
- Cross-Layer Techniques: In wireless networks, protocols like CL-APCC predict congestion by analyzing node memory and network traffic

>[!important] Router
> A Router is a network layer device that is also involved in data-link layer
> - It performs Decapsulation of a frame into a packet (to consult the routing table of Layer 3) and then re-encapsulates the packet into a frame to send it through Layer 2
> - This is a Layer 2 (DLL) service

# Addressing
When an network datagram is transfered between links (as frames) we only know the IP address of the receiving node. Each router gets the IP address of the next router by consulting the forwarding table and the last router is called *destination host*.

But for transfer of frames, we need the *link-layer address* and hence we require a way to convert the IP addess (from network layer) to link-layer address. This is done by [[ARP - Address Resolution Protocol]].

In the data link layer, unicast, multicast, and broadcast addresses are used to manage how data is transmitted across a network. 
1. *Unicast Address*
	- **Definition**: Unicast addresses are used for one-to-one communication, where a frame is sent from a single sender to a single receiver.
	- **Use**: Each host or router interface is assigned a unique unicast address. In Ethernet, these addresses are 48 bits long and represented as 12 hexadecimal digits (e.g., `A3:34:45:11:92:F1`)[2][6].
	- **Function**: Frames with a unicast destination address are delivered to only one device on the network.
2. *Multicast Address*
	- **Definition**: Multicast addresses enable one-to-many communication, where a single sender sends data to multiple receivers that have joined a specific multicast group.
	- **Use**: Multicast addresses are also 48 bits long and similar to unicast addresses but with specific rules (e.g., the second digit must be an even number in hexadecimal)[2].
	- **Example**: In Ethernet, a multicast address might look like `A2:34:45:11:92:F1`[2].
	- **Function**: Frames with a multicast destination address are delivered to all devices that have subscribed to the multicast group within the local network.
 3. *Broadcast Address*
	- **Definition**: Broadcast addresses are used for one-to-all communication, where a single sender sends data to all devices on the local network segment.
	- **Use**: The broadcast address in Ethernet is represented by all ones (`FF:FF:FF:FF:FF:FF`)[2].
	- **Function**: Frames with a broadcast destination address are delivered to every device on the network segment.

**Comparison Table**

| Feature          | Unicast                     | Multicast                  | Broadcast                  |
|-------------------|-----------------------------|----------------------------|----------------------------|
| **Communication** | One-to-one                 | One-to-many                | One-to-all                |
| **Address Format**| Unique MAC per device       | Special MAC for groups     | All ones (`FF:FF:FF...`)   |
| **Use Case**      | Point-to-point communication| Group communication        | Network-wide announcements|
| **Efficiency**    | Efficient for single target| Efficient for groups       | Inefficient (floods all)   |

> [!NOTE]- Citations:
> [1] https://github.com/firmianay/Life-long-Learner/blob/master/data-communications-and-networking/chapter-9.md
> [2] https://www.rcet.org.in/uploads/academics/rohini_81835791715.pdf
> [3] https://www.techtarget.com/searchnetworking/definition/Data-Link-layer
> [4] https://en.wikipedia.org/wiki/Unicast
> [5] https://www.webopedia.com/insights/data-link-layer/
> [6] https://care4you.in/introduction-to-data-link-layer/
> [7] https://radhikaclasses.com/unicast-broadcast-multicast/
> [8] https://study-ccna.com/unicast-multicast-and-broadcast-addresses/
