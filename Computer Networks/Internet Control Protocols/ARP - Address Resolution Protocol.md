ARP is an auxiliary protocol in the network layer that maps IP addresses (Layer 3) to MAC addresses (Layer 2).

Steps of ARP
1. Sender wants to contact a host on the same LAN
    - Sender knows the destination’s IP address (e.g., from DNS).
    - Sender checks its ARP cache for a mapping (IP ↔ MAC).
    - If not found, sender broadcasts an ARP request:  
        “Who has IP address X.X.X.X? Tell me your MAC address.”
    - All hosts on the LAN receive the broadcast.
    - Only the host with that IP replies with its MAC address.
    - Sender stores the mapping in its ARP cache for future use.
2. Sender builds and sends the Ethernet frame
    - The frame is addressed to the destination’s MAC address.
    - The IP packet is placed in the payload of the Ethernet frame.
    - The NIC of the destination host receives the frame, extracts the IP packet, and passes it up the stack.


- **Caching:** ARP results are cached to avoid repeated broadcasts.
- **Cache Timeout:** ARP cache entries expire after a few minutes to allow changes in network configuration.

> [!NOTE] Gratuitous ARP
> A host can broadcast its own mapping to update others’ caches or detect duplicate IPs.

> [!NOTE] Proxy ARP
> - Allows a device to appear local even when it is remote.
> - a router answers ARP requests on behalf of another host that is not on the local network. The router replies with its own MAC address for the remote host’s IP.
> - This is used for special cases, like mobile devices or network transitions.