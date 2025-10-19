#  UART Quick Reference (LPC2148)
- **Pin config:** `PINSEL0 |= 0x00000005;`
- **Line control:** `U0LCR = 0x83;` (8N1, DLAB=1), `U0LCR = 0x03;` (DLAB=0)
- **Baud rate:** U0DLL/U0DLM values (know how to look up/calculate for exam)
- **Transmit:** Wait for `U0LSR & (1u<<5)` then write to `U0THR`
- **Receive:** Wait for `U0LSR & 0x01` then read from `U0RBR`
## Calculation
DLM:DLL  = 15000000 / 16 * (115200)  = result
Hence,  DLL =  result % 256 =  8  (lower 8 bits of result)
               DLM = result / 256         (upper 8 bits of result)
(or , use calculator, convert answer in decimal to HEX, take  lower two digits  put into DLL, next two digits to DLM) 
## Initialization
```c
PINSEL0 |= 0x00000005;
U0LCR = 0x83;
U0DLM = 0; U0DLL = 8;
U0LCR = 0x03;
```
## Transmitting a Character
```c
while((U0LSR & (1u<<5)) == 0x00);
U0THR = ch;
```
## Receiving a Character
```c
while((U0LSR & 0x01) == 0x00);
ch = U0RBR;
```
## Sending a String
```c
void uart_send_string(const char *msg) {
    while(*msg) {
        while((U0LSR & (1u<<5)) == 0x00);
        U0THR = *msg++;
    }
}
```
## Output Received Byte to GPIO
```c
IO0DIR = 0xFF << 16;
while(1) {
    while((U0LSR & 0x01) == 0x00);
    unsigned char data = U0RBR;
    IO0CLR = 0xFF << 16;
    IO0SET = data << 16;
}
```