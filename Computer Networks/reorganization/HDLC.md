***A communication protocol for point-to-point links only***
- Implements stop and wait for transfer
- has 2 modes
	- *Normal response mode* - NRM - 1 primary station & many secondary stations. Primary requests data/service and secondary can only respond to it. for p2p and m2p
	- *Async balanced mode* - ABM - All are equal and can request data and service from each other. only for p2p
- Implements 3 types of frames
	- Information frame (I frame) for data-link user data and control info on user data
	- Supervisory frames (S frame) for transport control info. There are 4 types of S frames (RR, RNR, REJ, SREJ)
	- Unnumbered frames (U frame) system management and managing on the link itself ![[Pasted image 20250319093456.png]]
Flag, Address, Control and FCD are common fields over all frames
- Flag shows start and end of a frame
- Control field determines type of frame
- Address field has address of secondary station
- FCS has the frame check sequence for HDLC error detection
### **Control Field**
- first bit = 0 → i frame
-  10 → S frame
-  11 → U frame ![[Pasted image 20250319094201.png]]
- I frame
	- `0` → I frame
	- N(S) is the sequence number of the frame
	- P/F bit tells whether is packet is *poll* or *final* . P/F = 1 → Poll, else Final
	- N(R) is acknowledgement number when piggybacking
- S frame
	- `10` → S frame
	- Code bits (2b) determine type of S frame
	- N(R) bits are acknowledgement bits
- U frame
	- `11` → U frame
	- Code bits are 5 bits split across P/F bits (2b + 3b). Forms 32 different types of U frames for communicating info on the link

- U frames are used in setting up and breaking connections
![[Pasted image 20250319094929.png]]
