***Program in execution is a process***

>**[[Context switching]]**: Quickly switching between different processe
>Information of a process is stored in *process control block*. This enables context switching

> Processes are either *I/O-bound or CPU-bound* depending on what it spends more time performing
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
	- Actively updated in run-time. Tracks the progress of a process.
	- ![[Pasted image 20241008102034.png]]

## Process States
- The way a process changes in its lifetime
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
	- **Terminated/Dead:** The process has finished execution. Termination/Killing is where resources are forcefully pre-empted from the process and is removed from CPU and Job queue
	 - **New:** The process is being created.
	 - ![[Pasted image 20241008101209.png]]

- **Queuing Diagram:**
![[Pasted image 20241004110418.png]]
## Parent and Child processes
- **Child Process**: A replica of the parent process. Child processes are made by `fork()`
	- Child processes share memory and resources of the parent process.
	- The code/instructions will be the same for parent and child, until new instructions are assigned to the child by the parent.
	- Parent processes are in *waiting state* until all child processes die/terminate.
		- Parent processes can kill all child processes in-order to terminate.
			- *Cascading termination:* Killing children individually
			- *Default termination:* All children are killed together
	- Child cannot ask for more resources (they are killed if more resources are requested)

>(8mk) Explain Process, Process control block, and Process state, Queuing diagram.

