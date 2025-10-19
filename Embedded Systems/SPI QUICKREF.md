# SPI (Serial Peripheral Interface) — LPC2148 Quick Reference
- **SPI signals and pin mapping.**
- **Control register setup:** S0SPCR (master, data bits, CPOL/CPHA).
- **Status register:** SPIF (bit 7) is key for checking transfer done.
- **Write sequence:** SSEL low, write data, wait for SPIF, SSEL high.
- **SPI clock:** S0SPCCR sets SCK.
## Pins
- P0.4: SCK0 (Serial Clock)
- P0.5: MISO0
- P0.6: MOSI0
- P0.7: SSEL (Slave Select, GPIO)

## Registers
- **S0SPCR**: Control register (master, data bits, CPOL, CPHA)
- **S0SPSR**: Status register (SPIF = transfer complete)
- **S0SPDR**: Data register (write/read data)
- **S0SPCCR**: Clock counter (sets SCK speed)

## Typical Write Sequence (Master)
1. Set SSEL LOW (IOCLR).
2. Write to S0SPDR.
3. Wait for SPIF=1 in S0SPSR.
4. Set SSEL HIGH (IOSET).

## Example Code
```c
void spi0_init(void) {
    PINSEL0 |= (1<<8)|(1<<10)|(1<<12); // P0.4(SCK0), P0.5(MISO0), P0.6(MOSI0)
    IO0DIR |= (1<<7);                  // P0.7 (SSEL) as output
    S0SPCR = 0x20;                     // Master, 8 bits, CPOL=0, CPHA=0
    S0SPCCR = 8;                       // SCK = PCLK / 8
}

void spi0_write(unsigned char data) {
    IO0CLR = (1<<7);                   // SSEL LOW (select slave)
    S0SPDR = data;                     // Write data
    while (!(S0SPSR & (1<<7)));        // Wait for SPIF=1 (transfer complete)
    IO0SET = (1<<7);                   // SSEL HIGH (deselect slave)
}
```

## Exam Pointers
- Know the function and setup of each register.
- Remember SPIF bit (S0SPSR, bit 7) for "transmission complete".
- S0SPCCR must be even and ≥8.
