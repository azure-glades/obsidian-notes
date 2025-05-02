- There are groups of computers within the network and data is sent to all computers within these groups
Multicast routing is a method for efficiently sending a single stream of information to multiple recipients simultaneously. Instead of sending individual messages to each member of a group (unicasting), or broadcasting to the entire network, multicast delivers the message only to those who have explicitly joined a specific multicast group.

Think of it like subscribing to a specific channel on television. The broadcaster sends the signal once, and only those who have tuned into that channel receive it. This is particularly useful for applications like:

- **Video conferencing:** Distributing the video and audio feed from the speaker to all participants.
- **Online gaming:** Sending game state updates to all players in a session.
- **Streaming media:** Delivering live or on-demand content to interested users.
- **Distributed databases:** Replicating updates to multiple servers.

**Key aspects of multicast routing include:**

1. **Group Management:** This involves mechanisms to create, destroy, and manage the membership of multicast groups. Hosts need to be able to join and leave these groups, and the network needs to be aware of these memberships. Two common ways for routers to learn about group membership are:
    
    - Hosts explicitly inform their local router when they join or leave a group.
    - Routers periodically query the hosts on their directly connected networks to discover their group memberships.
2. **Multicast Forwarding:** Routers need to efficiently forward multicast packets only to the members of the destination group. A common technique for this is **pruning of spanning trees**.
    
    - Initially, each router might conceptually build a spanning tree that covers all other routers in the network.
        
    - When a multicast packet is sent, the router examines its local spanning tree for that group.
        
    - It then "prunes" the tree by removing any branches that do not lead to any hosts that are members of the multicast group. This is often achieved using "PRUNE" messages sent upstream to inform other routers that certain paths are not needed for that specific group.
        
    - As a result, the multicast packet is only forwarded along the branches of the spanning tree that lead to active members of the group.
        
    - **Link-state routing:** In networks using link-state protocols, each router has a complete view of the network topology and group memberships. Pruning can be done by starting from the potential destinations and working backward, removing any routers that are not on a path to a group member.
        
    - **Distance vector routing:** With distance vector protocols, a technique called **reverse path forwarding (RPF)** is often used as a basis for multicast forwarding. Routers receiving a multicast packet check if it arrived on the interface they would use to send unicast traffic back to the source. If it did, they forward it to all other interfaces (except the incoming one) that might lead to group members. To optimize this, **PRUNE** messages are used. If a router has no local group members and no downstream routers interested in the group, it sends a PRUNE message to the upstream router to stop forwarding traffic for that group down that path. This pruning process can be recursive.
        

**Disadvantages of basic spanning tree approaches:**

- **Poor Scalability:** If there are many multicast groups in the network, and each group has members scattered across the network, the number of pruned spanning trees that each router needs to store can become very large (potentially m×n trees, where n is the number of groups and m is the average number of members, although the storage is per group, not per member). This can consume significant memory resources in the routers.

**Alternative Designs:**

- **Core-Based Trees:** To address the scalability issue, methods like core-based trees are used. In this approach, a single spanning tree is computed for each multicast group, rooted at a designated "core" router, often positioned centrally within the group members. To send a multicast message, a host sends it to the core router, which then forwards it down the shared spanning tree for that group. This significantly reduces the storage overhead, as each router only needs to maintain information about one tree per group it's involved in.

In essence, multicast routing optimizes bandwidth usage by delivering traffic only where it's needed, making it a crucial technology for many-to-many communication in modern networks.