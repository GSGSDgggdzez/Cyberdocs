# System Security

Modern memory protections:

- DEP (Data Execution Prevention)
- ASLR (Address Space Layout Randomization) 
- Canary


## CPU Registers

### 1. Data Registers

| 32-bit Register | 64-bit Register | Name        | Description                                                                                                                                                                                        |
| -------------------- | -------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `EAX`                | `RAX`                | Accumulator | The accumulator is used for input/output and arithmetic operations. (Used in arthmetic operation)                                                                                        |
| `EBX`                | `RBX`                | Base        | The base is used in indexed addressing. (Used as a pointer to data)                                                                                                                              |
| `ECX`                | `RCX`                | Counter     | The counter is used for rotate instructions and loop counting. (Used in shift/rotate instruction and loops)                                                                       |
| `EDX`                | `RDX`                | Data        | Data is used for I/O and in arithmetic operations for multiplication and division operations involving large values. (Used in arthmetic operation and I/O) |

### 2. Pointer Registers

| 32-bit Register | 64-bit Register | Name                | Description                                                                                                                                                                                                                                                   |
| -------------------- | -------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ESP`                | `RSP`                | Stack Pointer       | The stack pointer points to the top of the stack. (Pointer to the top of the stack)                                                                                                                                                                             |
| `EBP`                | `RBP`                | Base Pointer        | The base pointer is also known as `Stack Base Pointer` or `Frame Pointer` which points to the base of the stack. (Pointer to the base of the stack (aka Stack Pointer, or Frame pointer))                                                   |
| `EIP`                | `RIP`                | Instruction Pointer | The instruction pointer stores the offset address of the next instruction to be executed. (Controls the program execution by storing a pointer to the address of the next instruction that will be executed: It tells the CPU where the next instruction is) |

### 3. Index Registers

| 32-bit Register | 64-bit Register | Name         | Description                                                                                                                                             |
| ----------------------- | ----------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ESI`                   | `RSI`                   | Source Index | The source index is used as a pointer from a source for string operations. (Used as a pointer to source in stream operation)      |
| `EDI`                   | `RDI`                   | Destination  | The destination is used as a pointer to a destination for string operations. (Used as a pointer to destination in stream operation) |


## Endianness

During load and save operations in registers and memory, bytes are read in an order called `endianness`. 

Endianness is distinguished between `little-endian` and `big-endian` formats.

Example with the following values:

- Address: `0xffff0000`
- Word: `\xAA\xBB\xCC\xDD`

| Memory Address | 0xffff0000 | 0xffff0001 | 0xffff0002 | 0xffff0003 |
| ------------------- | -------------- | -------------- | -------------- | -------------- |
| `big-endian`        | AA             | BB             | CC             | DD             |
| `little-endian`     | DD             | CC             | BB             | AA             |

This is very important so that we can enter our code in the correct order later when we need to tell the CPU which address to point to.


