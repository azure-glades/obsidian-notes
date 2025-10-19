***TCP is connection oriented , full-featured transport layer protocol***, which ensures that all of the data arrives at the destination. TCP includes fields which ensure the delivery of the application data. These fields require additional processing by the sending and receiving hosts.
- TCP divides data into segments.
- All TCP connections are *full duplex* and *point-to-point*

> TCP transport is analogous to sending packages that are tracked from source to destination. If a shipping order is broken up into several packages, a customer can check online to see the order of the delivery.

TCP is used by various services that prioritize security and error-free transfer of data, like HTTP, FTP, SSH and SMTP

TCP Services:
- **Establishes a Session** - TCP is a connection-oriented protocol that negotiates and establishes a permanent connection (or session) between source and destination devices prior to forwarding any traffic. Through session establishment, the devices negotiate the amount of traffic that can be forwarded at a given time, and the communication data between the two can be closely managed.
- **Ensures Reliable Delivery** - For many reasons, it is possible for a segment to become corrupted or lost completely, as it is transmitted over the network. TCP ensures that each segment that is sent by the source arrives at the destination.
- **Provides Same-Order Delivery** - Because networks may provide multiple routes that can have different transmission rates, data can arrive in the wrong order. By numbering and sequencing the segments, TCP ensures segments are reassembled into the proper order.
- **Supports Flow Control** - Network hosts have limited resources (i.e., memory and processing power). When TCP is aware that these resources are overtaxed, it can request that the sending application reduce the rate of data flow. This is done by TCP regulating the amount of data the source transmits. Flow control can prevent the need for retransmission of the data when the resources of the receiving host are overwhelmed.
*TCP does not support broadcasting or multicasting*

TCP Header is 20 Bytes but can go up-to 60 Bytes
![[Pasted image 20250620105555.png]]
There are 10 fields in the header
Control segment of the TCP Header is 6 bits, each called as a flag. There are 6 control flags that tell what task the packet is doing
- **URG** - Enables the urgent field
- **ACK** - Acknowledgment flag used in connection establishment and session termination
- **PSH** - Push function. Instruct the receiving side to deliver the data to the application immediately. Reduces delay
- **RST** - Reset the connection when an error or timeout occurs
- **SYN** - Synchronize sequence numbers used in connection establishment
- **FIN** - No more data from sender and used in session termination
Multiple flags can be enabled at once. Ex: In 3-way handshake, both ACK and SYN are set

# TCP Connection Establishment
Uses the *Three way handshake*, where 3 packets are exchanged. Each TCP session is one-way. So to setup a duplex communication, 2 TCP sessions have to be set-up
1. **Initiate a communication session**: The client sends a SYN (synchronize) packet to the server to start a client-to-server session
	- Control Bit (`CTL`) is set to `SYN` ![[Pasted image 20250620111121.png]]
2. **Server ACK and initiates communication session:** The server acknowledges in the incoming connection and requests an outgoing server-to-client session
	- Control bit is set to `SYN/ACK`. Both acknowledgement and synchronize is sent in the same packet ![[Pasted image 20250620111400.png]]
3. **Client ACK:** The client acknowledges with an ACK packet
	- Control bit is set to `ACK` ![[Pasted image 20250620111451.png]]

# TCP Connection Termination
Each TCP session needs two-way handshake to terminate. So to terminate a connection, 4 exchanges of packets are done (2 two-way handshakes)
1. **Client initializes termination:** Sends a packet with control bit = `FIN` to end the connection 
![[Pasted image 20250620111838.png]]
2. **Server ACK termination:** Server sends an ACK which terminates the client-to-server session
![[Pasted image 20250620112030.png]]
3. **Server initializes termination:** Server sends a `FIN` packet to terminate the server-to-client session
![[Pasted image 20250620112049.png]]
4. **Client ACK:** Client acknowledges this with an ACK
![[Pasted image 20250620112059.png]]