***Program in execution is a process***

>**Context switching**: Quickly switching between different process. Information of a process is stored in *process control block* before being switched out.

> Processes are either *I/O-bound or CPU-bound* depending on what it spends more time performing


-> Processes can create child processes or create threads : [[Operations on Processes]]
-> Processes can create and manage threads of execution : [[Threads of Execution]]
-> Processes compete for access to the CPU : [[Process Scheduling]]

## Parts of a Process
Text section, data section, heap section, stack section. See pg 106
## Process Control Block
- **Process control block** is stored in memory (RAM). It is a store of the current process state to enable context-switching
	- Stores 
		- *Process state:* Current state of the process running inside the CPU (Ready, Running, Waiting etc.)
		- *Program Counter*: Address(in memory) of the next instruction to be executed. Needed in-case the process is pre-empted (forceful remove of resource and cpu from a process)
		- *Process number/ID*: To identify a process
		- *Process Priority*: Used by the scheduler
		- *Memory Limits:* Ensures a process will not invade the memory space of other processes
		- *List of open files*: Stores the different files in memory that are currently opened and being run
		- *CPU Register storage*: Process instructions are always register oriented. Runtime changes in registers are continuously stored in memory.
		- *Heap and Stack memory*
	- Actively updated in run-time. Tracks the progress of a process.![[Pasted image 20241008102034.png]]

## Process State
***The state of a process is the current activity of that process.***
- The way a process changes in its lifetime
	 - **New:** The process is being created.
	- **Ready**: Process is waiting to be assigned to the processor
		- Process is waiting in *process queue (Ready-state queue)*, waiting for the *Scheduler* to assign it to the CPU
	- **Running:** Process is sent to the CPU and is being executed currently.
		- State of the process is stored in *Process control block*.
		- Running processes can be sent back to *ready queue* if an **Interrupt** occurs. The CPU has to be freed-up for the **interrupt service routine** to be run.
		- Running process can be sent back to ready state in a time-sharing system
	- **Waiting:** Process is waiting for an i/o device, or is waiting for an event to occur.
		- Running to waiting state when 
			- Process waits for an event to occur.
			- Process waits for an input or output
			- Can be implemented manually by including a *delay()* or *wait()* inside the process instructions.
			- Waiting for its child processes to finish execution
		- Process can go from Waiting to Running or Ready depending on the Scheduler.
	- **Terminated/Dead:** The process has finished execution. Termination/Killing is where resources are forcefully pre-empted from the process and is removed from CPU and Job queue![[Pasted image 20241008101209.png]]


