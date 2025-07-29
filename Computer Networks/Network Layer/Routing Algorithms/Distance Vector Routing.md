Used in [[RIP - Routing Information Protocol]]
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

