***The data link control (DLC) deals with procedures for communication between two adjacent nodes no matter whether the link is dedicated or broadcast***

The DLC sublayer takes the network protocol data, which is typically an IPv4 or IPv6 packet, and adds Layer 2 control information to help deliver the packet to the destination node.
→ [[Data Link Layer Protocols]]
# DLC Services
The procedure for communication between adjacent nodes (p2p or broadcast node). It is responsible for *framing, flow and error control*
## Framing
All frames have
- Header
- Data
- Trailer
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

Generic frame structure:![[Pasted image 20250414112026.png]]
Frame fields include the following:
- **Frame start and stop indicator flags** - Used to identify the beginning and end limits of the frame.
- **Addressing** - Indicates the source and destination nodes on the media.
- **Type** - Identifies the Layer 3 protocol in the data field.
- **Control** - Identifies special flow control services such as quality of service (QoS). QoS gives forwarding priority to certain types of messages. For example, voice over IP (VoIP) frames normally receive priority because they are sensitive to delay.
- **Data** - Contains the frame payload (i.e., packet header, segment header, and the data).
- **Error Detection** - Included after the data to form the trailer.

## Flow control
Flow control ensures a balance between production and consumption rates to prevent data loss or inefficiency. If data is produced faster than it can be consumed, the consumer may discard excess items due to being overwhelmed. This data loss is prevented by controlling the sender's transmission rate
- The sending data-link layer pushes frames to the receiving data-link layer, which must process and deliver them to its network layer.
- When the receiving node cannot handle incoming frames at the same rate, it sends feedback to the sender to slow down or stop transmission.
- Usually *buffers* are used at both sending and receiving data-link layers to temporarily store frames during transmission.
- Flow control signals are exchanged between producer and consumer when the buffer is full or has vacancies.
Example: If each data-link layer uses a single memory slot as a buffer, communication becomes simpler. The receiver signals the sender when the slot is empty, allowing transmission of the next frame.
## Error Control
A transmitting node creates a logical summary of the contents of the frame, known as *the cyclic redundancy check (CRC) value*. This value is placed in the *frame check sequence (FCS)* field to represent the contents of the frame. This is an error detection mechanism
- Corrupted frame is silently discarded (in LAN and ethernet)
- An acknowledgement is sent whenever a complete frame is received. Else it is silently discarded and we wait the sender to resend the frame
---

