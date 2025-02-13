- Where pages are allocated to a process only when requested, i.e *on demand*. Only necessary pages of a program are loaded
- A process has to demand for more memory during execution, and the MMU allocates it virtual memory. Pages are only mapped onto physical memory once they are accessed
- When a program tries to access a page that is not currently in memory, a *page fault* occurs. The operating system then retrieves the required page from secondary storage (like a hard disk) and loads it into RAM.

> [!note] **Page Fault**
> A *page fault* is an exception raised by the memory management unit (MMU) when a process attempts to access a memory page that is not currently loaded in physical memory (RAM). This event signals the operating system (OS) to retrieve the required page from secondary storage, such as a hard disk or SSD, and load it into RAM for the process to continue execution
> Handling a page fault:
> 1. **Detection**: The hardware detects the page fault and interrupts the current process, transferring control to the OS kernel
> 2. **Address Validation**: The OS checks whether the requested page is valid and if it exists in secondary storage (backing store/swap space)
> 3. **Page Replacement**: If there is no free space in RAM, the OS must decide which existing page to evict. This decision can be based on various algorithms, such as Least Recently Used (LRU) or First-In-First-Out (FIFO)
> 4. **Loading the Page**: The required page is loaded from disk into RAM and is allocated a free frame
> 5. **Updating Page Tables**: The OS updates the page table to reflect that the new page is now in memory and accessible by the process
> 6. **Resuming Execution**: Finally, the OS resumes execution of the interrupted process, allowing it to continue as if no fault had occurred
> ![[Pasted image 20250102164809.png]]

## Performance
The efficiency of demand paging is calculated by effective access time.
- If there is no page fault : effective access time = memory access time
- If there is page fault : effective access time = memory access time + page fault time
$$effective\ access\ time = (1 − p) × (memory\ access\ time) + p × (page\ fault\ time).$$
where $p$ is *page-fault rate*
>(see pg 398 in dino book for what happens at a page fault interrupt)

- Demand paging causes a huge performance penalty on the CPU, and is only advantageous when the page fault rate is ~ 1 page-fault in every 400,000 memory accesses.
- There are multiple techniques used to make it more efficient:
	1. **Initial Loading**: One approach to improve paging throughput is to copy an entire file image into swap space at process startup. This allows for demand paging from the swap space as needed. However, this method has the disadvantage of requiring significant time to copy the file image initially.
	2. **File System Demand Paging**: A more efficient method used by operating systems like Linux and Windows is to initially demand-page from the file system. Pages are loaded into memory only when needed, and once they are replaced, they are written to swap space. This means that only the necessary pages are read from the file system, while subsequent paging operations occur from swap space.
	3. **Handling Binary Executable Files**: For binary executable files, demand pages can be directly fetched from the file system. When page replacement is necessary, these frames can be overwritten since they are not modified. If needed again, they can be re-read from the file system.
	4. **Anonymous Memory**: Pages that are not associated with a file (like those used for a process's stack and heap) still require swap space. These pages are referred to as **anonymous memory** because they do not have a direct counterpart in the file system.
	5. **Mobile Operating Systems**: Mobile operating systems typically do not support traditional swapping. Instead, they demand-page directly from the file system and reclaim read-only pages when memory is constrained. Anonymous memory pages in mobile systems are only reclaimed when an application is terminated or explicitly releases memory. *Compressed Memory* is often used as an alternative to swapping, allowing for more efficient use of limited resources.


> [!note] **Free Frame List**
> A *free frame list* is a pool of free frames maintained by the OS to quickly access whenever frames are required for pages called on demand(by page faults)
> ![[Pasted image 20250102165532.png]]
> Free frame allocation follows ***zero fill on demand*** strategy where pages are assigned to a frame *only* after the entire frame has been initialized to 0 (to clear any previously present memory, for security reasons)
> - When a system starts up, all available memory is placed on free-frame list, which shrinks over time due to demand paging. 
> - When it is completely empty, replacement and repopulation strategies are used to free up frames



