***UDP is a connectionless simple protocol***
Because UDP does not provide reliability or flow control, it does not require an established connection. Because UDP does not track information sent or received between the client and server, UDP is also known as a *stateless protocol*.
- UDP does not add anything to IP and just enables process-to-process communication

UDP is also known as a best-effort delivery protocol because there is no acknowledgment that the data is received at the destination. With UDP, there are no transport layer processes that inform the sender of a successful delivery.

> UDP is like placing a regular, nonregistered, letter in the mail. The sender of the letter is not aware of the availability of the receiver to receive the letter. Nor is the post office responsible for tracking the letter or informing the sender if the letter does not arrive at the final destination.

UDP is used for simple request-respond services (like [[DNS - Domain Name Service]], [[DHCP - Dynamic Host Control Protocol]]) and in cases where fast-transfer is more important than errorless-transfer (like Skype, VoIP, Streaming)

UDP uses *socket address* for communication, i.e IP address + port `xxxx.xxxx.xxxx.xxxx:yyyy`


UDP header is only 8 Bytes in size
![[Pasted image 20250601131722.png]]


- **Characteristics:**
    - **Stateless:** Doesn't track the connection.
    - **Fast:** Lower overhead.
    - **No acknowledgments:** Doesn't confirm receipt.
    - **Doesn't resend lost data:** If data is lost, it's gone.
    - **No guaranteed order:** Data arrives in the order it's received.
    - **No flow control:** Doesn't manage sender's rate.
- **Overhead:** Smaller header (Source/Destination Ports, Length, Checksum).
- **Common Applications:** DHCP, DNS, SNMP, TFTP, VoIP, Video Conferencing (where speed is more critical than absolute reliability).
