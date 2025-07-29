IPv4 address is 32 bits long
Ex: IPv4 has 4 segments. Each *octet* is **8 bits** long.
`192.168.10.10` translates to `11000000.10101000.00001010.00001010`
It is written decimal to make it more readable	

IPv6 addresses are 128 bits long
Format: `x:x:x:x : x:x:x:x` = Each part (called *hexlet*) is **16 bits** long
16\*8 = 128

Subnet mask → id the network address part of IP address

1. Unicast : packet has destination IP
2. Broadcast : packet has broadcast IP `xxxx.xxxx.xxxx.255`. routers dont foward broadcast packets
3. Multicast : packet has multicast group IP 
	- IPv4 has reserved the 224.0.0.0 to 239.255.255.255 addresses as a multicast range.
	- OSPF uses multicast

Network address and broadcast address cannot be assigned
1. *Loopback addresses*  are more commonly identified as only 127.0.0.1, these are special addresses used by a host to direct traffic to itself. For example, it can be used on a host to test if the TCP/IP configuration is operational, as shown in the figure
2. *Link-local addresses*are more commonly known as the Automatic Private IP Addressing (APIPA) addresses or self-assigned addresses. They are used by a Windows DHCP client to self-configure in the event that there are no DHCP servers available. Link-local addresses can be used in a peer-to-peer connection but are not commonly used for this purpose

Classful addressing:

| **Class** | **Address Range**          | **Prefix** | **Network/Host Division** | **Hosts per Network** | **First Bits** | **Purpose** |
|-----------|----------------------------|------------|---------------------------|-----------------------|----------------|-------------|
| **A**     | 0.0.0.0 - 127.255.255.255  | /8         | 1 octet network<br>3 octets host | 16,777,214           | 0              | Large networks |
| **B**     | 128.0.0.0 - 191.255.255.255 | /16        | 2 octets network<br>2 octets host | 65,534               | 10             | Medium networks |
| **C**     | 192.0.0.0 - 223.255.255.255 | /24        | 3 octets network<br>1 octet host | 254                  | 110            | Small networks |
| **D**     | 224.0.0.0 - 239.255.255.255 | N/A        | N/A                       | N/A                  | 1110           | Multicast |
| **E**     | 240.0.0.0 - 255.255.255.255 | N/A        | N/A                       | N/A                  | 1111           | Experimental |

**Key Notes:**
1. Class A-C were used for standard host addressing
2. Class D was reserved for multicast groups
3. Class E was reserved for experimental purposes
4. The system was inefficient and replaced by CIDR (Classless Inter-Domain Routing)
5. Modern networks use VLSM (Variable Length Subnet Masking) instead


Now classless addressing is used - No classes exist
- Public IPs are globally routed and need to be unique (not needed for private IP)
- Both Public IPv4 and IPv6 addresses are managed by the Internet Assigned Numbers Authority (IANA). The IANA manages and allocates blocks of IP addresses to the Regional Internet Registries (RIRs). The five RIRs are shown in the figure.


private IPv4 address blocks defined by RFC 1918:  

| **Class** | **Private Address Range**       | **CIDR Notation**      | **Number of Addresses** | **Typical Use Case**       |
|-----------|--------------------------------|-----------------------|------------------------|---------------------------|
| **A**     | 10.0.0.0 – 10.255.255.255      | 10.0.0.0/8           | 16,777,216             | Large enterprises, ISPs   |
| **B**     | 172.16.0.0 – 172.31.255.255    | 172.16.0.0/12        | 1,048,576              | Medium businesses         |
| **C**     | 192.168.0.0 – 192.168.255.255  | 192.168.0.0/16       | 65,536                 | Home/Small office networks |
### Key Notes:
1. **Non-Routable on the Internet**: These addresses are reserved for internal networks and are not globally unique.  
2. **NAT Required**: To access the internet, devices using private IPs must go through [[NAT - Network Address Translation]] 
3. **Common Uses**:  
   - **10.0.0.0/8**: Used in large corporate networks (e.g., data centers).  
   - **172.16.0.0/12**: Often seen in enterprise branch offices.  
   - **192.168.0.0/16**: Default for most home routers (e.g., 192.168.1.0/24).  


Grouping devices into [[Subnets]] → subnetting. Host bits are used for subnetting

Subnetting with magic number → magic number is the increment/difference beween each subnet mask. example, for 4 subnets the magic number is 64 → `xxxx.xxxx.xxxx.0`, `xxxx.xxxx.xxxx.64` , `xxxx.xxxx.xxxx.128` and `xxxx.xxxx.xxxx.192`


- **Intranet** - This is the internal part of a company’s network, accessible only within the organization. Devices in the intranet use private IPv4 addresses.
- **DMZ** - This is part of the company’s network containing resources available to the internet such as a web server. Devices in the DMZ use public IPv4 addresses.
	- Lack of public IPv4 addresses means VLSM is used (variable subnet length masking) → size of the subnet may vary → subnet mask may vary

**VLSM - Variable length subnet mask** → Subnetting more subnets (nested subnets)
- When your subnets need a varying number of hosts, ex: 
	- network 1 - 200 hosts - 256
	- network 2 - 100 hosts - 128
	- network 3 - 50 hosts - 64
	- network 4 - 25 hosts - 32
	- network 5 - 10 hosts - 16
- Now you subnet from greater. Each consequtive subnet has a different (longer) subnet mask. Suppose network : `172.16.0.0`
	- subnet 1: 172.16.0.0-255/24 (256)
		- subnet 172.16.1.0-127/25 (128)
			- 172.16.1.128-191/26 (64)
				- 172.16.1.192-223/27 (32)
					- 172.16.1.224-239 (16)
- Basically VLSM is used divide subnets into more subnets

