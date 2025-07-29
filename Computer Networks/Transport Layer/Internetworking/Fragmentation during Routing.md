Networks have a **maximum transmission unit (MTU)** which is the largest packet that can be transferred. If incoming packets are larger than the MTU, they are fragmented into smaller ones and then transmitted
- MTU depends on network, medium, hardware etc
These fragments need to be reassembled before they are sent to the destination

Fragmentation avoidance:
1. **Path MTU Discovery:** source finds the smallest MTU along the path and sends data as packets of that MTU size.
	- The sender transmits packets with the `Don't Fragment - DF`  flag set.
	- If a router receives a packet that's too large, it drops the packet and sends an ICMP `Fragmentation Needed` message back to the sender, indicating the maximum MTU it can handle
	- The sender then reduces the packet size and tries again, repeating this until the packet gets through without fragmentation
	- This increases delay since this exchange will occur multiple times
2. **[[Tunnelling]]:** transfer is not handled by the source/destination

Fragmentation Strategies
1. **Transparent fragmentation:** Fragments are reassembled at the exit of the small-packet network, making fragmentation invisible to subsequent networks.
	- However, this requires all fragments to exit through the same router and can add complexity and performance issues
2. **Nontransparent fragmentation:** Once fragmented, the fragments are not reassembled until they reach the final destination. 
	- This reduces router workload but can increase overhead and risks losing the entire packet if any fragment is lost

![[Pasted image 20250619173637.png]]