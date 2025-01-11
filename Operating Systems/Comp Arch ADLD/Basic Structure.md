- A computer has 5 functional parts:
	- Input units
	- Memory units
	- Arithmetic and Logic units
	- Output units
	- Control units
- Basic operation of computer:
	- Accepts information as programs and data through an input unit and stores it in memory
	- Information in memory is fetched and processed by an arithmetic-logic unit. The fetching of info is controlled by a program
	- Processed info leaves the computer through an output unit
	- All activities are directed by the control unit

A program is a list of instructions for a task. An instruction:
- Control the transfer of information within a computer, and with the i/o devices
- Specifies the order and type of arithmetic and logic operations to be performed
Ex:
```
LOAD r2, loc
ADD r0,r2,r3
STORE r0, loc
```

- **Instruction Register**: Holds the instruction currently being executed. It's output is available to the control unit which generates appropriate timing signal that controls the various elements involved in executing the instruction
- **Program counter:** Stores the address to the next instruction to be fetched and executed from memory.

A computer tries to maximize performance for lowest cost. Performance depends on:
- Instruction set design
- Hardware and software (like the OS)
- Technology of hardware
- Instruction loading speed
- Instruction execution speed

Performance can also be improved by implementing *paralellism*
- **Instruction Pipelining:** Multiple consecutive instructions can be overlapped and decrease the effective number of instruction executions
- **Multicore processors:** Multiple processing cores on a single chip that share registers and cache
- **Multiprocessor systems:** Multiple processing chips with their own registers and cache that can run different applications/subtasks/tasks in parallel

**Basic performance equation:** $$T = \frac{(N*S)}{R}$$
where N - Number of machine language instructions. S - Avg number of steps to execute 1 machine instruction, R - No of clock cycles per second and T - CPU time/ processing time

**SPEC Rating:** SPEC rating is a standardized computer performance rating given by System Performance Evaluation Corporation (SPEC). $$Rating = \frac{Running\ time\ on\ reference\ computer}{Running\ tim\ on\ computer\ under\ test}$$
Higher rating -> Better performance
- A *Benchmark program* is ran on both computers to evaluate performance
	- Ex: for SPEC2000, reference computer is Ultra-SPARC10 computer with UltraSPARC-III processor
- The test is done with all benchmark programs and the geometric mean is calculated $$Rating = (\prod^{n}_{i = 1} SPEC_i)^\frac{1}{n}$$
