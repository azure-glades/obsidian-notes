A module that gives control of CPU to the process.
- Dispatcher runs in ***kernel mode***. It is called by the short term scheduler because of an  **interrupt** or **system call**.
- Dispatcher is responsible for Context switching. It stores the process state in **process control blocks**  when preempted. These are retrieved when the process re gains access to CPU.

The dispatcher is invoked during every context switch. The CPU time spent by the dispatcher for context-switching is called ***Dispatcher latency***.
