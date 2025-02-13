-> [[Forks]]
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

## Process Creation
## Process Termination

## [[Process Waiting]]
