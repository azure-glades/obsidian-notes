*Definition:*
	**Thrashing** is a phenomenon in operating systems where a computer spends a significant amount of time swapping data between physical memory (RAM) and secondary storage (such as a hard disk) rather than executing actual processes.

>*How does thrashing occur?*
>1. When CPU utilization drops, the scheduler schedules more processes to maintain utilization
>2. These processes get pages allocated by a replacement algorithm by demand paging
>3. The previous running processes require those pages/enter new phases of execution, so they begin demanding pages too
>4. They start page faulting, and the pages of the new processes gets replaced
>5. This ends up in a negative cycle where they are continuous faulting pages
>6. The paging device gets fully utilized and processes begin piling up waiting for the paging hardware to catch-up and allocate them pages
>7. Processes begin filling up wait-queue and the CPU is left empty with minimum utilization
>8. The scheduler sees the dropping utilization and begins to send more processes to the CPU
>9. These processes again demand pages and fill up the paging device and cause more page faults
>10. This creates a run away affect of continuous page faulting and processes entering CPU and overloading the paging hardware

![[Pasted image 20250115102136.png]]

- Thrashing can be minimized with local replacement algorithm or priority replacement algorithm

> The current strategy to prevent thrashing is to include enough physical memory such that the entire working-set can be stored in memory.
### 1. Locality Model
The locality model states that, as a process executes, it moves from *locality* to *locality*. A locality is a set of pages that are actively used together. A running program is generally composed of several different localities, which may over-lap.
- A locality is just the common set of memory pages it is referencing. These localities change as the program progresses through different phases of execution and switches between different functions. There may be some overlap between the localities.
	- Ex: Phase 1: {12,13,14,26,27,28,30,31}, Phase 2: {15,16,17,18,27,28,29,30}. Here Each phase has a distinct locality which is a collection of pages. After a while when it switches to phase 2, its locality changes but there is an overlap of some pages (namely 27,28,30)
	- Due to demand paging, in any given phase of execution, its locality of pages must be loaded in memory/allocated pages. This is because the process will be using these pages continuously will be accessing them regularly. It is necessary for the locality to be loaded in memory.
		- If at a given point, the entire locality is unable to be loaded in memory, the process will be faulting regularly to load specific pages back into memory.
		- Hence, if we do not allocate sufficient frames for a locality to retain all pages in memory, it causes *thrashing* since it will continuous page-fault to load its required pages into memory

### 2. Working-Set Model
The working set model is an attempt to use the localities that exist for different processes. It looks back in memory and defines the latest few pages that have been called in the time-span to be the locality for a process. This is the *working set of pages* for the process.
- The OS then monitors the working set of each process and makes sure it is fully loaded in memory
- The sum of all the working-sets of all the processes is called the *total demand*. If the total demand is greater than the total number of available frames, *thrashing will occur*.

The working set model uses a few variables, defined as:
- The *working set window* $\Delta$ which is the time range which we consult. All pages that have been called in the last $\Delta$ seconds are the *working set*
	- Accuracy of the working-set with locality depends on the size of $\Delta$. If $\Delta$ is too small, it will not encompass the full locality. If $\Delta$ is too big, it may overlap multiple localities. (If $\Delta$ is infinity, then working-set will be the complete list of all pages referenced during its execution)
- The number of pages in the working-set is the *working set size, WSS*
- The sum of WSS for all processes is the *demand* $D = \sum WSS_i$  
	- If $D > m$ then thrashing occurs, where $m$ is the *number of available frames*
![[Pasted image 20250115183040.png]]

### 3. Page-Fault Frequency (PFF)
Thrashing is characterized by an extremely high page-fault rate. This strategy deals with controlling and maintaining the *page-fault frequency* within a pre-defined range.
- When page-fault rate is high, the process does not have enough frames allocated
- When the page-fault rate is low, the process may have extra frames allocated
An upper and lower bound is set and whenever the PFF crosses these limits, a frame is allocated or removed from a process.