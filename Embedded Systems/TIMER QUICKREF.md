# Quick Reference: Timer Unit in LPC2148

### Core Timer Registers

| **Register**                  | **Size** | **Function**          | **Key Bits/Values**                                                                                                                |
| ----------------------------- | -------- | --------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **TC** (Timer Counter)        | 32-bit   | Counts PCLK cycles    | `0x00000000` to `0xFFFFFFFF`                                                                                                       |
| **TCR** (Timer Control)       | 8-bit    | Timer enable/reset    | Bit 0 (E): `1`=Enable, `0`=Disable  <br>Bit 1 (R): `1`=Reset TC                                                                    |
| **MR0-MR3** (Match Registers) | 32-bit   | Compare values for TC | Set to desired match count                                                                                                         |
| **MCR** (Match Control)       | 16-bit   | Action on match       | Per MRx (3 bits each):  <br>- **I**: Interrupt (`1`=Enable)  <br>- **R**: Reset TC (`1`=Reset)  <br>- **S**: Stop timer (`1`=Stop) |

---

### Key Configurations
#### **Match Control Register (MCR) Setup**

| **Action**     | **MR0** | **MR1** | **MR2** | **MR3** |
| -------------- | ------- | ------- | ------- | ------- |
| **Interrupt**  | Bit 0   | Bit 3   | Bit 6   | Bit 9   |
| **Reset TC**   | Bit 1   | Bit 4   | Bit 7   | Bit 10  |
| **Stop Timer** | Bit 2   | Bit 5   | Bit 8   | Bit 11  |
Each Timer port gets 3 bits to set the mode. S R I -> Set, Reset, Interrupt
**Example**: `T0MCR = 0x0004` → Stop timer on MR0 match (binary: `0000 0000 0000 0100`).

#### **Timer Control Register (TCR)**
8b register
Bit 0 -> Counter enable
Bit 1 -> Counter reset (reset TC and the timer)
Bit 2:7 -> Reserved, unused

#### **Timer prescaler control (PR)**
Prescales clock cycles. Let PR = n. Then TC is incremented every (n+1) clock cycles.

---

### Programming Workflow: Generate 1KHz Square Wave

#### **1. Calculate Match Value**

- **PCLK**: 15MHz → Period = 1/15µs ≈ 0.067µs
- **Required half-period**: 0.5ms (for 1KHz wave)
- **MR0 value**: `0.5ms / 0.067µs ≈ 7462`

#### **2. Initialization Code**

```c
// Setup GPIO  
IO1DIR |= (1 << 16);    // Set P1.16 as output  

// Configure Timer0  
T0MR0 = 7462;           // Set match value  
T0MCR = 0x0004;         // Stop timer on MR0 match  
T0TCR = 0x02;           // Reset and disable timer  
```

#### **3. Delay Function**

```c
void delay() {  
    T0TCR = 0x01;           // Start timer (E=1)  
    while(T0TC != T0MR0);   // Wait for match  
    T0TCR = 0x02;           // Reset & stop timer (R=1)  
}  
```

#### **4. Main Loop (Square Wave)**

```c
while(1) {  
    IO1SET = (1 << 16);     // Set P1.16 high  
    delay();                 // High for 0.5ms  
    IO1CLR = (1 << 16);     // Set P1.16 low  
    delay();                 // Low for 0.5ms  
}  
```

---

### Critical Formulas

1. **Match Value Calculation**:
$$
\text{MRx} = \frac{\text{Desired Delay (s)}}{\text{PCLK Period (s)}}
$$
```
- Example (0.5ms @ 15MHz):
```
$$
\text{MR0} = \frac{0.5 \times 10^{-3}}{1 / (15 \times 10^6)} = 7500 \quad (\approx7462)
$$
2. **Timer Resolution**:
$$
																																																																	\text{Min Delay} = \frac{1}{\text{PCLK Frequency}}
$$
---

### Summary: Timer Workflow

1. **Configure**:
    - Set MRx with target count
    - Define match actions in MCR
2. **Start Timer**: `T0TCR = 0x01`
3. **Wait for Match**: Poll `T0TC == T0MRx`
4. **Reset/Stop**: `T0TCR = 0x02`
5. **Repeat** for periodic signals.

> **Note**: For precise timing, account for instruction cycles in delay loops. Use interrupts for background timing.