
IPv4 packet has *header* and *body/payload*
IPv4 header is **20 bytes** and an extra variable-length optional part
![[Pasted image 20250619174824.png]]
![[Pasted image 20250619175054.png]]

| Field                       | Size (bits)              | Purpose                                                                                     |
| --------------------------- | ------------------------ | ------------------------------------------------------------------------------------------- |
| **Version**                 | 4                        | Indicates IP version (4 for IPv4).                                                          |
| **IHL**                     | 4                        | Header length in 32-bit words (min: 5 [20 bytes], max: 15 [60 bytes]).                      |
| **Differentiated Services** | 8                        | QoS prioritization (6b) (*Expedited and Assured Services*) + ECN (4b) *congestion signals*. |
| **Total Length**            | 16                       | Entire datagram size (header + data, max 65,535 bytes).                                     |
| **Identification**          | 16                       | Unique ID for fragment reassembly.                                                          |
| **Flags**                   | 3                        | Controls fragmentation (Unused bit, DF=Don't Fragment, MF=More Fragments)                   |
| **Fragment Offset**         | 13                       | Fragment position in original datagram (in 8-byte units).                                   |
| **Time-to-Live**            | 8                        | Prevents loops by limiting hops (decremented on each hop).                                  |
| **Protocol**                | 8                        | Upper-layer protocol (e.g., TCP=6, UDP=17).                                                 |
| **Header Checksum**         | 16                       | Error detection for header integrity.                                                       |
| **Source Address**          | 32                       | Sender's IP address.                                                                        |
| **Destination Address**     | 32                       | Receiver's IP address.                                                                      |
| **Options**                 | Variable (Upto 40 Bytes) | Optional features (e.g., security, routing).                                                |

1. **Version (4 bits)**  
   Identifies IPv4 (`0100`). Enables coexistence with newer versions (e.g., IPv6).
2. **IHL (4 bits)**  
   Specifies header length in 32-bit increments. Minimum value is **5** (20 bytes), maximum is **15** (60 bytes). Options field expands the header beyond 20 bytes.
3. **Differentiated Services (8 bits)**  
	   - **Top 6 bits**: Define packet priority (QoS classes like low delay/high throughput).  
	   - **Bottom 2 bits**: Explicit Congestion Notification (ECN).
4. **Fragmentation Fields**  
	   - **Identification**: Tags fragments of the same datagram.  
	   - **Flags**:  
	     - **DF (Don't Fragment)**: Forces routers to drop oversized packets.  
	     - **MF (More Fragments)**: Indicates non-final fragments.  
	   - **Fragment Offset**: Locates fragments in the original payload.
5. **TTL (8 bits)**  
   Initially measured in seconds, now counts hops. Discarded when reaching 0 to prevent loops.
6. **Protocol (8 bits)**  
   Specifies the encapsulated protocol (e.g., TCP, UDP, ICMP).
7. **Header Checksum (16 bits)**  
   Validates header integrity. Recalculated at each hop due to TTL changes.


- **Fragmentation**: Managed via Identification, Flags, and Fragment Offset. MF=1 signals non-final fragments; DF=1 blocks fragmentation.  
- **Options Field**: Supports debugging/tracing (e.g., record route, timestamp). Limited to 40 bytes, rarely used.  
- **TTL & Routing**: Ensures packets expire if routing loops occur.  

### Critical Constraints
- **Maximum Datagram Size**: 65,535 bytes (limited by 16-bit Total Length).  
- **Header Size Limit**: 60 bytes (due to 4-bit IHL field).  

> IP options are no longer used and supported. All routers ignore optional bits and the IP Header is always 20 Bytes

## Limitations of IPv4
- **IPv4 address depletion** - IPv4 has a limited number of unique public addresses available. Although there are approximately 4 billion IPv4 addresses, the increasing number of new IP-enabled devices, always-on connections, and the potential growth of less-developed regions have increased the need for more addresses.
- **Lack of end-to-end connectivity** - Network Address Translation (NAT) is a technology commonly implemented within IPv4 networks. NAT provides a way for multiple devices to share a single public IPv4 address. However, because the public IPv4 address is shared, the IPv4 address of an internal network host is hidden. This can be problematic for technologies that require end-to-end connectivity.
- **Increased network complexity** - While NAT has extended the lifespan of IPv4 it was only meant as a transition mechanism to IPv6. NAT in its various implementation creates additional complexity in the network, creating latency and making troubleshooting more difficult.
