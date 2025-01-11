>[!note] Overallocation
>The assignment of more memory to processes than is physically available on a machine. This can occur in environments such as virtual machines, where multiple instances may not utilize their allocated memory fully at any given time. 
>- For example, if 4 processes each have 10 pages assigned but use only 5 pages. Here a total of 20 pages are wasted pages which could be assigned to other processes and increase cpu utilization.
>- Hence, 4 more processes (total 8) can be loaded and allocated 10 pages each while in reality they only use 5 pages. Here, the computer's memory of 40 pages is fully utilized, by *overallocating* 80 pages of memory
>- If in-case a process needs to use all 10 pages, they have to be replaced with existing processes. this is page replacement

*Definition:*
- **Page replacement** is a memory management scheme that enables an operating system to manage the allocation of pages in memory when a page fault occurs—i.e., when a program tries to access a page that is not currently in physical memory. When this happens, the operating system must decide which page to remove to make space for the new one. The goal is to minimize page faults and optimize performance.

- *Basic page replacement:*  The sequence of steps during page replacement:
	- When a page fault occurs, the required page is located.
		- If there is a free frame, memory is allocated
	- If there is no free frame, an algorithm determines the *Victim Frame*
	- Victim frame is moved to storage and the page is moved to memory
	- Return to page fault
- It is possible to optimize this:
	- If the victim frame has *not undergone any change* since it was initially loaded, then it *need not be copies to storage*
	- Hence, a flag is used to determine whether a frame has been modified or not, called a ***dirty bit*** (***Modify Bit***)
		- If dirty bit = 0 -> no modification, hence no need to copy contents
		- If dirty bit  = 1 -> modification has happened
	- This effectively reduces the requirement for 2 storage accesses to usually 1 (when dirty bit = 0)
### Types of Page Replacement Algorithms
A **reference string** is a sequence of memory addresses that a process accesses during its execution. It serves as a trace of memory access requests, which is crucial for evaluating the performance of page replacement algorithms in operating systems. 
- Each entry in the reference string corresponds to a specific memory location that the process attempts to access.
- Ex: ![[Pasted image 20250108204530.png]] which is reduced to (by looking at the 1st 2-bits i.e frame number)![[Pasted image 20250108204559.png]]

>[!note] Belady's Anomaly
> 1. **Page Faults**: A page fault occurs when a program attempts to access a page that is not currently loaded in physical memory. The operating system must then load the required page from disk, which can be time-consuming.
> 2. **Expected Behavior**: Generally, it is assumed that as the number of available frames increases, the number of page faults should decrease because there is more space to hold pages that are frequently accessed.
> 3. **Paradoxical Result**: However, Belady's anomaly shows that under certain conditions and with specific algorithms (like FIFO), increasing the number of frames can actually lead to more page faults. This happens because the FIFO algorithm may evict pages that would have been beneficial to keep in memory, thus leading to more frequent page faults.

There are several algorithms for page replacement, each with its own strategy:
1. **First-In-First-Out (FIFO)**: This algorithm replaces the oldest page in memory. It maintains a queue of pages; when a page fault occurs, the page at the front of the queue is removed ![[Pasted image 20250108205147.png]]

2. **Optimal Page Replacement**: Theoretical algorithm that cannot be implemented, but it guarantees the lowest possible page faults
	- OPT: *Replace the page that will not be used for the longest time*
	- It requires future knowledge of the reference string

3. **Least Recently Used (LRU)**: LRU replaces the page that has not been used for the longest time. Approximation of the OPT algorithm![[Pasted image 20250108205526.png]] 
2. **LRU Approximation**: This technique approximates LRU without needing extensive bookkeeping. It uses simpler methods, such as reference bits or counters, to track usage
3. **Counting-Based Algorithms**: These algorithms keep track of how often pages are accessed and replace pages based on their frequency of use. For example, Least Frequently Used (LFU) replaces the least frequently accessed pages
