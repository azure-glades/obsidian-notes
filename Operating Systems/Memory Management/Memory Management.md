> Goals:
> What goes behind the abstraction when we allocate memory, deallocate memory, how RAM is managed
> What the hell is virtual memory?

Cache memory stores frequently used variables for quick access by CPU.

- A pair of *base* and *limit* registers define the logical address space for a process. They act as walls that separate the memory of different processes inside RAM. 
	- If processes cross this base-limit size they are auto-aborted
- Any time  a process terminates/moved out, it's current cache is cleared and stored in the PCB. This makes room for the cache of the next processes to load in. This is *cache invalidation* 
- *Relocation registers* are used as temporary registers for transferring user processes across memory. Stores the base-limit registers to know where the transferred memory is initially taken from.
> MMU: Memory Management Unit > Responsible for allocating, deallocating memory, it is a chip/hardware device present on RAM that is more of a device controller

Address binding: Merging logical address with hardware address. 
- Can be done during compile time, linker time etc.
- Source code addresses are symbolic addresses.
- Compiled object files have addresses that are bound to relocatable addresses (address that can be adjusted to point to a location)
- Linker/Loader will bind relocatable addresses to absolute (static) addresses.
- Static addresses are bound to physical addresses by the MMU

If logical to hardware linking occurs at compile-time, it is static allocation
If it occurs at run-time, it is dynamic allocation

Memory allocation strategy
1. Contiguous memory allocation
2. Non-contiguous memory allocation

Memory has: system area (where os/kernel resides) and user area (where user programs reside) 
- Memory allocated for OS/Kernel has specifically allocated space in memory
- Also has a buffer zone incase more memory is needed, called *transient area*

Multiple partition allocation
- Degree of multi-programming (controlling the number of i/o bound programs and cpu bound programs) is limited by number of partitions
- Variable partition sizes increase efficiency of memory utilisation.
- *Hole*: Block of empty memory 

Dynamic storage allocation problem: How to satisfy size request when memory has a set of free holes
1. **First fit**: Allocate the *first* hole that is big enough. Fastest strategy
2. **Best fit:** Allocate the *smallest* hole that can fit the memory. Has to search the entire list of holes
3. **Worst-fit**: Allocate the *largest* hole that can fit the memory. Searches the entire list of holes

> **Fragmentation** of memory:
> - When allocated memory is randomly distributed across the memory resulting in inefficient use of memory. Produces a lot of holes in memory
> 
> **Memory compaction** is an attempted solution to fragmentation:
> - Moving all holes to the end of memory
> - Compacting allocated memory into a continuous block of assigned memory

