## Registers and Special Functions
- **r0 to r6**: General-purpose storage.
- **r7**: Used for system calls.
- **sp (Stack Pointer)**: Points to the top of the stack.
- **lr (Link Register)**: Stores the return address for functions.
- **pc (Program Counter)**: Holds the address of the next instruction to execute.
- **cpsr (Current Program Status Register)**: Stores program information (e.g., sets a flag if the result of the previous operation was negative).
## Endianness
- ARM uses **little-endian** by default but can be switched to **big-endian**.
---
## Basic Syntax and Instructions
### Example 1: Program Start and Termination
```
.global _start @ Defines the starting point
_start:        @ Starting point of the program
    MOV r0, #30
    MOV r7, #1  @ Set r7 to 1 for the terminate system call
    SWI 0       @ Software interrupt to invoke the system call
```
### Example 2: Loading Data from Memory
```
.global _start
_start:
    LDR r0, =list       @ Direct addressing
    LDR r1, [r0]        @ Load value at address r0
    LDR r2, [r0, #4]!   @ Pre-increment the value at r0 by 4 and load
    LDR r3, [r0], #4    @ Load value at r0, then post-increment by 4

.data
list:
    .word 1, 2, 3, 4, 5, 6, 7, 8
```

---
## Arithmetic Operations
- **ADD**, **SUB**, **MUL**: Perform basic arithmetic.
- **ADDS**, **SUBS**, **MULS**: Use `S` to indicate that results might be negative. Updates the CPSR register.
### Logical Operations
- **AND**: Bitwise AND.
- **ORR**: Bitwise OR.
- **EOR**: Exclusive OR.
- **MVN**: Negation (bitwise NOT).
- Flag-setting versions: **ANDS**, **ORRS**, **EORS**, **MVNS**.
### Example: Logical Operations
```
.global _start
_start:
    MOV r0, #0xAA
    MVN r0, r0
    AND r0, r0, #0xFF @ AND with 0xFF to mask trailing bits

    MOV r7, #1
    SWI 0
```

---
## Shift and Rotation
- **LSR**: Logical Shift Right.
- **LSL**: Logical Shift Left.
- **ROR**: Rotate Right.
### Example: Shift and Rotate
```
.global _start
_start:
    MOV r0, #10
    LSR r0, #1 @ Shift right by 1
    LSL r0, #1 @ Shift left by 1
    ROR r0, #1 @ Rotate right by 1

    MOV r7, #1
    SWI 0
```
---
## Branching Instructions
- **BGT**: Branch if greater than.
- **BGE**: Branch if greater than or equal to.
- **BLT**: Branch if less than.
- **BLE**: Branch if less than or equal to.
- **BEQ**: Branch if equal.
- **BNE**: Branch if not equal.
- **BAL**: Branch always.
---
## Example: Adding a List of Numbers (Loop)

```
.global _start
.equ endlist, 0xAAAAAAAA
_start:
    LDR r0, =list       @ Load address of list
    LDR r3, =endlist    @ Load end marker
    LDR r1, [r0]        @ Load first value
    ADD r2, r2, r1      @ Add to r2
	loop:
	    LDR r1, [r0, #4]!   @ Pre-increment and load
	    CMP r1, r3          @ Compare with end marker
	    BEQ exit            @ Exit if equal
	    ADD r2, r2, r1      @ Accumulate sum
	    BAL loop            @ Loop back
	exit:
    MOV r7, #1          @ Terminate program

.data
list:
    .word 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```
---
## Compound Instructions
- **CMP**: Compare two values.
- Conditional arithmetic/movement instructions:
    - **ADDLT**: Add if less than.
    - **ADDGT**: Add if greater than.
    - **ADDEQ**: Add if equal.        
    - **ADDGE**: Add if greater than or equal to.
    - **ADDLE**: Add if less than or equal to.
    - **ADDNE**: Add if not equal.
    - Similar variants exist for **MUL**, **SUB**, and **MOV**.
---
## Example: Reading from a Switch and Outputting to an LED
```
.equ SWITCH, 0xff200040 @ Address of switch register
.equ LED, 0xff200000    @ Address of LED register

.global _start
_start:
    LDR r0, =SWITCH     @ Load address of switch register
    LDR r1, [r0]        @ Read value from switch
    LDR r0, =LED        @ Load address of LED register
    STR r1, [r0]        @ Write value to LED
```