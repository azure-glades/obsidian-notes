[[Primitive]]
Size: 4 bytes = 32 bits
Range: (2^31) - 1 to -2^(31)  \[first bit is used for sign +/-]
* can store octal, hexadecimal and decimal values

1. short int | 2 bytes | 2^(+-15) | %hd
2. unsigned short int | 2 bytes | %hu
3. long long int | 8 bytes | 2^(+-63) | %lld
4. unsigned char, char | 1 byte | 0 to 255 or -128 to 127 | %c
5. float | 4 bytes | %f
6. double | 8 bytes | %lf

size of integer is compiler dependent, use 
```

```
ps: 1 byte = 8 bits 
