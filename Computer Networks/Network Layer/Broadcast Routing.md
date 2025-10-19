Messages are sent to every computer on the network is called broadcasting.
- The main problem with broadcasting is the number of copy/repeat packets in generates which need to be culled

# How to do broadcast routing?
**Send a packet to all destinations in network** : The sources sends a distinct packet to every destination. Easy to implement but needs a lot of work on the source router
## Multi-destination routing
This approach optimizes broadcast traffic by:
1. **Packet Structure**: Including a list of all destination addresses within a single packet
2. **Router Processing**:
    - The router examines all destinations in the packet.
    - Identifies the optimal output lines required to reach at least one destination in the list
3. **Packet Splitting**:
    - Generates a new copy of the packet for each necessary output line.
    - Partitions the destination list among these copies, assigning only relevant destinations to each line
## Flooding
Packet is sent to all neighbours who forward it to all of their neighbours. Generates a huge number of packets exponentially which floods the network.
To limit the number of flood packets
- Age
- hop count
- reverse path forwarding

> Reverse path forwarding
> The destination looks at the route to the source of packet. If the packet arrived on the link it would’ve used, the router considers it as the first packet and forwards it to all other links. Else it is considered a copy and discarded.

> Reverse path forwarding vs flooding
> - The broadcast packet is sent only once in each direction.
> - It requires the routers know how to reach all destinations without needing to remember sequence numbers or list all destinations in the packet.
> - Easy to implement.

## Using a spanning tree
A spanning tree is needed for broadcast routing to **prevent loops** in networks with redundant paths, which can cause broadcast storms and network congestion[1](https://www.techtarget.com/searchnetworking/definition/spanning-tree-protocol)[2](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol)[5](https://www.tutorialspoint.com/spanning-tree-protocol). By creating a loop-free topology, it ensures:
1. **Elimination of infinite loops**: Blocks redundant paths, stopping data from circulating endlessly[1](https://www.techtarget.com/searchnetworking/definition/spanning-tree-protocol)[5](https://www.tutorialspoint.com/spanning-tree-protocol).
2. **Controlled broadcast propagation**: Broadcasts follow a single tree structure, reaching all nodes without duplication[4](https://ocw.mit.edu/courses/6-263j-data-communication-networks-fall-2002/e4e5a5f72a2876efee7a9a4c4a0a715b_Lecture19.pdf)[7](https://networklessons.com/spanning-tree/spanning-tree-stp-limitations).
3. **Fault tolerance**: Automatically activates backup paths if primary links fail, maintaining connectivity[3](https://www.jetking.com/blog/spanning-tree-protocol-explained)[6](https://www.auvik.com/franklyit/blog/first-deployment-spanning-tree/).
Without a spanning tree, redundant links in switched networks lead to MAC table instability, packet duplication, and degraded performance[2](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol)[5](https://www.tutorialspoint.com/spanning-tree-protocol)[7](https://networklessons.com/spanning-tree/spanning-tree-stp-limitations).