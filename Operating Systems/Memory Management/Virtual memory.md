**Definition:**
	The separation of logical memory from physical memory, allowing a much larger, and abstract *virtual memory* to exist for utilization by processes.
The *virtual address space* is the virtual view of a process stored in memory. A process is allocated virtual memory that is mapped onto physical memory during execution
- **Advantage**
	- Allows for discontinuous allocation of pages/frames to processes which prevents external fragmentation of memory
	- System libraries and reentrant code can be shared by several processes by mapping the physical memory onto different virtual address spaces given to different processes
	- Processes can share virtual memory and allow for inter-process communication
	- Pages can be shared across child processes by a parent process without needing new mapping of physical addresses.
## Demand Paging
- Where pages are allocated to a process only when requested, i.e *on demand*.
- A process has to demand for more memory during execution, and the MMU allocates it virtual memory. Pages are only mapped onto physical memory once they are accessed
- If a process attempts to access memory outside its range without demanding, it is terminated
### 1. Free-Frame list
## Copy-on-Write
A method of quickly allocating memory to processes (especially child processes) without demanding for more memory.
- Done by sharing pages of the parent process to the child processes when `fork()` is called.
- Since most child processes are assigned different tasks via `execl()` physical addresses need not be immediately mapped to the child process
	- Hence, only when the child requests/*writes* onto the shared page, new physical memory is mapped.
	- This prevents shared but unmodified pages from being translated and saves a huge CPU overhead.
	- When a child writes onto a page, a *copy* of the page is created and mapped, and is allocated to the child process. (Hence, *copy-on-write*)
	- These shared and modifiable pages are called *copy-on-write pages*
![[Pasted image 20241231171807.png]]
![[Pasted image 20241231171814.png]]

## Page Replacement
## Frame allocation
## Thrashing