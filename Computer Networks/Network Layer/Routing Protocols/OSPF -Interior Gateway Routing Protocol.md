Link-state routing protocol
- Similar to IS-IS

OSPF divides an AS into areas to increase scalability

| Area Type                  | Description                           | Key Characteristics                                                                                                       |
| -------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Backbone Area (Area 0)** | Central hub connecting all areas.     | - Mandatory for multi-area OSPF.  <br>- Routers moves traffic between areas                                               |
| **Regular Area**           | Standard non-backbone area.           | - Mas many border-routers that connect the area to backbone<br>- May have AS border routers also                          |
| **Stub Area**              | Blocks external routes (Type 5 LSAs). | - Has only 1 border router connecting it to a backbone.<br>- All inter-area traffic has to flow through the border router |

OSPF also has many different routers that do specific tasks

| Router Type                                  | Description                                              | Key Tasks                                                                                                                                                 |
| -------------------------------------------- | -------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Internal Router**                          | Router that is within an area                            | Routes traffic only within the area                                                                                                                       |
| **Area Border Router (ABR)**                 | Connects multiple areas (including Area 0).              | - Informs internal routers about the destinations in other area (so that internal routers can forward packets to ABR)<br>- Forwards traffic between areas |
| **Backbone Router**                          | Transfers data between layers                            | - Routes traffic within the backbone.  <br>- Can be an ABR or internal router.                                                                            |
| **Autonomous System Boundary Router (ASBR)** | Connects the AS to external networks (e.g., other ASes). | - **Redistributes external routes** (e.g., BGP/EIGRP) into OSPF.  <br>- Can be in backbones or regular areas                                              |
![[Pasted image 20250620092142.png]]


Steps:
- Using flooding, each router informs all the other routers in its area of its links to other routers and networks and the cost of these links. This information allows each router to construct the graph for its area(s) and compute the shortest paths. 
- The backbone area does this work, too. In addition, the backbone routers accept information from the area border routers in order to compute the best route from each backbone router to every other router. 
- This information is propagated back to the area border routers, which advertise it within their areas. 
- Using this information, internal routers can select the best route to a destination outside their area, including the best exit router to the backbone.
These steps are done by exchanging packets
![[Pasted image 20250620093332.png]]


