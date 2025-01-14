**Definition:**
	The separation of logical memory from physical memory, allowing a much larger, and abstract *virtual memory* to exist for utilization by processes.
The *virtual address space* is the virtual view of a process stored in memory. A process is allocated virtual memory that is mapped onto physical memory during execution
- **Advantage**
	- Allows for discontinuous allocation of pages/frames to processes which prevents external fragmentation of memory
	- System libraries and reentrant code can be shared by several processes by mapping the physical memory onto different virtual address spaces given to different processes
	- Processes can share virtual memory and allow for inter-process communication
	- Pages can be shared across child processes by a parent process without needing new mapping of physical addresses.

Managing virtual memory:
-> [[Demand Paging]]
-> [[Copy-on-Write]]
-> [[Page Replacement Algorithms]]
-> [[Frame Allocation Algorithms]]