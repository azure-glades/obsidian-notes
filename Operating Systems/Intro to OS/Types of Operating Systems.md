- **Batch processing system**: Batches of processes are sent to the cpu. 
	- Each batch has a set of jobs/tasks. 
		- Each job carries an instruction set (steps)
			- Each job step has a program
	- *Turnaround time*: the time taken to execute a batch (from uploading to output)
	- Early OS. used when cpus were single core.
	- Had high cpu utillization
- **Multiprogramming system**: CPU utillization and resource utillization. Implements *context switching*
	- Context switching is where the CPU can switch between multiple contexts/processes
- **Time sharing system**: Allowed multiple users. Ensures all users get equal cpu utillization. Goes in a round robin fashion. 
	- Aimed to improve *response time* (time from placing a sub-request to getting a response from OS)
		- *Subrequest*: Auxillary operation 
	- OS controls all resources. *Pre-emption* is where a process is forcefully terminated from resources. 
		- CPU pre-emption is when a process exits the CPU.
		- Resources pre-emption is where the resources are removed
	- Interrupts are a type of sub-requests. Interrupts can be errors or process-end flags
		- Interrupts are handled by Interrupt manager
	- Resources allocation manager controls the allocation of resources to processes
		- *Fixed allocation strategy*: Where resources are allocated *a priori*, before the processes begin
		- *Resource allocation pool:* OS allocates resources as and when needed by processes
			- Processes request for resources via **system calls** 
				- System calls are a type of **Software interrupt**
	- *Process queue*: Houses all processes that are waiting to use cpu. -> Taken as input by **Scheduler**. The scheduler chooses the process from the queue that needs to be sent to the cpu.
	- **Dispatcher**'s role is to transfer processes to and from cpu or other resources.
		- Takes the processes *chosen* by the scheduler and transfers it to the cpu.
		- The dispatcher moves a process from a ready state (where it is waiting to be executed -> which is in job queue) to a running state.
		- When the scheduler decides to switch processes, the dispatcher handles saving the state (registers, program counter, etc.) of the current process and loading the state of the new process. The dispatcher enables **context switching** 
- **Real time operating system:** OS continuously monitors for user input. Runs continuously in real time. Ex: ATM, Washing machine (embedded system)
	- *Soft real-time*: Allows for occasional deadline misses.
		- Relative deadline, even if there is a miss, next deadline is from when it finished task
		- Washing machine
	- *Hard real-time*: Does not allow for occasional deadline misses
		- Absolute Deadline, no missing time slice
		- Response time is extremely less
		- Anti-lock braking.
- **Distributed systems**: Mainly used in cloud-computing to manage clusters of computers. Uses *load distribution algorithms* to distribute even load to all computers in a cluster.

