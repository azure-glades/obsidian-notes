Used in [[OSPF -Interior Gateway Routing Protocol]]

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
