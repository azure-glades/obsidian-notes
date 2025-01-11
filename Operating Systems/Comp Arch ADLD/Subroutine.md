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
In more complex scenarios, parameters can be passed to subroutines. This is often done by pushing values onto the stack before making the call. The subroutine then accesses these values from the stack.
### Example with Parameters
```assembly
; Main Program
START:
    PUSH 5            ; Push first parameter onto stack
    PUSH 10           ; Push second parameter onto stack
    CALL ADD_NUMBERS   ; Call the subroutine
    ...

; Subroutine Definition
ADD_NUMBERS:
    POP BX            ; Retrieve second parameter into BX
    POP AX            ; Retrieve first parameter into AX
    ADD AX, BX        ; Add the two numbers
    RET                ; Return to the caller
```
In this example, parameters are pushed onto the stack before calling `ADD_NUMBERS`, which then pops them off for processing.

> *See Further*
[1] http://www.sce.carleton.ca/courses/sysc-3006/s13/Lecture%20Notes/Part11-Subroutines.pdf
[2] https://fastercapital.com/topics/subroutines-in-assembly-language.html
[3] http://jklp.org/profession/books/mix/c06.html
[4] https://www.tutorialspoint.com/what-are-subroutines
[5] https://www.geeksforgeeks.org/subroutine-in-8085/
[6] https://www.youtube.com/watch?v=EloT9mZlouw
