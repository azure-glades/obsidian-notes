## **Congestion Control**

**Definition**: Mechanisms to prevent network overload by regulating data flow when too many packets cause delays/loss[1](https://www.tutorialspoint.com/data_communication_computer_network/congestion_control.htm)[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545).
**How It Works**:
- **TCP Congestion Control**
    - **AIMD** (Additive Increase/Multiplicative Decrease): Gradually increases window size (additive) until loss occurs, then halves it (multiplicative)[12](https://en.wikipedia.org/wiki/TCP_congestion_control)[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545).
    - **Slow Start**: Exponentially increases window size initially to probe available bandwidth[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545)[9](https://www.ripublication.com/gjcir/gjcirv2n1_02.pdf).
    - **Congestion Avoidance**: Linear window growth after a threshold (_ssthresh_) to avoid overloading[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545)[12](https://en.wikipedia.org/wiki/TCP_congestion_control).
- **Detection**: Timeouts or duplicate ACKs trigger window reduction[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545)[9](https://www.ripublication.com/gjcir/gjcirv2n1_02.pdf).

**Real-World Example**: Video streaming adjusts quality (bitrate) based on network conditions, mimicking AIMD[12](https://en.wikipedia.org/wiki/TCP_congestion_control).
## **Congestion Collapse**
**Definition**: Network state where excessive retransmissions waste bandwidth, reducing useful throughput[4](https://networkengineering.stackexchange.com/questions/49817/what-is-congestion-collapse)[5](https://datatracker.ietf.org/doc/html/rfc896)[10](https://anirudhsk.github.io/teaching/lectures/lec6.pdf).
**Causes**:
- **Retransmissions**: Duplicate packets from timeouts (e.g., TCP retransmits even if original packets are delayed)[5](https://datatracker.ietf.org/doc/html/rfc896)[10](https://anirudhsk.github.io/teaching/lectures/lec6.pdf).
- **Buffer Overprovisioning**: Excess memory in routers delays packet drops but worsens collapse by increasing latency[5](https://datatracker.ietf.org/doc/html/rfc896)[10](https://anirudhsk.github.io/teaching/lectures/lec6.pdf).

**Why More Memory Fails**: Larger buffers delay collapse but increase latency, leading to more retransmissions[5](https://datatracker.ietf.org/doc/html/rfc896)[10](https://anirudhsk.github.io/teaching/lectures/lec6.pdf).
**Example**: In 1980s ARPANET, unregulated TCP caused collapse until algorithms like AIMD were adopted[10](https://anirudhsk.github.io/teaching/lectures/lec6.pdf)[12](https://en.wikipedia.org/wiki/TCP_congestion_control).

## **Congestion Control vs. Flow Control**

|**Aspect**|**Congestion Control**|**Flow Control**|
|---|---|---|
|**Purpose**|Prevents network overload (global issue)[1](https://www.tutorialspoint.com/data_communication_computer_network/congestion_control.htm)[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm).|Prevents receiver overload (local issue)[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control).|
|**Techniques**|AIMD, slow start, ECN[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545)[12](https://en.wikipedia.org/wiki/TCP_congestion_control).|Sliding window, ACK throttling[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control).|
|**Layers**|Transport/Network layers[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control).|Data Link/Transport layers[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control).|
|**Feedback**|Implicit (packet loss/RTT)[12](https://en.wikipedia.org/wiki/TCP_congestion_control)[13](https://how.dev/answers/flow-control-vs-congestion-control).|Explicit (receiver’s buffer size)[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control).|

**Interaction**: Flow control ensures the receiver keeps up; congestion control ensures the network doesn’t choke[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control).

## **FAQs**
**Q1**: _Why can’t we just add more memory to routers to prevent collapse?_  
**A**: Larger buffers increase latency, causing more retransmissions and wasted bandwidth[5](https://datatracker.ietf.org/doc/html/rfc896)[10](https://anirudhsk.github.io/teaching/lectures/lec6.pdf).
**Q2**: _Does flow control handle network congestion?_  
**A**: No-it only manages sender-receiver speed mismatch[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control).
**Q3**: _How does TCP detect congestion?_  
**A**: Via packet loss (timeouts/duplicate ACKs) or ECN signals[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545)[12](https://en.wikipedia.org/wiki/TCP_congestion_control).
## **Key Points**
- **Congestion Control**: AIMD balances fairness and efficiency; slow start avoids sudden overload[2](https://www.slideshare.net/slideshow/congestion-control-in-tcppptx/265401545)[12](https://en.wikipedia.org/wiki/TCP_congestion_control).
- **Collapse**: Caused by redundant traffic, not just high load[4](https://networkengineering.stackexchange.com/questions/49817/what-is-congestion-collapse)[10](https://anirudhsk.github.io/teaching/lectures/lec6.pdf).
- **Flow vs. Congestion**: Flow = receiver protection; Congestion = network protection[6](https://www.tutorialspoint.com/data_communication_computer_network/flow_control_vs_congestion_control.htm)[13](https://how.dev/answers/flow-control-vs-congestion-control)
## **Provisioning**
**Definition & Purpose**: Allocating network resources (bandwidth, routers) to match traffic demand, preventing congestion by design.  
**How It Works**:
- **Static**: Fixed capacity based on historical data (e.g., enterprise LANs with predictable traffic)[1](https://www.tutorialspoint.com/what-are-different-approaches-to-congestion-control).
- **Dynamic**: Auto-scaling resources (e.g., cloud providers adding servers during peak loads)[1](https://www.tutorialspoint.com/what-are-different-approaches-to-congestion-control)[4](https://www.sanfoundry.com/congestion-control-in-computer-network/).  
    **Real-World Example**: Content Delivery Networks (CDNs) over-provision bandwidth to handle traffic spikes.  
    **FAQs**    
- _Does over-provisioning eliminate congestion?_ No-it delays collapse but increases latency if buffers overflow[1](https://www.tutorialspoint.com/what-are-different-approaches-to-congestion-control)[4](https://www.sanfoundry.com/congestion-control-in-computer-network/).  
    **Key Points**:
- Over-provisioning: High cost, low utilization.
- Under-provisioning: Risky during traffic surges.

## **Traffic-Aware Routing**
**Definition & Purpose**: Dynamically reroutes traffic based on real-time link congestion.  
**How It Works**:
- Protocols like OSPF/EIGRP use metrics (delay, packet loss) to avoid congested paths[2](https://www.tutorialspoint.com/what-is-traffic-aware-routing-in-computer-networks)[4](https://www.sanfoundry.com/congestion-control-in-computer-network/).
    
- Adjusts link weights to prioritize underutilized routes[2](https://www.tutorialspoint.com/what-is-traffic-aware-routing-in-computer-networks).  
    **Real-World Example**: Data centers balance East-West traffic across multiple paths[2](https://www.tutorialspoint.com/what-is-traffic-aware-routing-in-computer-networks)[4](https://www.sanfoundry.com/congestion-control-in-computer-network/).  
    **FAQs**:
    
- _Can it cause routing loops?_ Yes, if updates are too frequent[2](https://www.tutorialspoint.com/what-is-traffic-aware-routing-in-computer-networks).  
    **Key Points**:
    
- Reduces hotspots but risks oscillations.
    
- Combines with congestion control for efficiency.
    

## **Admission Control**

**Definition & Purpose**: Limits new connections to prevent overload (e.g., VoIP call limits)[3](https://www.tutorialspoint.com/what-is-an-admission-control-approach-for-congestion-control)[14](https://www.sciencedirect.com/topics/computer-science/admission-control-decision).  
**How It Works**:

- **Leaky Bucket**: Smooths bursts into steady flows[6](https://www.linkedin.com/pulse/comparing-rate-limiting-algorithms-leaky-bucket-token-aditi-mishra-r1ofc).
    
- **Token Bucket**: Allows temporary bursts using saved credits[6](https://www.linkedin.com/pulse/comparing-rate-limiting-algorithms-leaky-bucket-token-aditi-mishra-r1ofc).  
    **Real-World Example**: Video conferencing apps reject new users during server overload[3](https://www.tutorialspoint.com/what-is-an-admission-control-approach-for-congestion-control).  
    **FAQs**:
    
- _Is it the same as congestion control?_ No-it’s preventive, not reactive[14](https://www.sciencedirect.com/topics/computer-science/admission-control-decision).  
    **Key Points**:
    
- Critical for QoS in real-time apps.
    
- Requires accurate traffic prediction.
    

## **Congestion Avoidance Techniques**

|**Technique**|**Mechanism**|**Use Case**|
|---|---|---|
|**Traffic Throttling**|Rate limiting (e.g., leaky bucket)[6](https://www.linkedin.com/pulse/comparing-rate-limiting-algorithms-leaky-bucket-token-aditi-mishra-r1ofc)[4](https://www.sanfoundry.com/congestion-control-in-computer-network/).|API servers limiting requests/sec.|
|**Choke Packets**|Routers send ICMP Source Quench alerts[7](https://vikramuniv.ac.in/files/wp-content/uploads/BE_8_SEM_EL_CN-CONGESTION_CONTROL-AMIT_THAKUR.pdf)[4](https://www.sanfoundry.com/congestion-control-in-computer-network/).|Legacy networks signaling congestion.|
|**ECN**|Marks packets instead of dropping them[8](https://www.juniper.net/documentation/us/en/software/junos/cos/topics/concept/cos-qfx-series-explicit-congestion-notification-understanding.html).|Low-latency trading systems.|

**FAQs**:

- _Does ECN eliminate packet loss?_ No-it reduces loss but relies on endpoint cooperation[8](https://www.juniper.net/documentation/us/en/software/junos/cos/topics/concept/cos-qfx-series-explicit-congestion-notification-understanding.html).
    

## **Hop-by-Hop Backpressure**

**Definition & Purpose**: Local congestion signals propagate upstream (node-to-node), unlike end-to-end[10](https://www.usenix.org/system/files/nsdi22-paper-goyal.pdf)[17](https://www.alibabacloud.com/blog/analysis-of-network-flow-control-and-back-pressure-flink-advanced-tutorials_596632).  
**How It Works**:

- Congested nodes pause upstream neighbors via credits/flow control[10](https://www.usenix.org/system/files/nsdi22-paper-goyal.pdf)[17](https://www.alibabacloud.com/blog/analysis-of-network-flow-control-and-back-pressure-flink-advanced-tutorials_596632).
    
- Used in programmable switches (e.g., Tofino)[10](https://www.usenix.org/system/files/nsdi22-paper-goyal.pdf).  
    **Real-World Example**: High-frequency trading networks minimizing latency[10](https://www.usenix.org/system/files/nsdi22-paper-goyal.pdf).  
    **FAQs**:
    
- _Is it scalable?_ No-per-flow state limits large networks[11](https://en.wikipedia.org/wiki/Hop-by-hop_transport).  
    **Key Points**:
    
- Faster reaction than end-to-end but complex.
    
- Requires hardware support for low latency.
    

## **Key Comparisons**

|**Aspect**|**Admission Control**|**Congestion Control**|
|---|---|---|
|**Timing**|Prevents congestion upfront.|Reacts after congestion occurs.|
|**Scope**|Per-connection.|Network-wide.|

**Exam Tip**: Focus on trade-offs (e.g., provisioning cost vs. dynamic routing agility) and layer-specific mechanisms (ECN at transport vs. backpressure at data link).


## **Load Shedding ("Milk and Wine" Policy)**

**Definition & Purpose**: Selectively discarding packets to prevent congestion. Prioritizes traffic based on application needs.  
**How It Works**:

- **Wine Policy**: Drops **newer packets** (prioritizes older data), ideal for file transfers where retransmissions are costly[1](http://www.icet.ac.in/Uploads/Downloads/CNModule%204.pdf)[8](http://becbapatla.ac.in/wp-content/uploads/IT-CN-UNIT2.pdf).
    
- **Milk Policy**: Drops **older packets** (prioritizes newer data), suited for real-time apps (e.g., VoIP)[1](http://www.icet.ac.in/Uploads/Downloads/CNModule%204.pdf)[8](http://becbapatla.ac.in/wp-content/uploads/IT-CN-UNIT2.pdf).  
    **Use Cases**:
    
- **Wine**: TCP-based file transfers.
    
- **Milk**: Video streaming/real-time communications.  
    **FAQs**:
    
- _Why not use one policy universally?_ Different apps have opposing needs (e.g., retransmissions vs. latency).  
    **Key Points**:
    
- Priority tagging (e.g., ATM’s CLP bit) determines which packets to drop first[8](http://becbapatla.ac.in/wp-content/uploads/IT-CN-UNIT2.pdf).
    

## **Random Early Detection (RED)**

**Definition & Purpose**: Proactively drops packets to avoid buffer overflow and TCP synchronization.  
**How It Works**:

- Monitors **average queue length**; drops packets probabilistically when between min/max thresholds[3](https://en.wikipedia.org/wiki/Random_early_detection)[9](https://www.cs.princeton.edu/courses/archive/fall06/cos561/papers/red.pdf).
    
- **Tail Drop Comparison**: RED prevents global TCP slowdowns by spreading drops, unlike tail drop’s all-or-nothing approach[3](https://en.wikipedia.org/wiki/Random_early_detection)[4](https://networklessons.com/cisco/ccie-routing-switching-written/wred-weighted-random-early-detection).  
    **Use Cases**: Congested routers in data centers.  
    **FAQs**:
    
- _How does RED calculate drop probability?_ Linear increase between min/max thresholds (e.g., 0% at min, 100% at max)[9](https://www.cs.princeton.edu/courses/archive/fall06/cos561/papers/red.pdf).  
    **Key Points**:
    
- **Analogy**: Acts like a thermostat, adjusting drops to maintain queue stability.
    

## **Jitter Control**

**Definition & Purpose**: Mitigates delay variation in packet arrival times for real-time apps.  
**How It Works**:

- **Buffering**: Temporarily stores packets to smooth playback (e.g., jitter buffers in VoIP)[10](https://www.techtarget.com/searchunifiedcommunications/definition/jitter)[13](https://cyara.com/blog/what-is-jitter/).
    
- **Timestamping**: Tags packets to reorder them at the receiver[1](http://www.icet.ac.in/Uploads/Downloads/CNModule%204.pdf).  
    **Use Cases**: Video conferencing, online gaming.  
    **FAQs**:
    
- _What’s an acceptable jitter?_ <30 ms for VoIP; >50 ms causes noticeable lag[10](https://www.techtarget.com/searchunifiedcommunications/definition/jitter)[13](https://cyara.com/blog/what-is-jitter/).  
    **Key Points**:
    
- Jitter buffers add latency but prevent skips/gaps.
    

## **Quality of Service (QoS)**

**Definition & Purpose**: Ensures performance for critical apps via bandwidth, latency, and reliability guarantees[6](https://www.fortinet.com/resources/cyberglossary/qos-quality-of-service)[14](https://www.techtarget.com/searchunifiedcommunications/definition/QoS-Quality-of-Service).  
**How It Works**:

- **Traffic Shaping**: Limits bursts using token bucket/leaky bucket algorithms.
    
- **Prioritization**: DiffServ marks packets (e.g., EF for VoIP), while IntServ reserves bandwidth[11](https://www.paloaltonetworks.com/cyberpedia/what-is-quality-of-service-qos)[14](https://www.techtarget.com/searchunifiedcommunications/definition/QoS-Quality-of-Service).  
    **Use Cases**: VoIP, video streaming, cloud gaming.  
    **FAQs**:
    
- _QoS vs. CoS?_ QoS manages bandwidth/latency; CoS prioritizes traffic classes without guarantees[14](https://www.techtarget.com/searchunifiedcommunications/definition/QoS-Quality-of-Service).  
    **Key Points**:
    
- QoS is critical for inelastic traffic (e.g., real-time apps).
    

## **Overprovisioning**

**Definition & Purpose**: Allocating excess bandwidth to handle traffic spikes.  
**How It Works**:

- **Pros**: Simplifies congestion management (e.g., enterprise LANs)[7](https://www.datacore.com/glossary/what-is-overprovisioning/)[12](https://www.acceldata.io/blog/over-provisioning).
    
- **Cons**: Costly and wasteful in WANs with variable traffic[7](https://www.datacore.com/glossary/what-is-overprovisioning/)[12](https://www.acceldata.io/blog/over-provisioning).  
    **Use Cases**: Static environments (e.g., corporate networks).  
    **FAQs**:
    
- _When is dynamic control better?_ For unpredictable traffic (e.g., public clouds)[12](https://www.acceldata.io/blog/over-provisioning).  
    **Key Points**:
    
- Overprovisioning ratio balances cost vs. performance[7](https://www.datacore.com/glossary/what-is-overprovisioning/).
    

## **Key Comparisons**

|**Aspect**|**RED**|**Tail Drop**|
|---|---|---|
|**Congestion Signal**|Early, probabilistic drops.|Drops only at full buffer.|
|**TCP Sync Risk**|Reduces global synchronization.|Causes widespread TCP slowdown.|

|**Strategy**|**Load Shedding**|**Admission Control**|
|---|---|---|
|**Timing**|Reactive (during congestion).|Proactive (blocks new flows).|
|**Impact**|Discards existing traffic.|Prevents new traffic.|

**Exam Tip**: Focus on trade-offs (e.g., overprovisioning’s cost vs. RED’s complexity) and layer-specific tools (QoS at transport vs. jitter control at application).


---
