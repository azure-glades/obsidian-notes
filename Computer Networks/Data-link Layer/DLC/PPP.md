***Point to Point Protocol is a byte-oriented protocol for communication over mainly p2p links and remains the most commonly used protocol on the internet***

Services:
- Defines format of frames, how to establish a link
- How to encapsulate network layer data → framing
- How to authenticate devices
- Implements many network layer services
- provides connection over many links
- provides network address config
 Does not have
- error or flow control
- no complex addressing mechanism
# Services
PPP is a simple bye oriented protocol
- Defines format of frames exchanged between devices
- Specifies how to establish and negotiate links
- Provides framing method for network layer data encapsulation
- Includes optional authentication mechanism
- Supports multiple network layer protocols (not just IP)
- Implements various network layer services
- *Multilink PPP* allows connections over multiple links
- Provides network address configuration capability
**PPP Does Not Provide:**
- Error control mechanisms
- Flow control mechanisms
## Framing
PPP uses a **character-oriented (byte-oriented)** frame structure

| Field        | Size      | Value/Description                                                                                                                                                            |
| ------------ | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Flag**     | 1 byte    | `01111110` - Marks start/end of frame                                                                                                                                        |
| **Address**  | 1 byte    | Constant `11111111` (broadcast address)                                                                                                                                      |
| **Control**  | 1 byte    | Constant `00000011` (imitates HDLC unnumbered frames)                                                                                                                        |
| **Protocol** | 1-2 bytes | Defines payload content (user data/control info). Default 2 bytes, negotiable to 1                                                                                           |
| **Payload**  | Variable  | Carries user data/control info. Characteristics:<br>- Default max 1500 bytes (negotiable)<br>- Byte-stuffed used when flag is seen<br>- Padding required if size < max value |
| **FCS**      | 2-4 bytes | Frame Check Sequence (CRC for error detection)                                                                                                                               |
![[Pasted image 20250405104017.png]]
- **No flow control** (control field is constant)
- **Limited error control** (only detection via FCS)
- **Byte stuffing** performed on payload if flag pattern appears
- **Padding** required for undersized payloads
- **Protocol field** determines payload interpretation
***Byte stuffing: escape character = `01111101`***

# Transition phases
The function of PPP can be expressed as transition phase diagram
![[Pasted image 20250402200209.png]]
# Multiplexing
PPP uses a set of supporting protocols to establish and authenticate nodes and carry data. It uses
1. **Link Control Protocol:** The Link Control Protocol (LCP) is responsible for establishing, maintaining, configuring, and terminating links. It also provides negotiation mechanisms to set options between the two endpoints. Both endpoints of the link must reach an agreement about the options before the link can be established.
2. **Authentication Protocols:** Authentication means validating the identity of a user who needs to access a set of resources. 2 protocols deal with this
	1. *Password authentication protocol - PAP*
	2. *Challenge handshake authentication protocol - CHAP*
3. **Network control protocols:** There are many different network protocols for dealing with each network packet type, like IPCP, Xerox CP, etc.