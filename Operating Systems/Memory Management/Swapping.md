**Definition:**
	 Moving a process from main memory to secondary storage and vice versa to allow the system to free up memory for other processes is called swapping
- **Swap in:** moving an active process into memory from the swap space
- **Swap out:** moving an idle process out of memory into the swap space
*Swap space*: A secondary storage devices (also called *Backing store*) that stores swapped out processes. The swap space is a secondary storage device with a relatively higher read-write speeds. Usually exists as a separate hidden partition on the hard drive (called a *swap partition*)
-> [[Thrashing]]
### 1. Standard Swapping
A type of swapping where entire processes are moved between main memory and the swap space
- All data and structures associated with a process are frozen and moved to the swap space
- In multi-threaded processes, per-thread data and metadata are swapped to maintain structure and enable the process to immediately restart when it is reloaded into memory without loosing its data
- **Advantage:** It allows physical memory to be *oversubscribed*, i.e it allows us to exceed the max number of processes that can be accommodated by physical memory since it allows *virtualization*.
	- Any pages allocated to swapped out processes are reallocated to new active processes
- **Disadvantage:** It generates a large overhead since process take a lot of space and swapping out all its data while maintaining its integrity is time consuming.

### 2. Swapping Pages
Most commonly used swapping technique, where pages of a process are swapped out. Pages that are rarely accessed/inactive are swapped out of memory and are swapped in when requested by the process.
- **Advantage**: Allows *oversubscription* without the overhead of swapping entire processes
The act of swapping in and swapping out pages of memory are called *page in* and *page out*
![[Pasted image 20241231164330.png]]

### 3. Swapping on Mobile systems
Mobile OS's do not support swapping in any form.
- Mobiles use flash memory and usually do not have sufficient space for a swap partition. 
- Flash memory is less stable secondary storage than hard disks, and cannot reliably support the large number of read-writes that are performed on swap spaces
Usually iOS and Android *request* an application to voluntarily give up allocated memory when thresholds are crossed. 
- Unmodified/read-only data is deemed unnecessary and removed from main memory, but stack data and other modified variables are kept
- Android stores the *application state* in flash memory before terminating a process to enable quick restarting