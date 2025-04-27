***one-to-one delivery where a datagram is sent to only one destination host is unicast routing. The best unicast routing algorithm is the algorithm that finds the shortest path in least amount of time***

- Networks are represented as graphs, and hence routing algorithms are generally graph traversal techniques
- **Cost** is the total energy required to send a packet along the route/link. More cost → worse the route. Routing is a *minimization problem* to minimize the cost.
	- The **distance metric** is commonly used as a cost metric. Distance can be Euclidean distance, Hamming distance etc.

> Algorithms:
> - Dijkstra’s algorithm
> - Bellman-Ford algorithm

# Routing Algorithms
## Distance -Vector Routing
A decentralized routing protocol where routers determine optimal paths based on distance metrics (e.g., hops, latency) and share this information with neighbouring nodes.
- Each router maintains a *distance-vector table* which has
	- Target router
	- Distance to target router
	- Next hop/neighbour to reach target router
	- ![[Pasted image 20250425222920.png]]
- The Bellman-Ford Equation is used to find the least-cost distance
- Each router informs its neighbours on what it knows about the internet and updates it based on that knowledge

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
## Link-State Routing
A routing technique where every router knows the state of every edge in the network and uses that information to find the shortest route. The edge state is stored in a matrix called the *link state database*. There is only 1 LSDB for the whole internetwork.
- The LSDB is created by *flooding* where each node sends a *link-state packet* to every node. The LS packet retrieves information on the identity of the node and the cost to reach it. Once each LS packet arrives an LSDB is created
- If any link breaks, the information is sent out to all other nodes and LSDBs are updated quickly.
- Each router is responsible for informing others about the state of the links around it
- Dijikstra’s algorithm is used for finding the best route by consulting the routing table.

## Path-Vector Routing
Path-vector routing is used to give greater control because it allows the source to detemine the route by imposing a policy that the packet has to follow when traversing. Path-vector routing is used in routing between ISPs.
- Each router generates a spanning tree which it consults to determine a path

## Least Cost Routing

## Hierarchical Routing
# Routing Protocols
- RIP (routing info protocol)
- OSPF (open shortest path first


---
## Shortest Path Routing

**Definition:**

- Briefly define what shortest path routing is.
    

**Key Concepts:**

- Graph representation of networks
    
- Cost metrics (distance, time, hops, etc.)
    

**Algorithms:**

- Dijkstra’s algorithm: steps and example
    
- Bellman-Ford algorithm: steps and example
    

**Advantages and Disadvantages:**

- List pros and cons
    

**Use Cases:**

- Where and why it is used
    

## Flood-Fill Routing

**Definition:**

- What is flood-fill routing?
    

**How It Works:**

- Packet propagation mechanism
    
- Handling of duplicate packets
    

**Advantages and Disadvantages:**

- List pros and cons
    

**Applications:**

- Scenarios where flood-fill is used
    

## Distance-Vector Routing

**Definition:**

- What is distance-vector routing?
    

**How It Works:**

- Routing table structure
    
- Periodic updates
    
- Bellman-Ford algorithm usage
    

**Key Features:**

- Route advertisement
    
- Count-to-infinity problem
    

**Advantages and Disadvantages:**

- List pros and cons
    

**Examples:**

- RIP (Routing Information Protocol)
    

## Link-State Routing

**Definition:**

- What is link-state routing?
    

**How It Works:**

- Link-state advertisements (LSAs)
    
- Building the network topology
    
- Shortest path computation
    

**Key Features:**

- Convergence
    
- Scalability
    

**Advantages and Disadvantages:**

- List pros and cons
    

**Examples:**

- OSPF (Open Shortest Path First)
    
- IS-IS (Intermediate System to Intermediate System)
    

## Least Cost Routing

**Definition:**

- What is least cost routing?
    

**Cost Metrics:**

- Types of costs (bandwidth, delay, monetary, etc.)
    

**Algorithms Used:**

- Mention algorithms (can refer to shortest path, etc.)
    

**Advantages and Disadvantages:**

- List pros and cons
    

**Applications:**

- VoIP, telephony, etc.
    

## Path-Vector Routing

**Definition:**

- What is path-vector routing?
    

**How It Works:**

- Path information in routing updates
    
- Loop prevention
    

**Key Features:**

- Policy-based routing
    
- Scalability
    

**Advantages and Disadvantages:**

- List pros and cons
    

**Examples:**

- BGP (Border Gateway Protocol)
    

You can fill in each section with definitions, diagrams, algorithm steps, examples, and pros/cons as you study each topic.

---

Answer from Perplexity: pplx.ai/share

