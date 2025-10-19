DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses and network settings (like subnet mask, default gateway, and DNS servers) to devices. This eliminates manual configuration, reducing errors and saving time.  

**Why is DHCP Needed?**  
- Manual IP assignment is impractical for large networks.  
- Devices can join a network without pre-configuration.  
- Ensures efficient IP address management.  

**How DHCP Works (DORA Process)** 

| **Step**  | **Message**     | **Sender** | **Purpose**                                                                 |
|-----------|----------------|------------|-----------------------------------------------------------------------------|
| 1         | DHCPDISCOVER   | Client     | Broadcasts to find available DHCP servers.                                  |
| 2         | DHCPOFFER      | Server     | Responds with an available IP and configuration.                            |
| 3         | DHCPREQUEST    | Client     | Requests the offered IP.                                                    |
| 4         | DHCPACK        | Server     | Confirms the lease and finalizes assignment.                                |
![[Pasted image 20250619195923.png]]

**Other DHCP Messages:**  
- **DHCPDECLINE:** Client reports the IP is already in use.  
- **DHCPNAK:** Server rejects the request (e.g., invalid network).  
- **DHCPRELEASE:** Client returns the IP to the server.  
- **DHCPINFORM:** Client asks only for config (no IP needed).  
---
**Lease Management**  
- IPs are assigned for a limited time (lease).  
- Clients attempt renewal before the lease expires.  
- If renewal fails, the IP returns to the pool for reuse.  

> [!NOTE] What DHCP Provides
> - IP address  
> - Subnet mask  
> - Default gateway  
> - DNS servers  
> - Optional: Domain name, TFTP server, etc.  

**Address Allocation Methods**  
- **Dynamic:** IPs assigned from a pool and reclaimed when unused.  
- **Automatic:** Same as dynamic but prefers assigning the same IP to a device.  
- **Manual (Reservation):** A fixed IP is always assigned to a specific device (by MAC address). 

**DHCP Across Networks**  
If the DHCP server is on a different subnet, a **DHCP relay agent** (usually a router) forwards requests between clients and the server.  

**Why DHCP Matters**  
- Automates network setup.  
- Reduces configuration errors.  
- Optimizes IP address usage.