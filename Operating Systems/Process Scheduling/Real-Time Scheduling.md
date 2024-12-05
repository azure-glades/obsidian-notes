## 1. Types of Real-Time Systems:
 - **Hard Real-Time**: A task must be serviced before its deadline. If it misses the deadline, it's as good as not performing the task itself. High priority is given to meeting the deadline
	 - Missing a deadline can lead to catastrophic consequences. Examples include pacemakers or anti-lock braking systems.
 - **Soft Real-Time**: Does not guarantee that a process will complete before its deadline, but it will give higher priority over processes without a deadline
	 - Missing a deadline degrades performance but isn't disastrous. Examples include video streaming or online transaction processing.

## 2. Event Latency
The time spent to service an event is called **event latency**.
- **Interrupt Latency**: The period of time from the arrival of the interrupt to the start of the interrupt service routine. ![[Pasted image 20241126184521.png]]
- **Dispatch Latency:** The time required by the dispatcher to preempt a process and start another.
	- *Conflicts* phase is 
		- Waiting for preemption
		- Waiting for low priority processes to release resources needed by the high priority one (called **priority inversion**)
	- *Dispatch* phase is dispatching the new process to the CPU![[Pasted image 20241126184555.png]]
> [!info]- Priority Inversion
> When a lower-priority task holds a resource needed by a higher-priority task, causing a delay (common in real-time scheduling).

## 3. Real-time Scheduling Algorithms:
Scheduling algorithms implemented in real-time systems to handle tasks with deadlines
> [!info]+ Periodic Processes
> Processes that require the CPU at regular intervals/processes that enter the ready queue at regular intervals
> - Processes have a processing time (t), a deadline (d) and a period cycle (p), and 0 < t < d <= p
> - The rate of a periodic task is 1/p

### 3.1. Priority-based scheduling
Only suitable for soft real-time systems since it only guarantees that it will give higher priority to tasks with a deadline but cannot reasonably ensure that they are completed within the deadline
- Often use a technique called **admission-control** where the scheduler makes one of two choices for a deadline-task
	- It admits the processes guaranteeing that the process will get service in time
	- Rejects the process if it deems it impossible to service the task within the deadline

### 3.2. Rate-monotonic scheduling
 Static preemptive priority based scheduling that is used for hard real-time systems.
 - Each periodic task is assigned a priority *inversely* based on its *period*. 
	 - Shorter period -> Higher priority
	 - Longer period -> Lower priority
- *Assumes that the burst time of processes remain constant throughout*
***Rate-monotonic scheduling is considered optimal in that if a set of processes cannot be scheduled by this algorithm, it cannot be scheduled by any other algorithm that assigns static priorities.***
- Because of how periodic processes work (*check pg 231 in dino book*) CPU utilization is bounded and cannot always be maximized. 

> [!NOTE]+ CPU Utilization
> CPU utilization is for a process $P_i$ is $$P_i = \frac{burst\ time}{period} = \frac{t_i}{p_i}$$
> Total CPU utilization is the sum of utilization for each process
> - For scheduling $N$ periodic processes; CPU utilization is bound at $N(2^{1/N} - 1)$
> When there is one process; Max CPU utilization is 100%
> When there are 2 periodic processes; Max CPU utilization is bounded at 83%
> - It approaches 69% as number of processes reach infinity
> *If the total CPU utilization of a set of processes is greater than the Maximum bound, then some of the processes will end up not meeting their deadline*

### 3.3. Earliest-Deadline First scheduling
Dynamic preemptive priority based scheduling that is used for hard real-time systems.
- Each task is assigned a dynamic priority based on how far away the deadline is
	- Earlier the deadline -> Higher priority
	- Farther the deadline -> Lower priority
- Because it is dynamic, processes that had long deadlines will get increased priority as their deadline approaches.
- *Requires every process to announce its deadline (when it enters ready queue)*
- Advantage of EDF over RMS:
	- EDF scheduling applies even when there are non-periodic processes with deadlines
	- Does not require periodic processes to have constant CPU burst times

### 3.4. Proportional Share Scheduling 
Allocates a total of T shares among applications to determine their CPU time allocation.
- Share allocation is based on the priority, deadline and period of a process that is implementation dependant (it is called as **weight**)
	- Each application receives N shares, which translates to a percentage of total processor time calculated as $\frac{N}{T}$
	- Example:
	    - Total shares (T) = 100
	    - Process A: 50 shares → 50% of CPU time
	    - Process B: 15 shares → 15% of CPU time
	    - Process C: 20 shares → 20% of CPU time

PSS implements an admission control policy once shares have been allocated to prevent processes who's deadline cannot be met from taking away CPU time from currently allocated processes
- Ensures that applications receive their allocated shares by managing the admission of new processes.
	- A new process can only be admitted if sufficient shares are available.
	- In the example, with 85 shares already allocated (50 + 15 + 20), a request from Process D for 30 shares would be denied, as it would exceed the total available shares (100).