![[Pasted image 20250601171529.png]]

**Presentation Layer**

The presentation layer has three primary functions:

- Formatting, or presenting, data at the source device into a compatible format for receipt by the destination device.
- Compressing data in a way that can be decompressed by the destination device.
- Encrypting data for transmission and decrypting data upon receipt.

As shown in the figure, the presentation layer formats data for the application layer, and it sets standards for file formats. Some well-known standards for video include Matroska Video (MKV), Motion Picture Experts Group (MPG), and QuickTime Video (MOV). Some well-known graphic image formats are Graphics Interchange Format (GIF), Joint Photographic Experts Group (JPG), and Portable Network Graphics (PNG) format.


**Session Layer**

As the name implies, functions at the session layer create and maintain dialogs between source and destination applications. The session layer handles the exchange of information to initiate dialogs, keep them active, and to restart sessions that are disrupted or idle for a long period of time.

- - -

Client and server processes are considered to be in the application layer. The client begins the exchange by requesting data from the server, which responds by sending one or more streams of data to the client. Application layer protocols describe the format of the requests and responses between clients and servers. In addition to the actual data transfer, this exchange may also require user authentication and the identification of a data file to be transferred.

In a P2P network, two or more computers are connected via a network and can share resources (such as printers and files) without having a dedicated server. Every connected end device (known as a peer) can function as both a server and a client. One computer might assume the role of server for one transaction while simultaneously serving as a client for another. The roles of client and server are set on a per request basis.

![[Pasted image 20250601172012.png]]

With P2P applications, each computer in the network that is running the application can act as a client or a server for the other computers in the network that are also running the application. Common P2P networks include the following:
- BitTorrent
- Direct Connect
- eDonkey
- Freenet

Some P2P applications are based on the Gnutella protocol, where each user shares whole files with other users. As shown in the figure, Gnutella-compatible client software allows users to connect to Gnutella services over the internet, and to locate and access resources shared by other Gnutella peers. Many Gnutella client applications are available, including μTorrent, BitComet, DC++, Deluge, and emule.
![[Pasted image 20250601172125.png]]

 Clients use a torrent file to locate other users who have pieces that they need so that they can then connect directly to them. This file also contains information about tracker computers that keep track of which users have specific pieces of certain files. Clients ask for pieces from multiple users at the same time. This is known as a swarm and the technology is called BitTorrent

- - -
Uniform Resource Locator (URL)
HTTP is a request/response protocol. When a client, typically a web browser, sends a request to a web server, HTTP specifies the message types used for that communication. The three common message types are GET (see figure), POST, and PUT:
- **GET** - This is a client request for data. A client (web browser) sends the GET message to the web server to request HTML pages.
- **POST** - This uploads data files to the web server, such as form data.
- **PUT** - This uploads resources or content to the web server, such as an image.

![[Pasted image 20250601172544.png]]
Simple Mail Transfer Protocol (SMTP), Post Office Protocol (POP), and IMAP.
- The application layer process that sends mail uses SMTP.
- A client retrieves email using one of the two application layer protocols: POP or IMAP.


- - -
FTP : ![[Pasted image 20250601174144.png]]

The Server Message Block (SMB) is a client/server file sharing protocol that describes the structure of shared network resources, such as directories, files, printers, and serial ports. It is a request-response protocol. All SMB messages share a common format. This format uses a fixed-sized header, followed by a variable-sized parameter and data component.

Here are three functions of SMB messages:
- Start, authenticate, and terminate sessions.
- Control file and printer access.
- Allow an application to send or receive messages to or from another device.
Samba shares use SMB

FTP client-server have 2 connections (port 20 and 21)

`nslookup` shows ip address of domains

The Dynamic Host Configuration Protocol (DHCP) for IPv4 service automates the assignment of IPv4 addresses, subnet masks, gateways, and other IPv4 networking parameters. This is referred to as dynamic addressing. The alternative to dynamic addressing is static addressing. When using static addressing, the network administrator manually enters IP address information on hosts.

The DNS server stores different types of resource records that are used to resolve names. These records contain the name, address, and type of record. Some of these record types are as follows:

- **A** - An end device IPv4 address
- **NS** - An authoritative name server
- **AAAA** - An end device IPv6 address (pronounced quad-A)
- **MX** - A mail exchange record

---

**OSI Layers (Application, Presentation, Session)**

- **Application Layer (OSI L7 / TCP/IP Application):** Closest to user; exchanges data between programs; protocols define format/control for common internet functions (e.g., HTTP, FTP).
- **Presentation Layer (OSI L6):** Formats, compresses, encrypts/decrypts data for compatible transmission/receipt.
- **Session Layer (OSI L5):** Manages communication dialogues (initiate, keep active, restart) between applications.

**Networking Models (Client/Server & Peer-to-Peer)**

- **Client/Server:** Client requests info, Server responds. Dedicated server.
- **Peer-to-Peer (P2P):** Computers act as both client and server; share resources directly without dedicated server.
    - **Hybrid P2P:** Decentralized sharing, but centralized index for resource locations.
    - **Torrent Files:** Small files help clients find other users for pieces of files; trackers monitor piece distribution.

**Web and Email Protocols**

- **HTTP (Hypertext Transfer Protocol):** Request/response protocol for web services. Uses GET, POST, PUT message types.
- **HTTPS (HTTP Secure):** HTTP with SSL/TLS encryption for secure web communication.
- **Email Protocols:**
    - **SMTP (Simple Mail Transfer Protocol):** Used by clients to send mail to a mail server. Requires header (recipient, sender) and body.
    - **POP (Post Office Protocol):** Client retrieves mail from server; mail is _downloaded and deleted_ from server.
    - **IMAP (Internet Message Access Protocol):** Client retrieves mail; _copies_ are downloaded, _originals kept on server_ until manually deleted.

**IP Addressing Services**

- **DNS (Domain Name System):** Resolves resource names to numeric IP addresses. Uses hierarchical structure; servers manage specific zones. `Nslookup` tool queries DNS manually.
- **DHCP for IPv4:** Automates IPv4 address, subnet mask, gateway, and other parameters assignment.
    - **Process:** Client broadcasts DHCPDISCOVER -> Server replies with DHCPOFFER.
- **DHCPv6:** Similar to DHCPv4, but does _not_ provide a default gateway address.
    - **Messages:** SOLICIT, ADVERTISE, INFORMATION REQUEST, REPLY.

**File Sharing Services**

- **FTP (File Transfer Protocol):** Client pushes/pulls data from FTP server.
    - Uses **two TCP connections**:
        1. **Control Connection (TCP port 21):** For commands and responses.
        2. **Data Connection (e.g., TCP port 20 or dynamic):** For actual file transfer.
- **SMB (Server Message Block):** Protocol for file and printer sharing.
    - Functions: Start/authenticate/terminate sessions, control file/printer access, send/receive messages between devices.
    - Clients establish **long-term connections** to servers, making shared resources appear local.