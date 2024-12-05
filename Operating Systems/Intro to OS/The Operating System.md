![[Pasted image 20241203193753.png]]
![[SYLLABUS.jpg]]
A computer system has:
- Hardware
- The OS
- Application Programs
- User

The OS provides a way a means for proper use of resources to meet the user's task requirements. It provides the right environment for other programs to run. The operating system is the one program running at all times on the computer—usually called the kernel. Along with the kernel, there are two other types of programs: system programs, which are associated with the operating system but are not necessarily part of the kernel

>**middleware**: a set of software frameworks that provide additional services to application developers.
>**system programs**: Aid in managing the system while it is running

#### 0.1.1. User View
- The goal is to maximize the work (or play) that the user is performing
- Focus is on Ease of use
- Contain features like touch-screens, voice assistants etc.
- Computers with no user-view (like embedded systems) lack a gui. OS is designed to run without user intervention
#### 0.1.2. System View
- Resource allocator: Manages cpu, i/o devices, memory, storage
- Control Program: manages the execution of user programs to prevent errors. 

---

Multiple [[types of operating systems]] evolved from simple ones, each developing new features that increased in complexity
#### 0.1.3. Multi-programming
- CPU maintains and runs multiple programs
- Several processes are kept in memory for running
- Process switching occurs when current-running process waits for an event
	- Waiting process causes idle CPU
	- Process-switching occurs and another process starts execution in CPU
		- Old process enters wait queue, and re-enters when current process terminates or waits
	- Prevents CPU idling since a process is always allocated if the CPU starts to idle
	- Process-preemption/context switching is not involved

#### 0.1.4. Multi-tasking
- CPU maintains and runs multiple processes
- Several processes are continuously switched between running-ready states
- [[Context switching]] is seen here. Multiple processes are switched via [[Interrupts]] or via I/O user operations
	- Increases *response time*
- Multi-tasking is implemented via [[Parallel Processing]]

![[Pasted image 20241020151930.png]]


---

- To enable multi-tasking and multi-programming, the OS has to choose/schedule the order of execution of tasks. This is handled by the **scheduling algorithm** run by the [[Scheduler]].
- The OS has to allocate memory, files, i/o devices, cache and threads to processes from a common index of resources called the **resource allocation table**. This is an essential task called [[Resource Management]]
- These systems provide file/storage management
- Ensure reasonable response time via **virtual memory** which can run programs larger than normal memory
---
![[Pasted image 20241020152125.png]]
The OS interacts with users, hardware and applications via events, interrupts and system calls

---
#### 0.1.5. Modes of operation
- Mode of operation is a set of permissions that a process carries. OS have atleast 2 modes/rings of operation/permissions
	- *User mode*: Where all user programs reside and the OS communicates to
	- *Kernel mode*: Where all system/OS programs reside. User programs can use kernel resources by communicating via [[System Calls]]

> [!info]-
> - The permissions of a process is controlled by the **mode bit** which assigns the mode it runs in \[0 for Kernel and 1 for User mode]

- [[System Calls]] provide the means for a user program to ask the operating system to perform tasks reserved for the operating system on the user program’s behalf
	- This prevents malware or erratic users/programs from running *privileged instructions* and causing permanent harm to the computer.
	- Any attempt to run instructions without suitable privileges are rejected
	- EX of privileged instructions
		- I/O control
		- timer management
		- interrupt management
- More than 2 modes of operations can also exist -> called protection rings/rings of operation

> [!info]+ Timer
> A timer prevents infinite loops in the CPU by interrupting the CPU processes at regular intervals
> - Prevents erratic User programs from generating infinite threads/loops and bogging down the CPU utillization time. 
> - When the timer interrupts, control is transferred to the OS which deals with the running process
> Interrupt time of the timer can be uniform or changed (which is a superuser permission)


 