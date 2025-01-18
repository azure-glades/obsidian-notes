*Definition:*
	**Non-Uniform Memory Access (NUMA)** is a computer memory architecture used in multiprocessing systems where the access time to memory varies based on the memory location relative to the processor. In a NUMA system, each processor has its own local memory, which allows for faster access compared to non-local memory that is associated with other processors.![[Pasted image 20250114112935.png]]

Processors can access their immediate local memory much faster than other memory units. These units are also used to communicate and share memory across processors.
- Due to the difference in access times, pages in local memory have faster access times than those in other locations
- When page-faults occur, new pages are allocated as close as possible to the faulting CPU
- Separate free-frame pools are kept for each memory unit

The *Linux CFS scheduler* (Completely Fair Scheduler) uses a hierarchy of scheduling domains, i.e identifying memory addresses that have faster or slower access times and assigning with this in mind to maximize speed.
