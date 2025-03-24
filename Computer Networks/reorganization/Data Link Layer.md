
- Nodes connected by links. Nodes can be switches or routers.
![[Pasted image 20250312093623.png]]
> how are data link address layers identified? how does a router/switch know which device to send the frames to?

- Flow control: to make sure all frames are recieved. frame buffer is used to temporarily recieve and store → full buffer results in frame drops
- error control: error induced due to physical noise is corrected → new frames may be requested

2 types of links; p2p links and broadcast links
Data link layer has 2 sublayers:
- *data link control (DLC) layer*
- *media access control (MAC) layer*
broadcast links have both DLC and MAC![[Pasted image 20250312095549.png]]

IP address stores the destination address of a datagram (network packet) → another addressing mechanism needs to be used » this is *link address/physical address/MAC address*


## DLC Services
### Framing
- byte-oriented encoding system
- flag byte separates consecutive bytes → frame has header and trailer
- see byte-stuffing → variable length framing. Frame borders are used to mark different frames in variable length framing. there is header, buffer and flag bits etc. normal framing all frames have same length so marking is not needed
### Flow control
### Error Control
- Cyclic redundancy check (CHECKSUM) to identify corrupted packets from network layer
- checksum is added to frame header by the sender
### Congestion Control

## Data Link Layer Protocols
- Protocol that manages flow, error and congestion control.
-  **Connection less** No ordering of service
- **Connection oriented** Ordering of service
	- 4 protocols exist: simple, stop-and-wait, go-back-N, and selective-repeat
### **Simple protocol** 
Does not implement error control or flow control. Just sends packets between nodes. Logic is explained as a FSM (finite state machine) with  state ![[Pasted image 20250318104334.png]]

### **Stop-and-wait protocol** 
Implements error and flow control. The sender sends a packet and waits for acknowledgement from receiver before sending the next one![[Pasted image 20250318104629.png]]
- Follows an FSM of 2 states![[Pasted image 20250318104714.png]]
- Sender state:
	- *ready state:* waiting for packet from network layer. When it gets a packet, it frames and copies the packet, starts the timer and sends the frame
	- *blocking state:* 
		- sender resends frame if timer expires
		- resends frame if ACK is corrupted
		- stops timer, deletes copy and moves to ready state if ACK is error-free

>[!note]+ Piggybacking
> h h h
> h h h

>[!note]+ Byte stuffing
> h h h 

### [[HDLC]] : High level data link control

### [[PPP]] : Point-to-point protocol
PPP servies given and not given → list out
### [[CSMA]] : Carrier Sense Multiple Access
Multipoint 