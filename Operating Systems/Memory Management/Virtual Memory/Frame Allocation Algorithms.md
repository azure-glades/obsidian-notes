*Definition:* 
	A **frame of memory**, also known as a **page frame**, is a fixed-length contiguous block of physical memory that corresponds to a specific size defined by the system's page size.
- Frames are used by the MMU to manage physical memory and enable virtualization
- All existing frames are accessed via a frame table
	- A pool of free frames is maintained, called  *free frame list*
- The number of frames allocated to a process significantly impacts performance. Insufficient frames can lead to increased page-fault rates, which slow down execution due to the overhead involved in handling these faults

Minimum number of frames per process is defined mainly by the computer architecture (more specifically, the instruction set)
- If pointers are involved in instructions, then atleast 3 frames of memory are needed (1 for the instruction, 1 for the pointer, 1 for the address stored in pointer). In this case the minimum frames for a process is 3 (assuming a process has 1 instruction only)
- The maximum frames for a process is defined by the OS and may even be all the frames in memory
-> An aside, [[Non Uniform Memory Access]]
## Allocation Algorithms
Algorithms that decide the allocation, transfer and handling of frames between pages
- **Equal Allocation**: Where the number of frames are divided equally among all processes
- **Proportional Allocation:** Where frames are allocated to each process according to its relative
	- Ex: Let processes $p_i$ have size $s_i$ from a total sum of all processes $S$ . Of course $S = \sum s_i$ . The number of frames allocated to $p_i$ is $a_i$ which is $$a_i = \frac{s_i}{S}*m$$ and $m$ is the total number of available frames
	- Proportional allocation can also be done based on *priority*
## Global vs Local allocation
Page replacement algorithms can be divided as global and local
- **Global replacement** allows a process to select a replacement frame from the set of all frames, even if that frame is currently allocated to some other process; that is, one process can take a frame from another.
- **Local replacement** requires a process to select a replacement frame from its own set of allocated frames.
Generally, high priority processes use global replacement strategy where they can sacrifice low priority processes by taking their frames.
- In global replacement, the performance of a process depends on its paging behaviour and *the paging behaviour of other processes* (since a higher priority process can interrupt its execution by stealing its frames. Effectively bullying it)
- In local replacement, the performance of processes with sufficient memory is high, but processes that require more end up with worse performance
Global replacement improves *system performance*, hence it is more commonly used

>[!note]+ Major and Minor Page Faults
>- A *major page fault* is when a page is referenced, but is not in memory and needs to be loaded from storage and assigned frames (*hard faults* in windows).
>	- Happens initially due to demand paging
>- A *minor page fault* occurs in computing when a process attempts to access a memory page that is already present in physical memory but is not correctly mapped in the memory management unit (MMU) for that specific process (*soft fault* in windows)
>	- Happens due to shared pages/libraries present in memory not being assigned to a process
>	- to view page faults: `ps -eo min_flt,maj_flt,cmd`

To ensure consistent performance, a portion of memory is kept free as a part of the free frame pool and buffer. This pool caters to sudden surges in memory usage and prevents the processes from scrambling for memory and thrashing.
- When free memory drops below a threshold, the OS calls ***reapers*** which are kernel routines that identify and reclaim pages/frames and add them to the free frame pool.
	- They use a type of LRU to identify and remove pages
- When free memory drops to dangerously low values, Linux has ***out-of-memory killers (OOM KILLERS)*** that select processes and terminate them to free up memory.
	- Each process has an OOM score which is used to determine which process gets killed. The OOM score depends on the size of the process (Can be viewed in `/proc/{process id}/oom_score`)
