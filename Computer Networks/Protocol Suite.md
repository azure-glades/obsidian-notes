***A protocol is a set of rules that 2 devices use to communicate over a link***

>[!note]- Protocol layering
> Dividing the task of communication into multiple layers of abstraction with protocols for each layer to translate between the application to the transmission is called protocol layering
# TCP/IP Model
![[Pasted image 20250326100158.png]]
TCP/IP suite is the most common and popular protocol suite used in the world wide web. It uses 5 layers of abstraction to exchange data called *packets*. Packets vary in size and structure depending on the layer they are in.
![[Pasted image 20250326100232.png]]
1. [[Physical Layer]]: Layer involved in transmission of signals in the media
	- Packets in physical layer are *bits* since they are the most basic unit of data that exists.
	- The transmission medium determines the type of receiver/transmitter (optical-electrical media)
	- There are several protocols handling bit transmission
2. [[Data Link Layer]]: Layer involved in choosing the best link for the packets to travel in to reach destination. Decides/chooses the physical link to take to reach destination.
	- Communication is link-to-link or between routers/switches
	- Packets in physical layer are *frames*
	- Data link layer performs *encapsulation* on datagrams and *decapsulation* on bits.
3. [[Network Layer]]: Responsible for creating and managing a stable connection between the source and destination computer. Communication is host-to-host
	- Routers are network layer devices because they do not need the info in application and transport layer
	- Packets in network layer are *datagrams*
	- IP is present in this layer along with routing protocols and auxillary protocols (like ICMP, IGMP, DHCP and ARP)
	- Includes *unicast* and *multicast* communication
4. [[Transport Layer]]: Responsible for giving services to the application layer through an established logical connection. Multiple protocols exist in transport layer and hence the application can use whichever protocol that meets its requirement
	- Packets in transport layer are *segments* or *user datagram*
	- TCP is present in this layer and established a logical connection, manages error correction and traffic/flow control. There are other protocols like UDP and SCTP also.
5. [[App layer]]: Responsible for process-to-process communication between applications by providing an *end-to-end* connection. Abstracts the other layers under it and acts as an API for programs to use for communication.
	- Packets in application layer are *messages*
	- Multiple protocols exist in wide use, like HTTP, WWW, SMTP, FTP SSH, TELNET, USENET and IRC. Other system protocols also exist, like SNMP and DNS
![[Pasted image 20250326103012.png]]
## Encapsulation and Decapsulation
The process of wrapping data with layer-specific headers and trailers as it moves through the layers of the protocol suite is called encapsulation
- The encapsulation process occurs as data moves from the application layer (topmost) to the physical layer (bottommost)
The process of removing headers and trailers added to a data packet during encapsulation to reveal the actual data payload
> If there are 5 layers in a protocol suite, encapsulation occurs 3 times (application → transport, transport → network, network → datalink)
> - ==There is no encapsulation done by physical and application layer==
> Similarly, decapsulation occurs 3 times (datalink → network, network → transport, transport → application)
> - ==There is no decapsulation done by physical and datalink layer== 
![[Pasted image 20250405120907.png]]


## Addressing
Addresses are used to identify host, destination and to transfer the packets through routers and devices in-between. Various protocols are used for translating addresses between layers

| **Layer**         | **Address Type** | **Data Unit Name** |
| ----------------- | ---------------- | ------------------ |
| Application Layer | Names            | Message            |
| Transport Layer   | Port Numbers     | Segment/Datagram   |
| Network Layer     | IP Addresses     | Packet             |
| Data Link Layer   | MAC Addresses    | Frame              |
| Physical Layer    | None             | Bits               |
![[Pasted image 20250620110413.png]]

## Multiplexing
- Multiplexing means that a protocol at a layer can encapsulate a packet from several next-higher layer protocols (one at a time) 
- Demultiplexing means that a protocol can decapsulate and deliver a packet to several next-higher layer protocols (one at a time)
![[Pasted image 20250405122022.png]]

# OSI Model
OSI model was introduced by ISO to act has a replacement to TCP/IP but was not sucessfully adopted. OSI model introduces 2 extra layers (Presentation and Session layer) and hence has 7 different layers exist
![[Pasted image 20250326103138.png]]

## Why was OSI not successful?
1. TCP/IP was in wide use when OSI was developed and it would be expensive to switch over
2. The role of presentation and session layer were not fully defined with no actual protocols defined for the layers
3. It had worse performance than TCP/IP
