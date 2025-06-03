The transport layer is responsible for logical communications between applications running on different hosts. This may include services such as establishing a temporary session between two hosts and the reliable transmission of information for an application.

The transport layer has no knowledge of the destination host type, the type of media over which the data must travel, the path taken by the data, the congestion on a link, or the size of the network.
2 main protocols: 
- TCP - transmission control protocol
- UDP - user datagram protocol
![[Pasted image 20250601130451.png]]

- - -
TCP is considered a reliable, full-featured transport layer protocol, which ensures that all of the data arrives at the destination. TCP includes fields which ensure the delivery of the application data. These fields require additional processing by the sending and receiving hosts.
- TCP transport is analogous to sending packages that are tracked from source to destination. If a shipping order is broken up into several packages, a customer can check online to see the order of the delivery.

TCP header → 10 fields - 20 bytes
![[Pasted image 20250601131401.png]]
![[Pasted image 20250601131551.png]]


TCP 3 way handshake
1. Client sends SYN
2. Server sends ACK+SYN (in single packet)
3. Client sends ACK

The six bits in the Control Bits field of the TCP segment header are also known as flags. A flag is a bit that is set to either on or off.
The six control bits flags are as follows:
- **URG** - Urgent pointer field significant
- **ACK** - Acknowledgment flag used in connection establishment and session termination
- **PSH** - Push function
- **RST** - Reset the connection when an error or timeout occurs
- **SYN** - Synchronize sequence numbers used in connection establishment
- **FIN** - No more data from sender and used in session termination

TCP session termination 4 steps
1. Client sends FIN
2. Server replies ACK
3. Server sends FIN
4. Client replies ACK

Acknowledgement packets are ACK and request for next packet
- retransmission when packet is lost may be duplicate or not. SACK is where server selectively acknowledges recieving specific packets![[Pasted image 20250601154213.png]]
- ![[Pasted image 20250601154221.png]]








- - -
UDP is a simpler transport layer protocol than TCP. It does not provide reliability and flow control, which means it requires fewer header fields. Because the sender and the receiver UDP processes do not have to manage reliability and flow control, this means UDP datagrams can be processed faster than TCP segments. UDP provides the basic functions for delivering datagrams between the appropriate applications, with very little overhead and data checking
- UDP is like placing a regular, nonregistered, letter in the mail. The sender of the letter is not aware of the availability of the receiver to receive the letter. Nor is the post office responsible for tracking the letter or informing the sender if the letter does not arrive at the final destination.

![[Pasted image 20250601131722.png]]
![[Pasted image 20250601151117.png]]

- - -
Port numbers
Socket pairs
- 0 to 65535 available ports
![[Pasted image 20250601152314.png]]
![[Pasted image 20250601152413.png]]

- - -

### Transport Layer: The Application Link

- **Role:** Links applications to the network, enabling **logical communication** between apps on different hosts.
- **Protocols:** Primarily uses **TCP** (Transmission Control Protocol) and **UDP** (User Datagram Protocol).
- **Key Responsibilities:** Tracking conversations (sessions), segmenting/reassembling data, adding header info, identifying applications, and conversation multiplexing.

---

### TCP: Reliable & Ordered

- **Characteristics:**
    - **Stateful:** Keeps track of the connection.
    - **Reliable:** Guarantees delivery.
    - **Acknowledges data:** Confirms receipt.
    - **Resends lost data:** Handles missing segments.
    - **Sequenced order:** Delivers data in the correct order.
    - **Flow Control:** Manages data rate to prevent overwhelming the receiver.
- **Overhead:** Adds 20 bytes of header information per segment.
- **Key Header Fields:** Source/Destination Ports, Sequence Number, Acknowledgment Number, Window Size.
- **Process:**
    - **Three-way handshake:** Establishes a session.
    - **Four exchanges:** Needed to terminate a session.
    - **Sequence numbers:** Used to reorder and identify missing data.
    - **Sliding windows & SACK:** Mechanisms for flow control and efficient retransmissions.
- **Common Applications:** HTTP (web), FTP (file transfer), SMTP (email), Telnet.

---

### UDP: Fast & Simple

- **Characteristics:**
    - **Stateless:** Doesn't track the connection.
    - **Fast:** Lower overhead.
    - **No acknowledgments:** Doesn't confirm receipt.
    - **Doesn't resend lost data:** If data is lost, it's gone.
    - **No guaranteed order:** Data arrives in the order it's received.
    - **No flow control:** Doesn't manage sender's rate.
- **Overhead:** Smaller header (Source/Destination Ports, Length, Checksum).
- **Common Applications:** DHCP, DNS, SNMP, TFTP, VoIP, Video Conferencing (where speed is more critical than absolute reliability).

---

### Port Numbers & Sockets

- **Purpose:** TCP and UDP use **port numbers** to manage multiple conversations and identify specific applications on a host.
- **Location:** Port numbers are in the TCP/UDP segment headers.
- **Socket:** The combination of an **IP address** and a **port number** (e.g., `192.168.1.1:80`). Used to identify services.
- **Ranges:**
    - **Well-known Ports (0-1023):** Reserved for common services (e.g., HTTP: 80, FTP: 21, DNS: 53).
    - **Registered Ports (1024-49151):** Assigned to specific applications by IANA.
    - **Private/Dynamic Ports (49152-65535):** Used by client applications for source ports.
- **Netstat:** A utility to view active TCP connections on a host.