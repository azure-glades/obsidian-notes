
## Memory locations and addresses
- All instructions are stored in memory.
- Memory is organized such that groups of 'n' bits can be stored/retrived in a single operation, the gorup of n bits is called a *word* of information. Ex: 16 bit, 32 bit, 64 bit, 128 bit
- **Byte addressable Memory:** Byte addressability refers to a memory architecture where each individual byte (8 bits) is assigned a unique address, allowing for independent access to these bytes. This contrasts with **word-addressable memory**, where the smallest addressable unit is typically a word, which may consist of multiple bytes.
![[Pasted image 20250104112431.png]]

**Big Endian:** MSB is at the lowest byte address. Ex: `0x12345678`, here MSB = `0x12`, LSB = `0x78` . Used in Networking protocols, PowerPC chips, motorola chips
![[Pasted image 20250104113150.png]]
**Little Endian:** MSB is at the highest byte address. Ex: `0x12345678`, here MSB = `0x12` and LSB = `0x78`. Used in intel x86. ARM supports both big and little endian
![[Pasted image 20250104113206.png]]
*words are said to be aligned in memory if they begin at a word, i.e their starting address is divisible by word size (like 16, 32...)*

## Memory operations
2 basic operations in RAM: Write and Read
In machine language, it is Store and Load
- Load brings from memory to register
- Store moves from register to memory and over writes prev info

All computers have instructions for:
- Data transfer
- Arithmetic and Logic (Data Manipulation/Processing)
- Program sequencing (Data control)
- I/O (Data input-output)

### 1. Register transfer notation
- `LOC`: Location/address
- `[LOC]`: Contents of memory at address LOC
Ex: `R0 <- [LOC]` and `R0 <- [R1] + [R2]`

### 2. Assembly Language notation
Types of instruction: 0, 1, 2, 3 address instruction -> no. of addresses as input
- 0 address instruction: Store in push-down stack `PUSH` and `POP`
- 1 address instruction: Syntax: `OPERATION destination`. Ex:
	- `ADD r0` (adds r0 to accumulator and stores in accumulator)
	- `LOAD r0` (loads r0 to accumulator)
- 2 address instruction: Syntax `OPERATION source,destination`. Ex:
	- `ADD A,B` is B <- \[A] + \[B]
- 3 address instruction: Syntax: `OPERATION source1, source2, destination`
	- `ADD A,B,C` is C <- \[A] + \[B]

>[!note]+ Condition Codes
> Results of various operations are tracked by conditional branch instructions. Done by recoding info into bits, called *condition code flags* like
> - `N` set to 1 is negative, else 0
> - `Z` set to 1 if result is 0, else 0
> - `V` set to 1 if overflow occurs, else 0
> - `C` set to 1 is carry out occurs, else 0

## Addressing Modes
Different ways in which location of an operand is specifies in an instruction is called an addressing mode
Addressing modes are essential in computer architecture, as they define how the operand's address is determined during instruction execution. Below is an explanation of various addressing modes, including immediate mode, register mode, direct mode, indirect mode, indexed addressing, base with index, base with index and offset, relative addressing, auto-increment, and auto-decrement.

## Addressing Modes Explained
### 1. Immediate Addressing Mode
In **immediate addressing mode**, the operand is specified directly within the instruction itself. This means that the instruction contains the actual data to be used in the operation rather than an address pointing to the data.
- **Example**: `ADD R2, #100` adds the immediate value 100 to the contents of register R2.
- **Advantages**: Fast execution since no memory access is needed.
- **Disadvantages**: Limited size for the operand due to instruction size constraints[1][2].
### 2. Register Addressing Mode
In **register addressing mode**, the operand is located in a specific CPU register. The instruction specifies which register contains the operand.
- **Example**: `ADD R1, R2` adds the contents of register R2 to register R1.
- **Advantages**: Fast access since registers are quicker than memory.
- **Disadvantages**: Limited number of registers available.
### 3. Direct Addressing Mode
In **direct addressing mode**, the instruction contains the effective address of the operand. The processor retrieves data directly from this specified memory address.
- **Example**: `LOAD A, 5000` loads data from memory address 5000 into register A.
- **Advantages**: Simple and straightforward access to operands.
- **Disadvantages**: Limited flexibility and potential for a restricted address space[2][3].
### 4. Indirect Addressing Mode
In **indirect addressing mode**, the instruction specifies a memory location or a register that contains the effective address of the operand. This requires an additional memory access to fetch the operand.
- **Example**: If register R1 contains address 5000, then `LOAD A, (R1)` loads data from memory address 5000 into register A.
- **Advantages**: More flexible than direct addressing as it can point to different operands dynamically.
- **Disadvantages**: Slower due to multiple memory accesses required[2][3].
### 5. Indexed Addressing Mode
In **indexed addressing mode**, an index value stored in a special register (index register) is added to a base address specified in the instruction to obtain the effective address.
- **Example**: `LOAD A, 100(R1)` where R1 contains a base address; this loads data from address $100 + \text{content of } R1$.
- **Advantages**: Useful for accessing elements in arrays or tables.
- **Disadvantages**: Requires additional processing to calculate the effective address.
### 6. Base with Index Addressing Mode
This mode combines a base address stored in a base register with an index value from an index register to calculate the effective address.
- **Example**: `LOAD A, (R1 + R2)` where R1 is a base pointer and R2 is an index.
- **Advantages**: Provides flexibility for accessing complex data structures.
- **Disadvantages**: Slightly more complex than simple indexed addressing.
### 7. Base with Index and Offset Addressing Mode
This variation adds a fixed offset value to both a base address and an index value to determine the effective address.
- **Example**: `LOAD A, (R1 + R2 + 10)` where 10 is an offset added to the sum of R1 and R2.
- **Advantages**: Allows for precise control over memory access patterns.
- **Disadvantages**: Increased complexity in calculating addresses.
### 8. Relative Addressing Mode
In **relative addressing mode**, the effective address is determined by adding a constant value (displacement) to the current program counter (PC).
- **Example**: In branch instructions like `BEQ LABEL`, where LABEL s defined relative to the current PC.
- **Advantages**: Useful for implementing control flow structures like loops and conditionals.
- **Disadvantages**: Limited by the size of displacement that can be specified.
### 9. Auto-Increment Addressing Mode
In this mode, after accessing an operand at a specified address, that address is automatically incremented for subsequent operations.
- **Example**: `LOAD A, (R1)+` would load data from R1 into A and then increment R1 by one.
- **Advantages**: Simplifies operations on arrays or sequential data structures.
- **Disadvantages**: Can lead to unintentional overwrites if not managed carefully.
### 10. Auto-Decrement Addressing Mode
Similar to auto-increment but decrements the address before accessing it.
- **Example**: `LOAD A, -(R1)` would decrement R1 first and then load data from that new address into A.
- **Advantages**: Useful for stack operations where data is pushed or popped.
- **Disadvantages**: Complexity in managing stack pointers or similar structures.

## Assembly Language
Translated to machine code by an *assembler*

### 1. Assembler Directives
Special instructions that guide the assembler in processing asm code
- Directives are not translated into machine code, they control various aspects of assembling, like mem allocation, data definition, program structure etc
#### 1.1. EQU (Equate)
- Similar to `#define` , creates macros. Ex: `MAX_SIZE EQU 128`
#### 1.2. ORG (Origin)
- The ORIGIN directive specifies the starting address for the following data or code. It tells the assembler where to place the subsequent instructions or data in memory.
	- Ex: `ORG 0xF40`

#### 1.3. RESERVE
- Allocate space for variables without initializing them (in bytes)
	- Ex: `SS: RESERVE 0x4` . Reserves 4 bytes of space for the variable SS

#### 1.4. DW (Dataword)
- Initializes a variable of size = word, and stores the value in it
	- Ex: `N: DATAWORD 0x56`. Stores 56 in N

#### 1.5. END
- End of assembly program
	- Ex: `END`

> Adding a bunch of numbers using a loop
```ARM ASM
_start:
    LDR r1, =N         // Load address of N
    LDR r1, [r1]       // Load value of N into r1
    LDR r2, =NUM1      // Load address of NUM1
    MOV r0, #0         // Clear r0

	LOOP:
	    LDR r3, [r2], #4   // Load word from address in r2
			               //increment r2 by 4
	    ADD r0, r0, r3     // Add the value to r0
	    SUBS r1, r1, #1    // Decrement r1 and set flags
    BGT LOOP           // Branch to LOOP if r1 > 0

    LDR r3, =SUM       // Load address of SUM
    STR r0, [r3]       // Store the result in SUM

    // Exit the program (ARM Linux syscall)
    MOV r7, #1         // syscall number for exit
    SVR #0

```

> Compute test scores in memory
```ARM
_start:
    LDR r4, =N         // Load address of N
    LDR r4, [r4]       // Load value of N into r4 (number of students)
    LDR r0, =LIST      // Load address of LIST into r0 (start of the list)

    MOV r1, #0         // Clear r1 (sum for test 1)
    MOV r2, #0         // Clear r2 (sum for test 2)
    MOV r3, #0         // Clear r3 (sum for test 3)

loop:
    LDR r5, [r0, #4]   // Load score 1 (4 bytes offset from student ID)
    LDR r6, [r0, #8]   // Load score 2 (8 bytes offset from student ID)
    LDR r7, [r0, #12]  // Load score 3 (12 bytes offset from student ID)

    ADD r1, r1, r5     // Add score 1 to r1
    ADD r2, r2, r6     // Add score 2 to r2
    ADD r3, r3, r7     // Add score 3 to r3

    ADD r0, r0, #16    // Move to the next student's record (16 bytes)
    SUBS r4, r4, #1    // Decrement r4 (number of students)
    BGT loop           // Branch to LOOP if r4 > 0

    LDR r5, =SUM1      // Load address of SUM1
    STR r1, [r5]       // Store the sum of test 1 scores in SUM1
    LDR r5, =SUM2      // Load address of SUM2
    STR r2, [r5]       // Store the sum of test 2 scores in SUM2
    LDR r5, =SUM3      // Load address of SUM3
    STR r3, [r5]       // Store the sum of test 3 scores in SUM3

    // Exit the program (ARM Linux syscall)
    MOV r7, #1         // syscall number for exit
    SVC #0
```


