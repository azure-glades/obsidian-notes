To subnet the Class C IP address 200.1.2.0 into 4 subnets:

## Subnet Configuration
- **Subnet mask**: 255.255.255.192 (using 2 additional bits for subnetting)
- **Hosts per subnet**: 62 usable IPs (26−22^6 - 226−2)
## IP Ranges for Each Subnet

| Subnet | Network Address | Usable Range              | Broadcast Address |
| ------ | --------------- | ------------------------- | ----------------- |
| 1      | 200.1.2.0       | 200.1.2.1 – 200.1.2.62    | 200.1.2.63        |
| 2      | 200.1.2.64      | 200.1.2.65 – 200.1.2.126  | 200.1.2.127       |
| 3      | 200.1.2.128     | 200.1.2.129 – 200.1.2.190 | 200.1.2.191       |
| 4      | 200.1.2.192     | 200.1.2.193 – 200.1.2.254 | 200.1.2.255       |

## Reserved IPs (Cannot Be Configured)
- **Network addresses**: 200.1.2.0, 200.1.2.64, 200.1.2.128, 200.1.2.192
- **Broadcast addresses**: 200.1.2.63, 200.1.2.127, 200.1.2.191, 200.1.2.255
- **Default gateways**: First usable IP in each subnet (e.g., 200.1.2.1 for Subnet 1)

The subnetting leaves 6 bits for host addresses, creating 4 subnets with 62 usable IPs each. Each subnet's first and last IPs are reserved for network/broadcast purposes, while the first usable IP typically serves as the default gateway.