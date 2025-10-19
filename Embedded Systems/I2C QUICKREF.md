# I2C (Inter-Integrated Circuit) — LPC2148 Quick Reference

## Wires
- SCL: Clock (master)
- SDA: Data (bi-directional)

## Key Registers
- **I2C0CONSET**: Set control bits (enable, start, stop, SI, AA)
- **I2C0CONCLR**: Clear control bits
- **I2C0STAT**: Status (state codes)
- **I2C0DAT**: Data (MSB first)
- **I2C0SCLH**: SCL high period
- **I2C0SCLL**: SCL low period

## Steps (Master Write)
1. Set `I2C0SCLH`/`I2C0SCLL` for SCL frequency.
2. Enable I2C: `I2C0CONSET |= (1<<6);`
3. Send START: `I2C0CONSET |= (1<<5);`
4. Wait SI: `while(!(I2C0CONSET & (1<<3)));`
5. Check status: `I2C0STAT`
6. Write slave address + R/W to `I2C0DAT`.
7. Clear START: `I2C0CONCLR |= (1<<5);`
8. Wait SI, check status, send/receive data as needed.
9. Send STOP: `I2C0CONSET |= (1<<4);`

## Bit Meanings
- I2EN (6): Enable
- STA (5): Start
- STO (4): Stop
- SI (3): Interrupt
- AA (2): Assert ACK

## Typical Status Codes
- 0x08: START transmitted
- 0x18: SLA+W transmitted, ACK received
- 0x28: Data byte transmitted, ACK received
- 0x40: SLA+R transmitted, ACK received
- 0x50: Data byte received, ACK returned
