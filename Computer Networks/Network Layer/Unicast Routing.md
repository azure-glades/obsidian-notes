routing from 1 source to 1 destination

- Networks are represented as graphs, and hence routing algorithms are generally graph traversal techniques
- **Cost** is the total energy required to send a packet along the route/link. More cost → worse the route. Routing is a *minimization problem* to minimize the cost.
	- The **distance metric** is commonly used as a cost metric. Distance can be Euclidean distance, Hamming distance etc.
- Many strategies can be used for routing packets.
	- It is possible to find the optimal path when the links of the system can be described (using Djikstra’s algorithm)
	- Routers can also just forward the packet to every router and hope it reaches the right one, other routers just delete it (flood-filling algorithm)

