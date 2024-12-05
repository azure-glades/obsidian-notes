Interrupts are a way for the *Device controller* to communicate with the *Device driver* via the CPU.
- Interrupts enter a CPU via the **interrupt-request line**
- All interrupts are stored in a common table; called an **interrupt vector**
- CPU reads the interrupt number and refers to the interrupt vector which determines the **interrupt-service routine**
- CPU directs the interrupt to an [[Interrupt Handler]] that performs a interrupt-service routine.
-  Interrupt-handler fixes the interrupt and restores the CPU state to before the interrupt occured, and gives control to the cpu via `return from interrupt`

- Device controller *raises* and interrupt, the CPU *catches* and *dispatches* the interrupt to the interrupt-handler which *clears* the interrupt by servicing the device

Interrupt handling mechanism depends on the computer architecture. Modern interrupt-handling carries:
- Defer interrupt handling during critical processes
- Efficient way to dispatch the input-handler for a device
- Multi-level interrupts, for the OS to respond with varying degree of uncertainity
These are provided in **Interrupt-controller hardware**
