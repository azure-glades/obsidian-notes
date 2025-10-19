>[!note] **Overallocation**
>The assignment of more memory to processes than is physically available on a machine. This can occur in environments such as virtual machines, where multiple instances may not utilize their allocated memory fully at any given time. 
>- For example, if 4 processes each have 10 pages assigned but use only 5 pages. Here a total of 20 pages are wasted pages which could be assigned to other processes and increase cpu utilization.
>- Hence, 4 more processes (total 8) can be loaded and allocated 10 pages each while in reality they only use 5 pages. Here, the computer's memory of 40 pages is fully utilized, by *overallocating* 80 pages of memory
>- If in-case a process needs to use all 10 pages, they have to be replaced with existing processes. this is page replacement

*Definition:*
- **Page replacement** is a memory management scheme that enables an operating system to manage the allocation of pages in memory when a page fault occurs—i.e., when a program tries to access a page that is not currently in physical memory. When this happens, the operating system must decide which page to remove to make space for the new one. The goal is to minimize page faults and optimize performance.
****
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
## Types of Page Replacement Algorithms
A **reference string** is a sequence of memory addresses that a process accesses during its execution. It serves as a trace of memory access requests, which is crucial for evaluating the performance of page replacement algorithms in operating systems. 
- Each entry in the reference string corresponds to a specific memory location that the process attempts to access.
- Ex: ![[Pasted image 20250108204530.png]] which is reduced to (by looking at the 1st 2-bits i.e frame number)![[Pasted image 20250108204559.png]]

>[!note] Belady's Anomaly
> 1. **Page Faults**: A page fault occurs when a program attempts to access a page that is not currently loaded in physical memory. The operating system must then load the required page from disk, which can be time-consuming.
> 2. **Expected Behavior**: Generally, it is assumed that as the number of available frames increases, the number of page faults should decrease because there is more space to hold pages that are frequently accessed.
> 3. **Paradoxical Result**: However, ***Belady's anomaly*** shows that under certain conditions and with specific algorithms (like FIFO), increasing the number of frames can actually lead to more page faults. This happens because the FIFO algorithm may evict pages that would have been beneficial to keep in memory, thus leading to more frequent page faults.

There are several algorithms for page replacement, each with its own strategy:
### 1. First-In-First-Out (FIFO)
 This algorithm replaces the oldest page in memory. It maintains a queue of pages; when a page fault occurs, the page at the front of the queue is removed ![[Pasted image 20250108205147.png]]

### 2. Optimal Page Replacement
An algorithm that mathematically minimizes page fault rate. A theoretical algorithm that cannot be implemented in practice since it requires the future usage rate and order of the pages.
	- OPT: *Replace the page that will not be used for the longest time*
	- It requires future knowledge of the reference string
	- OPT avoids belady's anomaly

### 3. Least Recently Used (LRU)
The victim page is the least recently used page. It is an approximation of OPT, and is a part of a class of algorithms called *stack algorithms* that avoid incurring Belady's anomaly. ![[Pasted image 20250108205526.png]]
- Merely assumes that the least recently used page will not be used again for some time. But there is no guarantee that because it is least recently used it will be needed soon.
LRU is implemented using hardware or data structures, but it incurs big overheads for checking/calculating
- **Using Counters:** Page table contains an additional field storing the last time of page access. Time of access is a counter that increments any time a page is accessed.
	- When a page is accessed, its "time of last access" field is updated
	- The page with the lowest "time of last access" field is the victim
	- Has a large overhead since a counter needs to be maintained and the last accessed page has to be searched
- **Using Stack/Doubly linked list:** Applying LIFO to LRU, the last accessed page will be at the bottom of the stack. This is taken advantage of by
	- Last accessed page is searched from the stack and pushed to the top
	- Implemented using a doubly linked list for easy removal, but there is a lot of pointers involved which make each operation more expensive

### 4. LRU Approximation
Least Recently Used (LRU) approximation algorithms are designed to manage memory efficiently by approximating the LRU page replacement strategy.
#### 4.1. Additional Reference Bit algorithm
An extra reference bit is used to keep track of page usages. Whenever a page is used, it is set to 1. A timer increments the bits of all pages, and hence the page table stores the usage rate of all pages over the last 8 cycles.
- This approximates the "time of last access" field used in LRU
- Ex: 00000000 : Page has not been used; 1010 1101 : Page has been used 5 times in the last 8 cycles, it was last used a cycle ago; 1110 0000 : Page has been used 3 times, it was last used 5 cycles ago
#### 4.2. Second Chance Algorithm
FIFO algorithm, but a reference bit is used to give the victim page a second chance.
- If a page is used, its reference bit is set to 1
- When a victim page is selected by FIFO, the reference bit is checked. If it is 1, it is given a *second chance* and FIFO selects the next page
- Often implemented as a circular queue![[Pasted image 20250113093343.png]]
#### Enhanced Second Chance Algorithm
Second chance algorithm but it includes the *dirty bit* also.
- 00 -> Not recently used or modified, best page to replace 
- 01 -> Not recently used but modified, page will need to be written out
- 10 -> Recently used but not modified, might be used again
- 11 -> Recently used and modified, will probably be used again
Works just like second chance. Victims are identified in FIFO order and their dirty bit + reference bits are checked. Reference bit is higher priority than dirty bit
### 5. Counting Based Algorithms
Utilize a counter to maintain the number of times a page is used.
- **Least Frequently Used (LFU):** The page with lowest count is the victim page.
	- Sometimes a page is used heavily in the beginning stages of a program (giving it a high count) and is then never used. This page will never be the victim due to its high count.
	- One solution is to make the counts decay over time
- **Most Frequently Used (MFU):** The page with highest count is the victim page. Assumes that the most recently brought page will have the lower count and hence should not be replaced.
They are not good approximations of OPT and have a high overhead to implement
### 6. Page Buffering Algorithms
Maintain a pool of free frames (called *page buffers*) that are called when a page fault occurs.
- While the victim page is being written out, the demanded page is loaded into memory using the free frames from the pool which increases response time
- Once the victim is written out, its frame is added to the free frames list
A list of modified pages are also maintained, using the dirty bit to identify such pages.
- When the paging hardware (usually MMU) is idle, these modified pags can be rewritten to storage and their dirty bit is switched. This increases the number of possible victim pages and decreases the high overhead incurred during a page fault, since it has already been written out previously
Similarly, pages linked to the frames in the free frame pool are stored.
- When the page (who's mapped frame is in the free frame pool) is demanded, the pool can allocate that frame again without having to copy memory from secondary storage.
- When page fault occurs, the desired page is checked in the free-frame pool to see if its frames already exist.