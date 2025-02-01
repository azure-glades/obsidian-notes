**ROM** is a type of **non-volatile memory**, which means it retains its stored data even when the power is turned off. This non-volatility makes ROM suitable for storing essential instructions and data that need to be available at startup, such as the initial instructions to load the operating system.

## Types of ROM
- **ROM**: Data is written into the ROM during the manufacturing process and cannot be altered by the user. This is the most basic type of read-only memory.
- **PROM (Programmable ROM)**: Allows the user to load data, but this process is irreversible.
	- Once programmed, the data cannot be changed. Data storage is permanent. Often used in deployed microcontrollers and embedded systems.
- **EPROM (Erasable Programmable ROM)**: Can be erased and reprogrammed, making it more flexible than ROM or PROM.
	- Erasure is typically done by exposing the chip to ultraviolet (UV) light.
	- Useful during developement since it is easy to reprogram.
- **EEPROM (Electrically Erasable Programmable ROM)**: Similar to EPROM, but the contents can be erased and rewritten electrically, without needing UV light. This makes it more convenient to update than EPROMs since they do not need to be physically removed from the circuit.
- **Flash Memory**: Operates similarly to EEPROM but is optimized for higher density and lower cost per bit. Flash memory reads data on a cell by cell basis, but writes in blocks
	- Consumes very little power, used in mobile devices
	- More prone to degradation over large read/write volumes

- **Operation**:
    - In normal operation, **ROM is primarily used for reading data**.
    - A separate writing process is required to store information in non-volatile memory, and this is different from the reading process.
- **Practical Applications**:
    - ROM is often used to **store boot instructions** for a computer to load its OS from the disk.
    - It is also used for storing firmware in embedded systems, where non-volatility is essential.

- **ROM Cell**:
    - A ROM cell can be implemented with a transistor (T) and a connection at the bit line (P).
    - If the bit line is connected to P, a 0 is stored, if not, a 1 is stored.
![[Pasted image 20250131185709.png]]


In summary, **Read-Only Memory (ROM)** encompasses several types of non-volatile memory, each with varying levels of programmability and erasability. These types range from fixed ROMs with data written during manufacturing to electrically erasable flash memory. ROMs are widely used for storing essential boot instructions, firmware, and other data that must persist even when the power is off.
