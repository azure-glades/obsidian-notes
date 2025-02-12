Subroutines in assembly language are sequences of instructions that perform specific tasks and can be called from various points within a program. They serve to organize code, reduce redundancy, and facilitate easier maintenance and testing. By encapsulating functionality, subroutines allow programmers to write cleaner and more modular code.
- **Reusability**: Subroutines can be called multiple times throughout a program, reducing the need to duplicate code.
- **Parameter Handling**: They can accept parameters, allowing different inputs to be processed without altering the subroutine's internal logic.
- **Control Flow**: Subroutines transfer control to a specific entry point when called and return control to the calling point upon completion.
## Basic Structure of a Subroutine
1. **Call Instruction**: The main program uses a call instruction (e.g., `CALL`) to invoke the subroutine.
2. **Execution**: The subroutine performs its designated task.
3. **Return Instruction**: Upon completion, it uses a return instruction (e.g., `RET`) to send control back to the point where it was called.
Here’s a simple pseudocode example illustrating a subroutine that adds two numbers:
```assembly
; Main Program
START:
    MOV AX, 5          ; Load first number into AX
    MOV BX, 10         ; Load second number into BX
    CALL ADD_NUMBERS    ; Call the subroutine
    ; Continue with other operations
    ...

; Subroutine Definition
ADD_NUMBERS:
    ADD AX, BX         ; Add the two numbers
    RET                 ; Return to the caller
```
- **Main Program**: 
  - Loads two numbers into registers `AX` and `BX`.
  - Calls the `ADD_NUMBERS` subroutine.
- **Subroutine (ADD_NUMBERS)**:
  - Performs addition of the values in `AX` and `BX`.
  - Returns control back to the main program using `RET`
## Parameter Passing
The exchange of information between a calling program and a subroutine is referred to as parameter passing. Here are three common methods:
1. **Using Registers**
   - **Efficient and straightforward**: Parameters are passed directly using CPU registers.
   - **Example**:
     ```assembly
     MOV AX, 5        ; First parameter in AX
     MOV BX, 10       ; Second parameter in BX
     CALL ADD_NUMBERS ; Call the subroutine
     
     ADD_NUMBERS:
         ADD AX, BX   ; Add the two numbers
         RET          ; Return to the caller
     ```

2. **Using Memory Locations**
   - **Useful for global/static data**: Parameters are stored in predefined memory locations.
   - **Example**:
     ```assembly
     MOV [param1], 5  ; Store first parameter in memory
     MOV [param2], 10 ; Store second parameter in memory
     CALL ADD_NUMBERS ; Call the subroutine
     
     ADD_NUMBERS:
         MOV AX, [param1] ; Load first parameter
         MOV BX, [param2] ; Load second parameter
         ADD AX, BX       ; Add the two numbers
         RET              ; Return to the caller
     ```

3. **Using the Processor Stack**
   - **Flexible and can handle many parameters**: Parameters are pushed onto the stack and popped off within the subroutine.
   - **Example**:
     ```assembly
     ; Main Program
     START:
         PUSH 5            ; Push first parameter onto stack
         PUSH 10           ; Push second parameter onto stack
         CALL ADD_NUMBERS  ; Call the subroutine
         ...
     
     ; Subroutine Definition
     ADD_NUMBERS:
         POP BX            ; Retrieve second parameter into BX
         POP AX            ; Retrieve first parameter into AX
         ADD AX, BX        ; Add the two numbers
         RET               ; Return to the caller
     ```


## Implementing a Stack in assembly
The stack is implemented by storing elements in a LIFO manner between two mem locations.

1. **Push:**
```
push:
	CMP #0x400, SP   ; check if stack pointer has reached the upper limit
	BLE OverFlowError
	SUB SP,#4   ; decrement stack pointer by 4 bytes, to next mem loc
	MOV [SP],R0   ; move number in R0 to stack
RET
```
If autodecrement is supported, that can be used instead of `SUB SP,#4`
```
push:
	CMP #0x400, SP 
	BLE OverFlowError   ; another section of code that handles exception
	MOV -[SP],R0   ; move number in R0 to stack after pre-decrementing
RET
```

1. **Pop**
```
pop:
	CMP #0x800, SP   ; check if stack pointer has reached bottom limit
	BLE UnderFlowError
	MOV [SP],R1
	ADD SP,#4   ; increment stack pointer by 4 bytes
RET
```
If autoincrement is supported, that can be used instead of `ADD SP,#4`
```
push:
	CMP #0x400, SP  
	BLE OverFlowError  ; another section of code that handles exception
	MOV [SP]+,R1   ; move data to R1 then post-increment
RET
```


## Implementing Queue in Assembly

```
enqueue:
	
```


```

PUSH OPERATION..
Compare
#1500, SP
Branch <= 0
FULL ERROR
Subtract
#4, SP
Move
NEWITEM, (SP)
; OR, autodecrement is supported
Move
NEWITEM, -(SP)
POP OPERATION...
#2000, SP
EMPTY_ERROR
Compare
Branh>0
Move
Add
#4, SP
(SP), ITEM
;OR, if autoincrement is supported
Move (SP)+, ITEM
```