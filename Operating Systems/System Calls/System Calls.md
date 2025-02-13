![[Pasted image 20250201203416.png]]
- System calls are an interface to services made available by the OS for access by User programs
- System calls are called via functions present in the **application programming  interfaces (API)** that are accessed by user programs with suitable perms
- System calls and services hence provide an environment for application development. These services are collectively called [[System Services]]
EX: File copy, file read, read input from i/o device, write message to console, read input buffer, terminate process

>***System calls are treated as Software interrupts***
> - They are generally handled via `traps/exception interrupts` but some implementations have a dedicated `syscall` instruction handler
> See further: -> [[Interrupts]]

![[Pasted image 20241020153913.png]]
## Application Programming Interface (API)
Set of functions, with parameters and return values that a programmer can use to access computer resources from the OS through system calls.
There are 3 main OS APIs
- *POSIX API* (for UNIX, Linux and macOS called **glibc**)
- *Windows API*
- *Java API* for the Java Virtual Machine (JVM)

> [!info]+ Runtime Environment (RTE)
> The current environment in which an application runs. RTE contains various packages that run simultaneously with the application to satisfy dependencies, like compilers, libraries, loaders, PATH variables, system variables et.c
>  - The RTE provides **system call interfaces**. This intercepts API function calls and translates them to system calls.
>  - API hides the internal working, and RTE manages the internal working
## Types of system calls
6 major categories:
- process control
- file management
- device management
- information management
- communication
- protection

- Process control
	◦ create process, terminate process
	◦ load, execute
	◦ get process attributes, set process attributes
	◦ wait event, signal event
	◦ allocate and free memory
- File management
	◦ create file, delete file
	◦ open, close
	◦ read, write, reposition
	◦ get file attributes, set file attributes
 - Device management
	◦ request device, release device
	◦ read, write, reposition
	◦ get device attributes, set device attributes
	◦ logically attach or detach devices
- Information maintenance
	◦ get time or date, set time or date
	◦ get system data, set system data
	◦ get process, file, or device attributes
	◦ set process, file, or device attributes
- Communications
	◦ create, delete communication connection
	◦ send, receive messages
	◦ transfer status information
	◦ attach or detach remote devices
- Protection
	◦ get file permissions
	◦ set file permissions

![[Pasted image 20250201203433.png]]
