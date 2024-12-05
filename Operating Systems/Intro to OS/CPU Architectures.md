 ***A description of the structure of a computer system made from component parts is called computer architecture***
 - Describes the instruction set architecture design
 - Logic design
 - Micro-architecture design
 - Implementation

The electronic design, structure and number of central processing units within a computer determines the type of instructions it can understand, the capabilities of the system and hence, the OS that can manage and maintain it. This is called CPU architecture, and there is a wide variety of them:
- Based on number of processors
- Based on the type of architecture
- Based on the degree of coupling between the processors

>Definitions:

- **CPU**: aka, the processor. Electronic chip that contains multiple cores, threads of execution, registers, memory bus, communication channels etc.
- **Core**: The component in a CPU that executes instructions and registers for storing data locally
- **Instruction set**: A set of supported instructions, data types, registers and hardware support for managing memory that can be used to control/use a processor
- **Device Drivers**: Software that is capable of understanding instructions from the computer/OS and driving microprocessors/controllers. Also sends the output from the device to the OS. Helps the OS to communicate and use the specific device
	- Drivers were originally written by kernel programmers.
	- Now they are mostly written by people who create the hardware.
- **Graceful degradation**: When systems continue providing service with remaining components even when some components fail.
- **Hot-standby mode**: Back-up systems that are always checking the health of the mainframe and always ready to step-in and take over processing jobs when the mainframe fails are said to be in hot-standby mode. They are always power-on and do not have a delay time, allowing graceful transfer of tasks
## 1. Processor Based
1. **Single Processor systems**: When the CPU has only 1 processing unit (called as a *core*) within it.  The core is capable of executing a general purpose instruction set (written in x86 or ARM assembly that is converted to machine code)
	- There are also device-specific processors, processors present within individual devices like hard disks, audio mixers, display monitors etc, which contain their own instruction set that is understood and managed by *device drivers*.
	- Weaker/smaller processors are called microcontrollers.
	- This releases a lot of the processing burden on the single-processor by off-loading tasks to these device microcontrollers.
	- Makes the devices effectively autonomous
2. **Multiprocessor systems**: Where there are multiple distinct processors within the same CPU chip. They function independently of each other but can communicate and share data across main memory. Distinct processors which have their own registers and cache and can run different execution threads. N processors can run N different programs simultaneously
![[Pasted image 20241205181637.png]]

3. **Multi-core systems**: Often considered as a type of multi-processor system. While mult-processors have multiple interlinked chips with single cores, multi-core systems have just 1 chip with multiple core. 
	-  Each core runs independently of other cores and executes different threads/processes
	- Multi-core systems have much faster communication since they exist on the same processor chip and can communicate directly
	- Can exchange memory on a common level 2 cache, instead of RAM.
	- Have less power consumption compared to multiprocessors. 
	- Are more complicated to construct than multiprocessors
![[Pasted image 20241205183110.png]]

## 2. Based on instruction set
1. **Complex instruction set computer**:
	- Implements a set of instructions that are used to execute processes and control the processor. 
	- CISC implements a complex instruction set where multiple functions may be bundled into a single instruction to make writing code a lot easier.
	- The advantage of CISC is the smaller size of programs which saves on computer memory and storage.
	- A lot easier to implement high level programming
1. **Reduced Instruction set computer**
	- Implements a simpler set of instructions that can be performed by the computer. Instructions are a lot simpler that CISC but require more clock-cycles to run. 
	- This is because each instruction is written in simple code that is executed with a smaller overhead than CISC.
		- Each RISC instruction performs only 1 function, while multiple functions may be bundled together in CISC.
	- Implements an instruction pipeline to speedup execution of each instruction (which is only possible if the instructions are simple)
	- The advantage of RISC is the vastly less power consumption.

The type of instruction set implemented determines the CPU architecture design. The two main ones are
- **x86**: Designed by intel and first implemented in 8086 micro-controllers. x86 implements CISC and is mostly used in personal computers to main-frame computers. Have a wide range of applications. Are also used on embedded systems (for smaller program sizes)
- **ARM**: Designed by Acorn RISC Machines that implements RISC. ARM chips have drastically less power consumption and are mostly used on mobile phones and embedded systems (for low power consumption). Snapdragon chips, and apple M1 chips implement ARM.

## 3. Based on degree of coupling
1. **Tightly coupled systems**: When processors are on the same board and can communicate extremely quickly
2. **Loosely coupled systems**, also called **Clustered systems**: Systems where multiple individual computers are connected and function as a singular entity. These distinct systems work together by sharing resources over a WAN  (usually ethernet). Often used in *high performance computing* since it is easily scalable and upgraded.
	- Usually used in running servers to provide continuous service to users
	- Used in supercomputers and HPC computing clusters
	- Used in *storage area networks* which allows many systems to utilize a large pool of shared storage
	Main advantage of clustered systems is their reliability in providing continuous service, even when some hardware breaks-down (called *graceful degradation*) and such systems are termed *fault tolerant*, since other processors can take over and divide workloads when an individual system (or **node**) fails.
	Clustering can be:
	1. **Asymmetric clustering**: where a collection of systems are active and running and perform tasks while the other set of backup systems (in *hot-standby mode*) continuously monitor the health of the active systems. 
	2. **Symmetric clustering**: where all systems in good health are performing tasks while also monitoring each others health. Is a better use of computing resources but requires parallelization between the system tasks to ensure synchronization. This requires the software/hardware to support [[Parallel Processing]]

## 4. Based on architecture
1. [**Von Neumann Architecture**](https://en.wikipedia.org/wiki/Von_Neumann_architecture#von_Neumann_bottleneck)
2. [**Harvard Architecture**](https://en.wikipedia.org/wiki/Harvard_architecture)

