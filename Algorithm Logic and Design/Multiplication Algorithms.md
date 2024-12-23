	- Sequential Binary Multiplication
	- Sequential Multiplier algorithm
	- Booth's algorithm
	- Bit-Pair recording algorithm

***In multiplication of two n-bit numbers , the resultant is of size 2n-bits***
## Sequential Multiplier Algorithm
- Similar to conventional multiplication.
- *Status Flag Register:* Stores information on the state of computation, like Zero , Negative, Carry, Overflow.
	- Zero: If the answer is 0
	- Negative: If the answer is negative
	- Carry: If carry or borrow has been done to the first bit (Most Significant Bit)
	- Overflow: If the result cannot be shown with the current number of bits (Result is out of range of bit-system) (Often causes the answer to be negative, which is wrong answer)
Ex:
25\*5
M = 25 = 11001
Q =    5 = 00101
A = 00000

|     | M     | C   | A      | Q'    |
| --- | ----- | --- | ------ | ----- |
|     | 11001 | 0   | 00000  | 00101 |
| #1  | -     | 0   | +11001 | 00101 |
|     |       | 0   | 01100  | 10010 |
| #2  | -     | 0   | 00110  | 01001 |
| #3  | 11001 | 0   | +11001 | 01001 |
|     | -     | 0   | 01111  | 10100 |
| #4  | -     | 0   | 00111  | 11010 |
| #5  | -     | 0   | 00011  | 11101 |
Answer: 00011 11101 = 125

## Booth's Algorithm
1. **Initialization**:
    - Start with two signed binary numbers: the multiplicand (M) and the multiplier (Q). Both are in two's complement form.
    - Maintain a register (A) initialized to zero, a copy of Q shifted left by one extra bit to act as a flag bit, and a count equal to the bit length of the numbers.
2. **Bit Analysis and Operation**:
    - Booth's algorithm checks the last two bits: the least significant bit of Q and a flag bit (Q and Q-1)
    - Based on the value of these two bits, the algorithm decides whether to:
        - **Add M to A if the bits are** `01`.
        - **Subtract M from A if the bits are** `10`.
        - **Do nothing if** the bits are `00` or `11`.
        --> Do not forget sign extension
1. **Right Shift**:
    - After each operation, the bits in the combined register (A, Q) are shifted right by one bit. (Or left shift is u are using conventional multiplication)
    - The algorithm repeats this cycle n times (for n bits)
2. **Final Result**:
    - At the end of the operations, the combined registers A and Q contain the result of the multiplication.

## Bit-Pair Recoding Algorithm
Optimization of Booth's algorithm done by skipping the restoring step until the end. 
1. **Convert the multiplier**
	- Analyse consecutive overlapping pairs of bits and based on its value, evaluate the action that has to be taken.
	- EX: 1001 -> 10010 (left shift) -> (-1 +1) is the recoded Q. 
	- ( 010 is analyzed first -> +1 ; then 100 is analyzed -> -1)
1. **Bit pair encoding values**:
	- Based on encoding table, it follows the `00 01 10 11` technique but with an emphasis on the previous bit also
	- ![[Pasted image 20241016101244.png]]
3. **Shift and Accumulate:**
	- Based on each two-bit pair, you either add, subtract, or do nothing with the multiplicand, shifting left by two bits each time instead of one.
	- The result is accumulated as you process each pair.
4. **Multiply**
	- Repeat this cycle n times for n bits.
	- The combined registers of A and M contain the answer