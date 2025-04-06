***A bit-oriented protocol for communication over p2p and m2p links which implements the stop-and-wait protocol***
- Is rarely used in practice
- has 2 modes of transfer
	- *Normal response mode* - NRM - 1 primary station & many secondary stations. Primary requests data/service and secondary can only acknowledge it. Used with p2p and m2p links![[Pasted image 20250328162414.png]]
	- *Async balanced mode* - ABM - All are equal and can request data and service from each other. only for p2p![[Pasted image 20250328162422.png]]

HDLC implements DLC services like error and flow control using different types of frames
→ S and U frames along with ACK flags are involved in flow control
→ FCS bits in all the 3 frames are involved in error control
## Framing
- Implements 3 types of frames
	- *Information frame (I frame)* for carrying user data across network with capabillites for piggybacking
	- *Supervisory frames (S frame)* for transport control info. There are 4 types of S frames (RR, RNR, REJ, SREJ)
	- *Unnumbered frames (U frame)* for managing the link itself 
![[Pasted image 20250328162535.png]]
Each frame has upto 6 fields
*Flag, Address, Control and FCS are common fields over all frames*
- Flag delimits the start and end of a frame (always `0111 110`)
- Address field has the address of receiver (i.e secondary station). May be 1 to many bytes long depending on network
- Control field used for flow+error control and is 1 or 2 bytes long
- Information field has the data
- FCS has the *frame check sequence* for HDLC error detection (usually 2 or 4 byte for CRC (checksum, i.e cyclic reduncy check which is an error detection technique))

Frames are distinguished by the first  bits.
`0` → I frame
`10` → S frame
`11` → U frame
![[Pasted image 20250319094201.png]]
The structure of control field varies based on the type of frame
#### I frame
`N(S)` is the sequence number of the frame which is 3b long
`P/F` bit tells whether is the frame is sent by primary or secondary station
- `1` → *Poll* i.e sent by primary to secondary station → Address field has receiver address
- `0` → *Final* i.e sent by secondary to primary station → Address field has sender address (because primary is always sender)
`N(R)` is acknowledgement number when piggybacking
#### S frame
Supervisory frames are used for flow+error control when piggybacking is not possible or not used. They do not have information fields and are only used for error and flow control
The `N(R)` is 3b long and corresponds to ACK (acknowledgement) or NAK (*negative acknowledgement*) depending on type of s frame
The `code` is 2b long and describes the type of S frame
1. `00` → **Receive Ready (RR)** → Sends an ACK and tells the receiver is free to receive more frames. `N(R)` = ACK. 
2. `10` → **Receive Not Ready (RNR)** → Sends an ACK and tells the receiver is busy and cannot receive more frames. Flow control mechanism. `N(R)` = ACK. 
3. `01` → **Reject (REJ)** → Sends a NAK informing that the frame was corrupted (used in Go-back-N protocol type). `N(R)` = NAK
4. `11` → **Selective Reject (SREJ)** → Sends a NAK used in selective-repeat protocol type. `N(R)` = NAK
#### U frame
U frames are used for session and info control between devices.
- Information field has system management information
- U frame code bits are split across the `p/f` bit. 2b prefix and 3b suffix. Total 5b → *32 different types of U frames*
- U frames are used in setting up and breaking connections
![[Pasted image 20250319094929.png]]
