# Network Congestion Management

## 1. Core Concepts
### [[Congestion Control]]
**Definition**: Mechanisms to prevent network overload when too many packets cause delays/loss  
**TCP Mechanisms**:  
- **[[AIMD]]**:  
  - Additive Increase: Window size +1 per RTT  
  - Multiplicative Decrease: Halve window on packet loss  
- **[[Slow Start]]**:  
  - Exponential growth until ssthresh  
  - Example: Initial cwnd = 1 → 2 → 4 → 8...  
- **[[Congestion Avoidance]]**:  
  - Linear growth after ssthresh  

**Detection**:  
- Timeouts  
- 3 Duplicate ACKs  

**Real-World Example**: Video streaming bitrate adaptation  

### [[Congestion Collapse]]  
**Definition**: Network state where retransmissions dominate useful throughput  
**Key Insight**:  
- More memory → ↑latency → more retransmissions (doesn't prevent collapse)  
- **ARPANET Case**: 1986 collapse led to TCP improvements  

---

## 2. Prevention Strategies
### [[Traffic Management]]
#### [[Provisioning]]  
**Types**:  
- **Static**: Fixed capacity (enterprise LANs)  
- **Dynamic**: Cloud auto-scaling  

**Tradeoffs**:  
- Over-provisioning: High cost, low utilization  
- Under-provisioning: Risk during spikes  

#### [[Traffic-Aware Routing]]  
**Protocols**:  
- OSPF/EIGRP with congestion metrics  
**Example**: CDN rerouting around congested paths  

---

## 3. Reaction Mechanisms
### [[Load Shedding]]  
**Policies**:  
| Policy | Priority | Use Case |  
|--------|----------|----------|  
| **Wine** | Older packets | File transfers |  
| **Milk** | Newer packets | VoIP/Video |  

### [[Random Early Detection (RED)]]  
**Mechanics**:  
- Avg queue length monitoring  
- Probabilistic drops between min_th/max_th  
**Vs Tail Drop**: Prevents TCP global synchronization  

---

## 4. Quality of Service
### [[QoS Fundamentals]]  
**Techniques**:  
1. **Traffic Shaping**:  
   - Token Bucket (allows bursts)  
   - Leaky Bucket (smooths traffic)  
2. **Prioritization**:  
   - DiffServ (DSCP markings)  
   - IntServ (RSVP reservations)  

### [[Jitter Control]]  
**Methods**:  
- Adaptive buffering (30-50ms for VoIP)  
- Packet timestamping  

---

## Comparative Tables
### [[Congestion Control vs Flow Control]]  
```properties
| Aspect          | Congestion Control       | Flow Control          |
|-----------------|--------------------------|-----------------------|
| Purpose         | Network-wide protection  | Receiver protection   |
| Layer           | Transport/Network        | Data Link/Transport   |
| Feedback        | Implicit (loss/RTT)      | Explicit (window ads) |