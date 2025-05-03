→ Congestion
→ Collision
→ Collision detection and collision avoidance

CSMA (carrier sense multiple access) is for multi-point links
Basically, all stations listen to the medium to check if it is busy before sending packets (called *carrier sense*). If it is busy, they wait until it is empty
- does not avoid collision since a station can think a medium is free because an already present signal has not reached it yet
- *Vunerability time is the time frame within which collision is possible*. Here it is the total time taken for a packet to reach all stations (because then all stations will be informed and will not transmit).
![[Pasted image 20250320130525.png]]

Way of checking if medium is free called persistence methods:
- 1 persistence
- non persistence
- p persistence

# CSMA/CD
CSMA/CD → uses a backoff mechanism when collision is detected![[Pasted image 20250402181858.png]]



# CSMA/CA
![[Pasted image 20250414111413 1.png]]
CSMA/CA → uses a probablitity technique to minimize/avoid collision (cannot prevent collision) ![[Pasted image 20250402182041.png]]