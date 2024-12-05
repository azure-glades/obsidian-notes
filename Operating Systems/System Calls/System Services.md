The features provided by APIs, implemented via system calls by the Runtime Environment that allow Applications to communicate with the OS and provide an environment for running them are called ***System services/Utillities**

## User interfaces
## Application interfaces
- **File management:** APIs that allow programs to create, copy, delete, list and manipulate files and directories
- **Status Information:** Provide basic info like date-time, available memory and disk-space, cpu utillization, number of users, current users, debugging info, etc. Can be viewed in GUI also
- **File modification:** Modifying the contents of files, like configurations and dependancies.
- **Programming language support:** Compilers, Assemblers, debuggers and interpreters of various programming languages (usually accesed via PATH)
- **Program loading and execution**: System provides loaders to load programs into memory.
	- (EX: *Absolute loaders, relocatable loaders, linkage editors, and overlay loaders*)
- **Communications:** APIs for inter-process and network communication. Used to communicate with other users, computers, share files, etc.
	- Used by processes to exchange info/wait for events, or communicate with child threads
- **Background services**: Kernel processes that are always running as long as the system remains active and in-use. These provide vital functions like garbage collection, networking, scheduling processes, etc. 
	- These are called *daemon processes*, *subsystems* or *services*.