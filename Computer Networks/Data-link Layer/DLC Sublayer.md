***The data link control (DLC) deals with procedures for communication between two adjacent nodes no matter whether the link is dedicated or broadcast***
# DLC Services
The procedure for communication between adjacent nodes (p2p or broadcast node). It is responsible for *framing, flow and error control*
## Framing
Bits from the physical layer are packed into sequences of bits called *frames*. A single frame encodes a sequence of consecutive bits encoding information.
- Framing also adds the source and destination address to the frame. It is a type of *encapsulation*
Frames can be *fixed length frames* or *variable length frames*.
- Fixed length frames do not need boundaries since a sequence of bits are counted and framed based on length. Ex: ATM WANs
- Variable length frames contain specific bit-sequences which act as *delimiters*/flags to differentiate. Ex: LANs
Variable length frames can be encoded as characters or numbers
- *Character oriented frames* use ASCII or Unicode to encode information
	- Contains a *header* with src and dst addresses and a *trailer* with error detection bits. An **8-bit (1 byte) flag** is added to the start and end to act as a delimiter. ![[Pasted image 20250326113735.png]]
	- Sometimes bit-sequences similar to flag end up in the data which can cause the receiver to falsely identify the delimiting flag. This is solved by **Byte stuffing**
- *Bit oriented frames* use raw bits to encode information which is then converted to test/graphics/audio etc.
	- Along with header and trailer, a delimiting sequence is used (usually `0111 1110`) to define beginning and end.![[Pasted image 20250328102608.png]]
	- Similar problem is encountered here where delimiter sequence may end up in data, solved by **bit stuffing**

>[!note]+  Byte stuffing
>The process of adding one extra byte whenever there is a flag or escape character in the text to inform the receiver. Escape characters are removed later on.

>[!note]+ Bit stuffing
>Adding one extra `0` whenever 5 consecutive `1`s  appear. Does this regardless of whether the next (i.e 6th bit) is a `0` or `1`. Extra bit is removed later on
## Flow control
Flow control ensures a balance between production and consumption rates to prevent data loss or inefficiency. If data is produced faster than it can be consumed, the consumer may discard excess items due to being overwhelmed. This data loss is prevented by controlling the sender's transmission rate
- The sending data-link layer pushes frames to the receiving data-link layer, which must process and deliver them to its network layer.
- When the receiving node cannot handle incoming frames at the same rate, it sends feedback to the sender to slow down or stop transmission.
- Usually *buffers* are used at both sending and receiving data-link layers to temporarily store frames during transmission.
- Flow control signals are exchanged between producer and consumer when the buffer is full or has vacancies.
Example: If each data-link layer uses a single memory slot as a buffer, communication becomes simpler. The receiver signals the sender when the slot is empty, allowing transmission of the next frame.
## Error Control
- *Cyclic redundancy check* (CHR), a checksum to identify corrupted packets from network layer
- checksum is added to frame header by the sender
Error control is handled in data link layer because almost all error is generated during physical transmission
- Corrupted frame is silently discarded (in LAN and ethernet)
- An acknowledgement is sent whenever a complete frame is received. Else it is silently discarded and we wait the sender to resend the frame
---
# Data Link Layer Protocols
- Protocol that manages flow, error and congestion control.
-  **Connectionless protocol:** No connection between the frames. Each frame is sent independently
- **Connection oriented** Logical connection exists between frames and are sent in order. Common in p2p protocols
	- 4 protocols exist: simple, stop-and-wait, go-back-N, and selective-repeat
> Ex: [[HDLC]], [[PPP]]

FSMs are used to explain the working of protocols
## **Simple protocol** 
Does not implement error control or flow control. Just sends packets between nodes. Assumed that the receiver always gets perfect packets and never gets overloaded
![[Pasted image 20250328155612.png]]![[Pasted image 20250318104334.png]]

## **Stop-and-wait protocol** 
Implements error and flow control. The sender sends a packet and waits for acknowledgement from receiver before sending the next one![[Pasted image 20250318104629.png]]
![[Pasted image 20250318104714.png]]
- Sender has 2 states:
	- *ready state:* waiting for packet from network layer. When it gets a packet, it frames and copies the packet, starts the timer and sends the frame
	- *blocking state:* 
		- sender resends frame if timer expires
		- resends frame if ACK is corrupted
		- stops timer, deletes copy and moves to ready state if ACK is error-free
- Receiver has 1 state: Always in ready state
	- If error free frame arrives, it sends an ACK back to the sender
	- If corrupted frame arrives, it silently discards it. 

>[!note]+ Piggybacking
> A concept involved in duplex (2-way) communication.
> When both Alice and Bob are communicating, Alice bundles her ACK for Bob’s message with her message, and hence Bob receives the acknowledgement for his previous message along with the new reply from Alice. This saves bandwidth and latency