*Definition:* 
	A **frame of memory**, also known as a **page frame**, is a fixed-length contiguous block of physical memory that corresponds to a specific size defined by the system's page size.
- Frames are used by the MMU to manage physical memory and enable virtualization
- All existing frames are accessed via a frame table
	- A pool of free frames is maintained, called  *free frame list*
- The number of frames allocated to a process significantly impacts performance. Insufficient frames can lead to increased page-fault rates, which slow down execution due to the overhead involved in handling these faults

Minimum number of frames per process is defined mainly by the computer architecture (more specifically, the instruction set)
- If pointers are involved in instructions, then atleast 3 frames of memory are needed (1 for the instruction, 1 for the pointer, 1 for the address stored in pointer). In this case the minimum frames for a process is 3 (assuming a process has 1 instruction only)
- The maximum frames for a process is defined by the OS and may even be all the frames in memory
## Allocation Algorithms
Algorithms that decide the allocation, transfer and handling of frames between pages


## Global vs Local allocation
