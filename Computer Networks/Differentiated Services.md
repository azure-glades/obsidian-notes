**Differentiated Services (DiffServ)** is a way for networks to handle different types of data traffic by **grouping them into classes and giving each class a different priority or quality of service (QoS)**[^1](https://en.wikipedia.org/wiki/Differentiated_services)[^3](https://www.ibm.com/docs/en/aix/7.2.0?topic=models-differentiated-services). This means important traffic (like voice or video calls) can get better, faster treatment than less important traffic (like file downloads or emails).

Here’s a simple way to remember it for your exam:

> **Differentiated Services = Grouping network traffic into classes, and treating each class differently based on its importance.**

**Key points to remember:**

- **Traffic is divided into classes** (not individual flows like IntServ).
- **Each class gets different treatment**—for example, voice calls get higher priority than web browsing[^1](https://en.wikipedia.org/wiki/Differentiated_services)[^3](https://www.ibm.com/docs/en/aix/7.2.0?topic=models-differentiated-services).
- **Routers use a special code (DSCP) in the IP packet header** to identify the class of each packet[^2](https://www.ibm.com/docs/en/aix/7.2.0?topic=models-differentiated-services).
- **No need to track each flow separately**—makes DiffServ scalable and easier for big networks[^3](https://www.sciencedirect.com/topics/computer-science/differentiated-service).
- **Examples of classes:**
    - Expedited Forwarding (EF) for low-delay traffic (like voice calls)[^3](https://www.ibm.com/docs/en/aix/7.2.0?topic=models-differentiated-services).
    - Assured Forwarding (AF) for important but less critical traffic[^3](https://www.ibm.com/docs/en/aix/7.2.0?topic=models-differentiated-services).
    - Default (DE) for regular, best-effort traffic[^3](https://www.ibm.com/docs/en/aix/7.2.0?topic=models-differentiated-services).

**Easy way to remember:**

> _DiffServ = “Traffic classes, different priorities, better network management.”_

So, **DiffServ helps networks run smoothly by making sure the most important data gets through first, especially when the network is busy**[^1](https://en.wikipedia.org/wiki/Differentiated_services)[^3](https://www.ibm.com/docs/en/aix/7.2.0?topic=models-differentiated-services).

---

The **essence of Differentiated Services (DiffServ)** lies in its ability to provide **scalable and flexible quality of service (QoS)** in IP networks by classifying and managing traffic based on **service classes** rather than per-flow handling (as in IntServ/RSVP). 

### **Key Aspects of DiffServ:**
1. **Traffic Classification & Marking:**  
   - Packets are classified into different **Per-Hop Behaviors (PHBs)** using the **Differentiated Services Code Point (DSCP)** in the IP header (6 bits in the ToS field).  
   - Example classes: **Expedited Forwarding (EF)** for low-latency traffic, **Assured Forwarding (AF)** for guaranteed delivery, and **Best Effort (BE)** for default traffic.

2. **Per-Hop Behavior (PHB):**  
   - Routers apply predefined forwarding treatments based on DSCP markings.  
   - **EF (Priority Queuing)** ensures minimal delay and jitter (e.g., VoIP).  
   - **AF (Weighted Fair Queuing)** provides drop precedence for different traffic levels.  

3. **Scalability & Simplicity:**  
   - Unlike IntServ (which requires per-flow state maintenance), DiffServ works on **aggregate traffic classes**, making it more scalable for large networks.  

4. **Domain-Based QoS:**  
   - DiffServ operates within a **DiffServ domain**, where edge routers classify/mark traffic, and core routers apply PHBs accordingly.  

### **Why DiffServ?**
- **Efficient resource utilization** without per-flow overhead.  
- **Prioritization of critical traffic** (e.g., VoIP, video conferencing).  
- **Simplified QoS management** in large-scale networks (ISPs, enterprise backbones).  

### **Comparison with IntServ:**
| Feature        | DiffServ | IntServ (RSVP) |
|---------------|----------|---------------|
| **Granularity** | Class-based | Per-flow |
| **Scalability** | High (aggregate traffic) | Low (per-flow state) |
| **Complexity** | Low (edge/core separation) | High (signaling required) |

### **Conclusion:**
DiffServ’s essence is **prioritizing traffic efficiently without complex per-flow management**, making it ideal for modern IP networks where scalability and simplicity are crucial.

![[Pasted image 20250712175517.png]]
![[Pasted image 20250712175544.png]]