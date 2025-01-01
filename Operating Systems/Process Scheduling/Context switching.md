- **Context Switching**: Quickly switching between different processes
	- Information/State of a process is stored in *process control block*.
	- Any time a process is pre-empted/interrupted, its state is stored and control is transferred to the other process
	- New process's PCB (Process control block) is loaded into CPU and runs
	- Once this process ends, the next process is determined by the [[Scheduler]] (it is not necessary for original process to resume running)


![[Pasted image 20241008101859.png]]
- System call: way for program to request resources from OS
