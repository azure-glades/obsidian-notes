The transport layer is responsible for logical communications between applications running on different hosts. This may include services such as establishing a temporary session between two hosts and the reliable transmission of information for an application.

The transport layer has no knowledge of the destination host type, the type of media over which the data must travel, the path taken by the data, the congestion on a link, or the size of the network.
2 main protocols: 
- [[TCP - Transmission Control Protocol]]
- [[UDP - User Datagram Protocol]]
![[Pasted image 20250620095056.png]]

Port numbers are transport layer addresses that are used by both TCP and UDP
The address in IP header and the address in transport header are both required for communication. This combination is called a *socket address*
-  A client socket might look like this, with 1099 representing the source port number: `192.168.1.5:1099`
- The socket on a web server might be `192.168.1.7:80`
- These two sockets combine to form a _socket pair_: `192.168.1.5:1099, 192.168.1.7:80`

Sockets enable multiple processes, running on a client, to distinguish themselves from each other, and multiple connections to a server process to be distinguished from each other.
- The source port number acts as a return address for the requesting application. The transport layer keeps track of this port and the application that initiated the request so that when a response is returned, it can be forwarded to the correct application.

Ports are grouped by the IANA
![[Pasted image 20250620110559.png]]

Some standard ports
![[Pasted image 20250620110650.png]]