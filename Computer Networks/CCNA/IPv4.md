***SUBNETTING AND VLSM WILL APPEAR FOR SURE, KNOW HOW TO CALCULATE ADDRESSES AND DO IT ON THE PACKET TRACKER FR FR***

32b → 4 octets (4 x 8b)
Subnet mask → id the network address part of IP address

1. Unicast : packet has destination IP
2. Broadcast : packet has broadcast IP `net.work.ip.255`. routers dont foward broadcast packets
3. Multicast : packet has multicast group IP 
	- IPv4 has reserved the 224.0.0.0 to 239.255.255.255 addresses as a multicast range.
	- OSPF uses multicast

Network address and broadcast address cannot be assigned
*Loopback addresses*  are more commonly identified as only 127.0.0.1, these are special addresses used by a host to direct traffic to itself. For example, it can be used on a host to test if the TCP/IP configuration is operational, as shown in the figure
*Link-local addresses*are more commonly known as the Automatic Private IP Addressing (APIPA) addresses or self-assigned addresses. They are used by a Windows DHCP client to self-configure in the event that there are no DHCP servers available. Link-local addresses can be used in a peer-to-peer connection but are not commonly used for this purpose

Classful addressing:
- **Class A (0.0.0.0/8 to 127.0.0.0/8)** - Designed to support extremely large networks with more than 16 million host addresses. Class A used a fixed /8 prefix with the first octet to indicate the network address and the remaining three octets for host addresses (more than 16 million host addresses per network).
- **Class B (128.0.0.0 /16 - 191.255.0.0 /16)** - Designed to support the needs of moderate to large size networks with up to approximately 65,000 host addresses. Class B used a fixed /16 prefix with the two high-order octets to indicate the network address and the remaining two octets for host addresses (more than 65,000 host addresses per network).
- **Class C (192.0.0.0 /24 - 223.255.255.0 /24)** - Designed to support small networks with a maximum of 254 hosts. Class C used a fixed /24 prefix with the first three octets to indicate the network and the remaining octet for the host addresses (only 254 host addresses per network).
**Note:** There is also a Class D multicast block consisting of 224.0.0.0 to 239.0.0.0 and a Class E experimental address block consisting of 240.0.0.0 - 255.0.0.0.

Now classless addressing is used

- Public IPs are globally routed and need to be unique (not needed for private IP)
- Both Public IPv4 and IPv6 addresses are managed by the Internet Assigned Numbers Authority (IANA). The IANA manages and allocates blocks of IP addresses to the Regional Internet Registries (RIRs). The five RIRs are shown in the figure.
![[Pasted image 20250531181333.png]]
Grouping devices into subnetworks → subnetting. Host bits are used for subnetting

Subnetting with magic number → magic number is the increment/difference beween each subnet mask. example, for 4 subnets the magic number is 64 → `xxxx.xxxx.xxxx.0`, `xxxx.xxxx.xxxx.64` , `xxxx.xxxx.xxxx.128` and `xxxx.xxxx.xxxx.192`



- **Intranet** - This is the internal part of a company’s network, accessible only within the organization. Devices in the intranet use private IPv4 addresses.
- **DMZ** - This is part of the company’s network containing resources available to the internet such as a web server. Devices in the DMZ use public IPv4 addresses.
	- Lack of public IPv4 addresses means VLSM is used (variable subnet length masking) → size of the subnet may vary → subnet mask may vary

VLSM → Subnetting more subnets (nested subnets)
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

