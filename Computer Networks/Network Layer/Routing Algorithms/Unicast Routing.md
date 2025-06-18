***one-to-one delivery where a datagram is sent to only one destination host is unicast routing. The best unicast routing algorithm is the algorithm that finds the shortest path in least amount of time***

- Networks are represented as graphs, and hence routing algorithms are generally graph traversal techniques
- **Cost** is the total energy required to send a packet along the route/link. More cost → worse the route. Routing is a *minimization problem* to minimize the cost.
	- The **distance metric** is commonly used as a cost metric. Distance can be Euclidean distance, Hamming distance etc.
- Many strategies can be used for routing packets.
	- It is possible to find the optimal path when the links of the system can be described (using Djikstra’s algorithm)
	- Routers can also just forward the packet to every router and hope it reaches the right one, other routers just delete it (flood-filling algorithm)

> Algorithms:
> - Dijkstra’s algorithm
> - Bellman-Ford algorithm

# Routing Algorithms
## [[Distance Vector Routing]]
A decentralized routing protocol where routers determine optimal paths based on distance metrics (e.g., hops, latency) and share this information with neighbouring nodes.
- Each router maintains a *distance-vector table* which has
	- Target router
	- Distance to target router
	- Next hop/neighbour to reach target router
	- ![[Pasted image 20250425222920.png]]
- The Bellman-Ford Equation is used to find the least-cost distance
Routers then share their distance-vector table with their neighbours and update it on comparison. This process repeats multiple times until all routes *converge* to the best paths in the network.
- DV converges slowly whenever a link gets broken

Steps:
1. Each router draws up a distance vector table by considering its neighbours. The initial distance vector hence only describes its neighbours
2. Routers then send their distance vectors to their neighbours. Bellman-ford equation is used to find the least-cost route. Suppose to reach a node, the current cost is 4. It receives a distance vector from another node which can reach the destination with a cost of 2. It takes a cost of 1 to reach this intermediate. Hence 2+1 < 4, and the least-cost route is by directing traffic through the intermediate node. 
3. This is done iteratively where every route checks its distance-vector with that of its neighbours to find the least-cost route
4. Upon multiple exchanges, the vectors stabilize and the final distance-vector is stored for routing

>[!important] Count to Infinity Problem
> An important case that occurs in DV routing where the routers end-up not able to converge to a value because they keep updating each-others DVs. Ends up with them counting to infinity. See pg 603, Unicast routing, Forouzan. Mainly caused due to broken links that need to be updated
> Some solutions have been proposed:
> - Split Horizon
> - Poison Reverse
## [[Link State Routing]]
A routing technique where every router knows the complete topology of the network, and uses that information to find the shortest route. The edge state is stored in a matrix called the *link state database*. There is only 1 LSDB for the whole internetwork.
- Router booted → identifies neighbours (*HELLO packet*)
- Link costs are set (based on bandwidth, time taken (*ECHO packet*))
- *Link-state packets* are sent with a sequence number and age to all routers by *flooding*. The LS packet retrieves information on the identity of the node and the cost to reach it. Once each LS packet arrives an LSDB is created
	- To prevent over-flooding, packets have a sequence-number/age. It helps to identify repeated packets (if the sequence number is bigger than the one it recieved, it means it has been broadcasted already and there is no need to resend it)
- New LS packets need to be sent whenever a link breaks or a router fails to update the table
Optimal path is calculated from the LSDB using Djikstra’s routing algorithm

|Feature|Distance Vector Routing|Link State Routing|
|---|---|---|
|Algorithm Used|Bellman-Ford|Dijkstra’s Algorithm|
|Knowledge Scope|Routers share info with immediate neighbors (local view)|Routers share info with all routers (global view)|
|Information Shared|Entire routing table|Link states (status/cost of directly connected links)|
|Bandwidth Usage|Lower (smaller, periodic updates)|Higher (flooding of link state packets)|
|CPU & Memory Usage|Lower|Higher|
|Convergence Speed|Slower, moderate|Faster|
|Looping Issues|Prone to persistent routing loops|Only transient loops, less prone|
|Path Selection Metric|Least number of hops|Least cost (can consider bandwidth, delay, etc.)|
|Scalability|Suited for smaller networks|Better for larger, complex networks|
|Example Protocols|RIP, IGRP|OSPF, IS-IS|
## [[Hierarchical Routing]]
Routing algorithm that clumps routers into clusters/zones to shorten the size of routing tables to make routing algorithms run faster
- Router stores the path to other routers within a group and path to other groups.
- Multiple zones and clusters are also made when network is huge
![[Pasted image 20250502103845.png]]
>[!important]+ Calculating hierarchy
> Optimal level for N routers → ln(N)
> Minimal size of routing table → try to have equal number of zones, groups, routers in a group
> Ex: 3-level hierarchy for N = 4800. ideally → 16\*16\*16 = 4800. By trial and error, ideal match is 15-16-20 (cluster, region, routers in region)
## [[Shortest Path Routing]]
Path-vector routing is used to give greater control because it allows the source to detemine the route by imposing a policy that the packet has to follow when traversing. Path-vector routing is used in routing between ISPs.
- Each router generates a spanning tree which it consults to determine a path
# Routing Protocols
- RIP (routing info protocol)
- OSPF (open shortest path first

---
