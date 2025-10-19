## Quick Reference: PWM on LPC2148 for DC Motor Control
### Pulse Period & Pulse Width
- **Pulse Period (T)**: Total duration of one PWM cycle (`Ton + Toff`), defined by **MR0**.
- **Pulse Width (`Ton`)**: Active-high duration within the period, defined by **MR1–MR6** for channels PWM1–PWM6.
- **Timer counts**: Both period and width can be any integer value of PCLK cycles.

### Match Registers (MRx)

|Register|Function|
|---|---|
|**MR0**|Sets PWM period (`T`). All channels share this period.|
|**MR1–MR6**|Sets pulse width (`Ton`) for channels PWM1–PWM6 respectively.|

### PWM Registers
- **`PWMTCR` (Timer Control Register)**:
	- 8b reg
    - Bit 0: Timer enable (1 = start).
    - Bit 3: PWM enable (1 = enable).
- **`PWMPCR` (PWM Control Register)**: 
	- 16b reg
    - Bits 9–14: Enable PWM channels (e.g., bit 14 enables PWM6).
    - Configures edge mode (single/double).
- **`PWMLER` (Latch Enable Register)**:
	- 8b reg
    - Bits 0–6: Latch updates for MR0–MR6 (1 = update on next match).
### PWM Control Register (PWMPCR)

| Bit Range | Name      | Function                                       | Values                               |
| --------- | --------- | ---------------------------------------------- | ------------------------------------ |
| **14**    | PWMM6     | PWM Channel 6 Enable                           | `0` = Disabled, `1` = Enabled        |
| **13**    | PWM5E     | PWM Channel 5 Enable                           | `0` = Disabled, `1` = Enabled        |
| **12**    | PWM4E     | PWM Channel 4 Enable                           | `0` = Disabled, `1` = Enabled        |
| **11**    | PWM3E     | PWM Channel 3 Enable                           | `0` = Disabled, `1` = Enabled        |
| **10**    | PWM2E     | PWM Channel 2 Enable                           | `0` = Disabled, `1` = Enabled        |
| **9**     | PWM1E     | PWM Channel 1 Enable                           | `0` = Disabled, `1` = Enabled        |
| **6-8**   | -         | Reserved                                       | Always write as `0`                  |
| **0-5**   | PWMx_EDGE | Edge Control for PWM1-PWM6 (1 bit per channel) | `0` = Single-edge, `1` = Double-edge |

**Key Functions**:
1. **Channel Enable**: Set bits 9-14 to `1` to enable PWM1-PWM6 respectively
2. **Edge Control**: Configure PWM mode:
    - **Single-edge**: Pulse starts at period beginning
    - **Double-edge**: Pulse centered in period

---

### PWM Latch Enable Register (PWMLER)

| Bit   | Match Register | Function                                   | Trigger Condition                            |
| ----- | -------------- | ------------------------------------------ | -------------------------------------------- |
| **7** | -              | Reserved                                   | Always write as `0`                          |
| **6** | **MR6**        | Latch update for PWM6 pulse width          | `1` = Updates PWMMR6 on next PWM match event |
| **5** | **MR5**        | Latch update for PWM5 pulse width          | `1` = Updates PWMMR5 on next PWM match event |
| **4** | **MR4**        | Latch update for PWM4 pulse width          | `1` = Updates PWMMR4 on next PWM match event |
| **3** | **MR3**        | Latch update for PWM3 pulse width          | `1` = Updates PWMMR3 on next PWM match event |
| **2** | **MR2**        | Latch update for PWM2 pulse width          | `1` = Updates PWMMR2 on next PWM match event |
| **1** | **MR1**        | Latch update for PWM1 pulse width          | `1` = Updates PWMMR1 on next PWM match event |
| **0** | **MR0**        | Latch update for PWM period (all channels) | `1` = Updates PWMMR0 on next PWM match event |
## PWM Timer Control Register

| Bit | Function                 |
| --- | ------------------------ |
| 0   | Enable counter           |
| 1   | Reset counter            |
| 2   | Reserved                 |
| 3   | PWM enable -> starts PWM |


**Key Functions**:
1. **Update Control**: Write `1` to corresponding bit to queue MRx update
2. **Synchronization**: Updates occur at next PWM match event (prevents glitches)
3. **Typical Usage**:

```c
PWMMR0 = 1000;       // Set new period
PWMMR6 = 300;        // Set new pulse width for PWM6
PWMLER = 0x41;       // 0100 0001: Latch MR0 (bit0) and MR6 (bit6)
```

---

### Critical Notes for Implementation
1. **Register Write Sequence**:
    - Always write to **Match Registers (MRx)** BEFORE enabling latch in `PWMLER`
    - Changes take effect only after match event when latch bit = `1`
2. **Single vs. Double Edge**:

```c
// Single-edge PWM (standard):
PWMPCR &= ~(1 << 12);  // Clear bit for PWM4 edge control

// Double-edge PWM (center-aligned):
PWMPCR |= (1 << 12);   // Set bit for PWM4 edge control
```

3. **Safety Protocol**:

```c
PWMTCR = 0x00;        // Disable PWM before reconfiguration
// ... Update MRx/PWMPCR ...
PWMLER = 0x7F;        // Latch all MR updates
PWMTCR = 0x09;        // Re-enable PWM
```
### Embedded C Program: DC Motor Speed Control
```c
#include <lpc214x.h>  

void runDCMotor(int direction, int dutycycle) {  
    if (direction == 1) IO0SET = 1 << 28;  // Anticlockwise  
    else IO0CLR = 1 << 28;                 // Clockwise  

    PWMMR0 = 1000;                         // Period (e.g., 1000 cycles)  
    PWMMR6 = (1000U * dutycycle) / 100;    // Pulse width (duty cycle %)  
    PWMPCR = (1 << 14);                    // Enable PWM6  
    PWMTCR = 0x09;                         // Enable PWM and timer (bits 3 & 0)  
    PWMLER = 0x70;                         // Latch MR0 (bit0) and MR6 (bit6)  
}  

int main() {  
    IO0DIR |= 1U << 28;          // P0.28 as direction control  
    PINSEL0 |= 2 << 18;           // Configure P0.9 as PWM6  
    runDCMotor(1, 10);            // Run at 10% duty (clockwise)  
    while(1);  
}  
```

### Key Notes
1. **Duty Cycle Calculation**: `PWMMR6 = (PWMMR0 * dutycycle) / 100`.
2. **ADC Integration**: To control duty via potentiometer:
```c
dig_val = adc(1, 2) / 10;       // Read ADC channel 2 (adjust scaling)  
runDCMotor(1, dig_val);          // Update duty cycle  
```

3. **Initialization**:
    - Set direction pin (e.g., P0.28).
    - Configure PWM pin (e.g., P0.9 as PWM6 via `PINSEL0`).
	
### Summary
- **Pulse Period**: Defined by **MR0**, shared across all PWM channels.
- **Pulse Width**: Set per channel using **MR1–MR6**.
- **Registers**: Use `PWMTCR` to start, `PWMPCR` to enable channels, and `PWMLER` to apply MR updates.
- **Code Flow**: Initialize pins → set MR0 (period) and MRx (width) → enable PWM → latch updates.