RSVP - Resource reservation protocol
- Allow multiple senders to transmit to multiple groups
- Individual recievers can switch channels freely
[[Quality of Service]]

Resource reservation protocol uses spanning tree with group address (standard [[Multicast Routing]]) In essence: **RSVP is the "messenger" for IntServ**, enabling dynamic resource reservations to meet strict QoS demands—ideal for small-scale, high-priority traffic but challenging for internet-scale deployments
![[Pasted image 20250712175548.png]]

![[Pasted image 20250712175528.png]]

**Integrated services** means **combining different services together so that users can access them easily, in one place, without having to go to each service separately**. The goal is to make things simpler and more efficient, whether for citizens using government services or for applications in computer networks.

Here’s a simple way to remember it for your exam:

> **Integrated services = Different services joined together to work as one, making life easier for users.**

The **essence of integrated services in networks** lies in providing **diverse traffic types** (e.g., voice, video, data) with **guaranteed Quality of Service (QoS)** over a shared infrastructure. This approach ensures that different applications receive the necessary bandwidth, latency, and reliability they require, as if they were running on dedicated networks.  

---
### **Key Principles of Integrated Services (IntServ):**  
1. **Resource Reservation**  
   - Uses **RSVP (Resource Reservation Protocol)** to reserve bandwidth and buffer space for each flow before data transmission.  
   - Ensures applications (e.g., VoIP, live streaming) get priority treatment.  

2. **Per-Flow QoS Guarantees**  
   - Treats **each data flow individually** (e.g., a single video call vs. file download).  
   - Provides **hard guarantees** on latency, jitter, and packet loss.  

3. **Admission Control**  
   - Checks if the network can support a new flow’s QoS requirements **before allowing it**.  
   - Prevents congestion by rejecting requests if resources are insufficient.  

4. **Traffic Classification & Scheduling**  
   - Prioritizes real-time traffic (e.g., Zoom calls) over best-effort traffic (e.g., emails).  
   - Uses queuing mechanisms like **Weighted Fair Queuing (WFQ)**.  

### **Advantages of IntServ:**  
✔ **Strict QoS guarantees** for high-priority traffic.  
✔ Ideal for **real-time applications** (e.g., telemedicine, video conferencing).  
✔ Fine-grained control over network resources.  

### **Challenges:**  
❌ **Scalability issues** (maintaining state for each flow is resource-intensive).  
❌ Complex to deploy in large networks (e.g., the Internet).  

### **IntServ vs. DiffServ (Differentiated Services)**  
- **IntServ** = Per-flow guarantees (precise but heavy).  
- **DiffServ** = Class-based QoS (scalable but less granular).  

### **Use Cases:**  
- **Enterprise networks** with critical real-time apps.  
- **ISPs** offering premium low-latency services.  

Would you like a deeper dive into RSVP or DiffServ comparisons? 😊
