A memory allocation scheme where physical and logical memory is divided into *frames* and *pages* of equal sizes.
- Processes are allocated pages from the OS
- The mapping of pages to frames is done by hardware (i.e the MMU)
The MMU translates logical to physical addresses.
![[Pasted image 20241223204826.png]]

## [[Page Table Structure]]
- Stores an index of all pages present in the logical space, along with info on whether it is allocated to a process
	- Logical address: Page number + page offset
		- Page number represents the page in the *page table*
	- If the logical address space is $2^m$ and the page size is $2^n$, then:
	    - The high-order $m - n$ bits represent the *page number*.
	    - The low-order $n$ bits represent the *page offset.
	- **Frame Table:** A system-wide data structure managed by the MMU that stores all frames, and indicates whether it is free or allocated
	- Physical address: Frame number + page offset
		- Frame number is the physical block of memory allocated

- Page tack
> Page and Frame sizes are fixed and implementation dependant. Usually 4KB. Some OS's support multiple page sizes.
> `getconf PAGESIZE` : returns page size

![[Pasted image 20241223212845.png]]

> [!NOTE]+ Calculating Physical Addresses
> Physical address is calculated from Frame number, frame size and page offset
> $Physical\ Address = (Frame\ Number*Frame\ Size) + Page\ Offset$
> Ex:
> 	Size = 4KB
> 	Logical address = 0,8 (where 0 is page number) mapped to 5,0 (where 5 is frame number)
> 	Physical address = 5x4 + 8 = 28

| **Benchmark**    | **Internal Fragmentation**                             | **External Fragmentation**                                        |
| ---------------- | ------------------------------------------------------ | ----------------------------------------------------------------- |
| **Occurrence**   | Happens during memory allocation                       | Occurs over time due to repeated allocations/deallocations        |
| **Cause**        | Results from fixed-size memory block allocation        | Caused by dynamic allocation of varying-size memory blocks        |
| **Location**     | Wasted space is within an allocated memory block       | Wasted space exists in the free memory area                       |
| **Nature**       | Unused memory within an allocated block                | Free memory fragmented into scattered holes                       |
| **Avoidability** | Unavoidable in fixed-size allocations                  | Can be mitigated using defragmentation/compaction algorithms      |
| **Impact**       | Leads to inefficient memory utilization within a block | Can result in allocation failures despite sufficient total memory |
| **Visibility**   | Visible to the memory manager/allocator                | Visible to the memory manager/allocator                           |
| **Overhead**     | Minimal overhead                                       | Additional overhead for defragmentation/compaction                |
