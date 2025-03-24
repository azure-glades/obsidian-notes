Communication through the VPB (VLSI Peripheral bus)
- SPI, SSP interfaces are communication interfaces for peripherals, many sensors and actuators use this
- I2C, PC bus interfaces 1 and 0 with clock and data inputs. Essentially all peripherals use this interface
- UART (Universal asynchronous receive-transmit): Interface to communicate, *generally used to communicate between laptop and ARM7 chip*. Has a receive and transmit pin. 
	- No clock signals to sync comms, instead a specific identifier bit combination is used.
	- 9600 Baud rate by default
	- Real-time clock: Clock with actual date-time. Built into the micro-controller
- *Watchdog timer*: Resolves deadlocks, stack smashing, thrashing etc. Resets the system at regular intervals
- PWM (pulse width modulation): Interfacing to actuators that need analog inputs.

ARM Core has no flags
ARM has 3 stage pipelining -> fetch, decode, execute
ARM is 32-bit
LDR: Load register
**ARM does not have a stack**

Registers:
R13 - Can be used as a stack pointer
R14 - Link register
R15 - Program counter

### 12.05.2025
Write datasheets for lab and submit before starting pogams
