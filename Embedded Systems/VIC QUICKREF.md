### Interrupt Classification

|**Type**|**Priority**|**Handling Mechanism**|**Key Registers**|
|---|---|---|---|
|**FIQ**|Highest|Single handler checks `VICFIQStatus` for source|`VICIntEnable`, `VICIntSelect`|
|**Vectored IRQ**|Medium|16 prioritized slots (0=highest, 15=lowest)|`VICVectCntl0-15`, `VICVectAddr0-15`|
|**Non-Vectored IRQ**|Lowest|Common handler for all sources|`VICDefVectAddr`|

---

### Critical VIC Registers

#### 1. **`VICIntEnable` (Interrupt Enable)**
- **Function**: Enable/disable specific interrupt sources
- **Bit Mapping**: 32 bits (Bit 0 = Interrupt 0, Bit 4 = Timer0, etc.)
- **Example**:

```c
VICIntEnable = 0x10;  // Enable Timer0 interrupt (Bit 4)  
```
![[Pasted image 20250622123239.png]]
#### 2. **`VICIntSelect` (Interrupt Type Select)**
- **Function**: Classify interrupts as FIQ (`1`) or IRQ (`0`)
- **Default**: All bits `0` (IRQ)
- **Example**:

```c
VICIntSelect = 0x00;  // Set Timer0 as IRQ (default)  
```

#### 3. **`VICVectCntl0-15` (Slot Configuration)**
- **Structure**:
```
[D5]    [D4:D0]  
Enable | Source ID  
```
- **Example** (Map Timer0 to Slot 4):
```c
VICVectCntl4 = 0x24;  // 0x24 = 0b100100 (Enable=1, Source=0x04=Timer0)  
```

#### 4. **`VICVectAddr0-15` (ISR Address Storage)**
- **Function**: Holds ISR address for its slot
- **Example**:
```c
VICVectAddr4 = (unsigned long)Timer0_ISR;  
```

#### 5. **`VICDefVectAddr` (Non-Vectored Handler)**
- **Function**: ISR address for all non-vectored IRQs
- **Usage**:
```c
VICDefVectAddr = (unsigned long)Generic_IRQ_Handler;  
```

---

### Timer0 Example: Generate 50Hz Waveform
#### **Configuration Steps**
1. **GPIO Setup**:
```c
IO1DIR |= (1 << 16);  // Set P1.16 as output  
```
2. **Timer0 Initialization**:
```c
T0TCR = 0x00;         // Stop timer  
T0MR0 = 150000;       // 10ms @ 15MHz PCLK (20ms period = 50Hz)  
T0MCR = 0x03;         // Interrupt + Reset TC on match  
T0TCR = 0x01;         // Start timer  
```
3. **VIC Setup for Timer0**:
```c
VICVectAddr4 = (unsigned long)Timer0_ISR;  // Link ISR to Slot 4  
VICVectCntl4 = 0x24;                       // Enable Slot 4, assign Timer0  
VICIntEnable = 0x10;                       // Enable Timer0 interrupt  
```
4. **ISR Implementation**:
```c
__irq void Timer0_ISR(void) {  
    static int toggle = 0;  
    toggle ^= 1;  
    if(toggle) IO1SET = (1 << 16);  // Set P1.16  
    else       IO1CLR = (1 << 16);  // Clear P1.16  
    T0IR = 0x01;                    // Clear Timer0 interrupt  
    VICVectAddr = 0;                // End IRQ  
}  
```

---

### Key Workflow Summary
1. **Configure Timer**:
    - Set `T0MR0` for desired period
    - Enable match interrupt/reset in `T0MCR`
2. **Setup VIC**:
    - Assign interrupt to vectored slot via `VICVectCntlX`
    - Store ISR address in `VICVectAddrX`
3. **Enable Interrupts**:
    - Unmask source in `VICIntEnable`
4. **ISR Essentials**:
    - Toggle GPIO
    - Clear timer interrupt flag (`T0IR`)
    - Write `0` to `VICVectAddr`

> **Note**: Always stop timer (`T0TCR=0`) before reconfiguring. Use `__irq` keyword for ISRs.