## Restoring division
- **Dividend (Q):** The number to be divided.
- **Divisor (M):** The number to divide by.
- **Accumulator (A):** Used to store intermediate values, initialized to zero.
- **Quotient (Q):** The final result, initially set to the dividend.
- **n:** The number of bits in the dividend and divisor.

1. **Initialize Values**
    - Set A=0 (accumulator).
    - Set Q= dividend.
    - Count = n (the bit length of Q).
2. **Repeat n times:**
    -  **Left-Shift** the values of A and Q by one bit. (combined shift of both A and Q)
    - **Subtract**: A = A - M
    - **Check MSB of A:**
	    -  A = 0 -> Set LSB of Q = 1.
	    - A = 1 -> A = A + M -> LSB of Q = 0
1. **After n loops**
    - Q now contains the quotient.
    - A contains the remainder.
## Non-restoring division
Values are all the same
1. **Initialize Values**
    - Set A=0 (accumulator).
    - Set Q= dividend.
    - Count = n (the bit length of Q).
2. **Repeat n times:**
    -  **Left-Shift** the values of A and Q by one bit. (combined shift of both A and Q)
    - **Subtract**: A = A - M
    - **Check MSB of A:**
	    - A = 0 -> Set LSB of Q = 1.
	    - A = 1 -> LSB of Q = 0
1. **After n loops**
	- *If MSB of A = 1 -> A = A + M*
    - Q now contains the quotient.
    - A contains the remainder.