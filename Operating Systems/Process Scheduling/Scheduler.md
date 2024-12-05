## [[Scheduling algorithm]]
A **scheduling discipline** (also called **scheduling policy** or **scheduling algorithm**) is an algorithm used for distributing resources among parties which simultaneously and asynchronously request them. Scheduling disciplines are used in [routers](https://en.wikipedia.org/wiki/Router_(computing) "Router (computing)") (to handle packet traffic) as well as in [operating systems](https://en.wikipedia.org/wiki/Operating_system "Operating system") (to share [CPU time](https://en.wikipedia.org/wiki/CPU_time "CPU time") among both [threads](https://en.wikipedia.org/wiki/Thread_(computer_science) "Thread (computer science)") and [processes](https://en.wikipedia.org/wiki/Process_(computing) "Process (computing)")), disk drives ([I/O scheduling](https://en.wikipedia.org/wiki/I/O_scheduling "I/O scheduling")), printers ([print spooler](https://en.wikipedia.org/wiki/Print_spooler "Print spooler")), most embedded systems, etc.

- FIFO: First in First out
- SJF: Shortest Job First -> Preemptive and non-preemptive approaches
- PBPS: Priority based preemptive scheduling
- RRS: Round Robin Scheduling (Preemptive scheduling algo)
- **Priority based Pre-emptive scheduling**: **Priorities** are assigned to all processes based on an algorithm and processes are picked/scheduled based on priority (Seen in Multiprogramming OS)
	- Process can be interrupted/context-switched by a higher-priority process
		- **Priority** is stored in Process-control block
		- Priority is determined by OS
			- Fixed priority: Priority assigned is permanent over a period of execution. Ex: *OS Programs*
			- Variable priority level: Priority changes over the period of execution. Ex: *User programs*
- **Event based pre-emptive scheduling**: Also uses Priorities (Used in Real-time OS: which listens continously for user input)
	- Uses priority-based scheduling to ensure real-time tasks to be handled asap to improve responsiveness

---
## Types of schedulers
### _1. Long term scheduler_
Also called admission scheduler.
- Decides what processes enter ready queue. Plans the execution of processes long-term.
- Admission scheduler is responsible for controlling the distribution of I/O bound and CPU bound processes.
	- An I/O-bound process is one that spends more of its time doing I/O than it spends doing computations.
	- A CPU-bound process generates I/O requests infrequently, using more of its time doing computations
- Long term scheduler tries to produce a good mix of processes for max efficiency.
	- More i/o bound process -> ready queue is empty -> Short-term scheduler and CPU is free
	- More CPU bound process -> i/o waiting queue is empty -> Devices are unused
> EX: batch processing systems, computing clusters, supercomputers, [render farms](https://en.wikipedia.org/wiki/Render_farm)

### _2. Medium term scheduler_
Medium term scheduler handles ***[[Process Swapping]]***
- Process swapping is used to clear up the RAM and the ready queue by moving process info into storage.
	- Inactive processes, low priority processes, page-faulting processes, and memory consuming processes are often swapped into storage.

### _3. Short term scheduler_
Also called *CPU Scheduler*.
- Decides which of the processes in ready queue will be sent to the CPU for execution.
	- Processes enter CPU after clock/timer interrupt, context switching, i/o interrupt, exceptions, or system calls.
- Short term scheduler is invoked more frequently that LTS and MTS. Always invoked once per time-quantum (time slice)
- Short term scheduler may implement preemptive or non-preemptive scheduling.
	- Preemptive scheduler can forcefully preempt processes from CPU
- Short-term scheduler invokes the [[Interrupt Handler]]
- Short-term scheduler invokes the [[Dispatcher]]
## Scheduling Priorities
Gantt chart: Visually depicts execution of tasks/processes over time
- High priority for CPU and low priority for I/O bound
- When high priority is given for I/O bound, the cpu idle cycles and i/o idle cycles are less

- **IO bound program:** Mainly deals with i/o process or i/o cycles
- **CPU bound program**: Mainly deals with CPU cycles, runs in CPU

1. **CPU Idle Cycles**:
	- I/O-bound processes generally spend more time waiting for I/O operations (like disk access) to complete rather than requiring intense CPU usage.
	- By prioritizing these processes, the CPU can quickly handle any small processing tasks these processes require, allowing it to stay active without waiting.
	- With the CPU more frequently occupied with small tasks from the I/O-bound process, there are fewer idle cycles.
2. **I/O Idle Cycles:**
    - Prioritizing I/O-bound tasks reduces the wait time before I/O operations are processed.
    - The faster processing minimizes the idle time of I/O devices as they spend less time waiting in the queue.
    - Therefore, the I/O devices remain engaged more consistently, which leads to fewer idle I/O cycles.

---

>[!Terms]
>**Burst time/Execution time**: The time spent by a process in running queue (includes only CPU time, does not include time spent in ready-queue, waiting queue, etc)
> **Arrival time:** Time taken by a process to enter system
> **Waiting time:** The time that a process spends in waiting queue

## Scheduling Queues
- Queue is a data-structure. It is used for storing an order of programs. Queue contains a head and tail	​￼- *Medium term scheduler:* Maintains max utilisation of CPU.
	- **Ready Queue:** Stores process control blocks of all processes in "ready" state
		- *Only ready queue has priority values*
	- **Wait Queue**: Stores process control blocks of all processes in "waiting" state
	- **I/O Queue**: Stores processes waiting to access an I/O device. Every I/O device has its own queue.
		- I/O devices run independently of the CPU. (Device has its own controller)
		- CPU has to initiate I/O execution via *system calls*
		- I/O Devices interact with CPU via *interrupts*
	![[Pasted image 20241008105210.png]]