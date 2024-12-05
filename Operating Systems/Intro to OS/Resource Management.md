## Process management
• Creating and deleting both user and system processes
• Scheduling processes and threads on the CPUs
• Suspending and resuming processes
• Providing mechanisms for process synchronization
• Providing mechanisms for process communication

## Memory Management
Memory implies RAM
• Keeping track of which parts of memory are currently being used and
which process is using them
• Allocating and deallocating memory space as needed
• Deciding which processes (or parts of processes) and data to move into
and out of memory

## File-system Management
A file is a collection of related information in a suitable format
• Creating and deleting files
• Creating and deleting directories to organize files
• Supporting primitives for manipulating files and directories
• Mapping files onto mass storage
• Backing up files on stable (nonvolatile) storage media

## Mass-storage management
Permanent storage devices like flash memory, Hard disks, magnetic tape
• Mounting and unmounting drives
• Free-space management
• Storage allocation
• Disk scheduling
• Partitioning
• Protection

## [[Cache]] management
Cache is a volatile memory with extremely high access speeds. It is used to store temporary data used by a process and is moved to permanent storage once the process terminates.
- Cache memory is used to store variables and data that is accessed more frequently, which helps to reduce read-write lag that from normal memory.
- All hardware controllers have cache memory where the next few lines of programs are stored
- Cache memory is extremely small, hence cache management is crucial in multi-processing and multi-programming systems.
- In systems with multiple caches, common variables have to be updated across all the cache to ensure the most recent value is stored and accessed by processes. This is seen in multi-core systems with L1 and L2 Cache. This is **cache coherency**

## I/O System management
I/O devices have complex architectures that are run by specific device controllers called **i/o subsystems**. Device drivers are essential for communication between i/o devices and the OS
• A memory-management component that includes buffering, caching, and
spooling
• A general device-driver interface
• Drivers for specific hardware devices