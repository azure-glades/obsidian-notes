The layer that handles sending data across links
- No encapsulation occurs here
- Modems, Signal generators, and signal processing devices are present
- *Bits* are the basic unit of data that is transferred

- **Bandwidth** is the capacity at which a medium can carry data. (bits per second - bps)
- **Latency** refers to the amount of time, including delays, for data to travel from one given point to another.
- **Throughput** is the measure of the transfer of bits across the media over a given period of time.
	- **Goodput** is the measure of usable data transferred over a given period of time. Goodput is throughput minus traffic overhead for establishing sessions, acknowledgments, encapsulation, and retransmitted bits
# Transmission Modes
Data transmission modes define how information is sent between devices, focusing on the direction and method of data flow.
![[Pasted image 20250407193033.png]]
## Parallel Transmission
Grouping and transferring n bits of data in n different channels in a single clock cycle is parallel transmission.
*Advantage:* Transmission speed is high
*Disadvantage:* More expensive
![[Pasted image 20250407195935.png]]

## Serial Transmission
All bits are transferred in a single channel, taking up n clock cycles to transmit is serial transmission
*Advantage:* Cost effective
*Disadvantage:* Expensive
1. **Asynchronous:**
2. **Synchronous:**
3. **Isochronous:**

![[Pasted image 20250521094516.png]]