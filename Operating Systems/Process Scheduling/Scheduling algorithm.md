Scheduling algorithm is used to decide the order of activation of tasks in ready queue.
- Execution of CPU: CPU Burst
- Execution of I/O: IO Burst

Scheduling decisions occur when:
- Switches from running to waiting
- Switches from running to ready
- Switches from waiting to ready
- Process is terminated
[[Deadlocks]]
 
## 1. Scheduling criteria
Criteria that the scheduling algorithm tries to improve/maximize by scheduling appropriate tasks
- **Throughput**: Amount of output by input. Number of tasks being run, involving context switching. 
- **CPU efficiency**: %utillization of CPU cores and uptime of CPU.
	-  OS programs are called *overhead* and is kept as low as possible (More preference is given for user programs) since CPU cannot spend its resources trying to run OS.
- **Response time**: Time elapsed between first subrequest and first response.
- **Turnaround time**: Time elapsed for a process to go from ready-state to dead-state (Lifetime of a process/time taken to complete a process) (Includes CPU time and I/O time and interrupts and time spent while it was context-switched)

## 2. Scheduling Algorithm
A set of instructions that a scheduler follows to decide the order in which tasks enter the CPU
- Burst time: time taken for each process execution is called cpu burst-time for that process
- Waiting time: the time when the process entered cpu - time it arrived to ready queue
- Turnaround time: the when the process completed execution - time it arrived to ready queue
### 2.1. First Come First Served (FCFS)
The processes are sent to the cpu based on when they arrive. The length of each process and priority is not considered.
Example:

| Process | Arrival time | Burst time |
| ------- | ------------ | ---------- |
| P1      | 0            | 24         |
| P2      | 1            | 3          |
| P3      | 2            | 3          |
Gant Chart:
![[Pasted image 20241025120009.png]]
Average waiting time: 17 ms

- **Convoy effect:** When shorter processes execute after longer processes.
	- While the longer process executes, there is a convoy of shorter processes waiting to enter the cpu and complete execution.
	- **Increases average waiting time and turnaround time**
	- Ex: if the processes arrived as P3, P2, P1
	- ![[Pasted image 20241025120153.png]]
	- Average waiting time = 3ms. This is 14 ms shorter and is significant


### 2.2. Shortest Job First (SJF)
SJF is optimal since it consistently gives the minimum average waiting time.
Example:

| Process | Arrival time | Burst time |
| ------- | ------------ | ---------- |
| P1      | 0            | 6          |
| P2      | 0            | 8          |
| P3      | 0            | 7          |
| P4      | 0            | 3          |
Gant Chart:![[Pasted image 20241025122141.png]]
Average waiting time: 7 ms

> How does scheduler know the burst time of a process?
- There is no real way to know the burst time of a process
- The burst time is predicted by looking at the previous burst times of that process (its history)
- The next burst time is predicted via *exponential averaging*
- Here:
	$t_{n}$ is nth CPU burst
	$\tau_{n+1}$ is the predicted value for the next CPU burst
	$0 \le \alpha \le 1$ where $\alpha$ is the relative weight , calculated from recent and past history 
	$$\tau_{n+1} = \alpha t_{n} + (1 - \alpha)\tau_{n}$$
- if $\alpha$ = 1, then $\tau_{n+1}$ depends only on the previous CPU burst.
- if $\alpha$ = $\frac{1}{2}$, then $\tau_{n+1}$ depends equally on previous and current burst time

SJF implemented with pre-emption is called *Shortest-remaining-time first*
***-- more stuff to be added --***

### 2.3. Round Robin Scheduling (RRS)
- Round Robin (RR) Scheduling is a preemptive CPU scheduling algorithm designed for time-sharing systems.
- Each process is assigned a fixed time in cyclic order, allowing multiple processes to share the CPU fairly.

- **Time Quantum (Time Slice):** A small unit of time (e.g., 10ms or 100ms) that is defined by the [[Scheduler]] which is allocated to each process. After this, the CPU is preempted and the next process in the queue is scheduled. 
	- The time quantum is maintained by the [[Timer]]. The timer passes an interrupt to the CPU once a time-quantum expires, which preempts the process and the next process enters.

- The process ready-queue is implemented as a *circular queue*.
- Performance of RRS is highly dependant on the size of the time-quantum that is chosen
	- Average wait-time in RRS is much longer for long process that require multiple time quanta to execute
	- If the time quantum is too **large**, RRS behaves like conventional FCFS scheduling algorithm.
	- If the time quantum is too **small**, high frequency of context switching increases CPU overhead.

> [!info]- Waiting time
> Waiting time is the time spent by the process in the wait queue (process enters wait queue when it is preempted)
> If there are n processes in the ready queue and the time quantum is q, then
each process gets 1/n of the CPU time in chunks of at most q time units. Each
process must wait no longer than (n − 1) × q time units until its next time quan-
tum


### 2.4. Priority based preemptive scheduling (PBPS)
Two types of priority assignment: *Fixed priority* and *Variable priority*

> [!info]- **Starvation**
> When priorities do not get CPU time due to their low priority level (they keep getting preempted by others)

> [!info]- **Ageing:** 
> When processes accumulate more priority. Ensures processes execute without high waiting time

- Processes are scheduled based on priority levels. Processes with equal priority are chosen based on arrival time.
	- Fixed priority is when the priority of a process remains constant
	- Variable priority is commonly used to prevent starvation of a process.
		- Generally OS/System process and critical functions occupy highest priority and user programs generally have lower priority.
- _SJF is a type of priority based CPU scheduling where the priority is the time taken for a process to execute_

### 2.5. Earliest Deadline First Scheduling
A type of PBPS where the priority is given to processes with earlier deadlines
## 3. [[Real-Time Scheduling]]
A set of scheduling algorithms used in real time operating systems. The goal here is to maximize ease of use. Prioritizes short response time and context switching to prevent the system from hanging.
- essential in systems where timing is critical, such as embedded systems in medical devices, industrial automation, and automotive control systems.
- 