shaping the flow of traffic → done by the server side
user and subnet agree to a traffic pattern called *service level agreement*

## Leaky bucket algorithm
- Uneven flow of packets from host gets evened out into a regular flow of packets
- Drops fall unevenly into the bucket, but the bucket leaks evenly.
leaky bucket is a finite internal queue. packets arrive in various bursts but processing is done regularly and the server sents it out in a constant stream.

- If leaky bucket queue is full, then any extra data has to be dropped
## Token bucket algorithm
- The bucket stores tokens which is a collection of data, usually the data from a single burst is a token.
- hence tokens are processed regularly and the output is transmitted regularly
- tokens are generated at every interval of del-T which stores the packets received in that time slot

# Resource reservation
network resources are reserved for transmission (usually bandwidth, buffer and cpu cycle). high resource processes are allocated more resources or are throttled to prevent congestion. all transmission needs to request and get access to transmit across network

Proportional routing → splitting the traffic by sending the packets over different paths
Packet Scheduling → Different queues for different output lines and the packets are divided and sent across different output lines. Weighted fair queuing algorithm
# Admission control
controlling the admission of packets into the router
when flow is offered to router, it decides whether to admit or reject a packet
