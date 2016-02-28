x328 CPU and Chipset
====================

#### Jazza_Hat & NeverCast

## Hardware Specifications

|Property|Value|Comments|
|---|---|---|
|QBYT size in bits|32||
|ISA size in bits|32||
|Endianess|Big||
|RAM Support|2^32 Bytes|current implementation is 26 bit or 64MB|
|RAM Addressing size|Bytes||
|I/O Method|Memory Mapped||
|Expansion Memory|256KB||
|Expansion Slots|16||
|Interupt Support|Yes||
|Interupt Priority|32 Levels||
|Unique Interupts|256||
|Interupt Table|256 * 5 Bytes|1.25KB|

## Internal Data type bit widths

| Data Type | Width   |
|-----------|---------|
| BYTE      | 8       |
| DBYT      | 16      |
| QBYT      | 32      |
| Immediate | Variable|
| Pointer   | 6       |

## Compiler data type bit widths

*Not nessasarilly the data itself, but the container of the Data*

| Type        | Width      |
|-------------|------------|
| Register    | 6          |
| Immediate   | Variable   |
| Label       | Variable   |
| Address     | 21         |
| Pointer     | 6          |
| PC          | MISSING    |

Immediate Type can be
* Base 10
* Base 2
* Base 16
* Fixed point
* ASCII *Up to 4 characters, will be truncated otherwise*

## Immediates examples

| Immediate Value         | Assembler output      | Register representation (QBYT)          |
|-------------------------|-----------------------|-----------------------------------------|
| 69                      | 0 0000 0000 0100 0101 | 0000 0000 0000 0000 0000 0000 0100 0101 |
| -69                     | 1 1111 1111 1011 1011 | 1111 1111 1111 1111 1111 1111 1011 1011 |
| 69.69f                  | 0 0100 0101 1011 0001 | 0000 0000 0000 0000 0100 0101 1011 0001 |
| 0b0 0000 0000 0100 0101 | 0 0000 0000 0100 0101 | 0000 0000 0000 0000 0000 0000 0100 0101 |
| -0b0 0000 0000 0100 0101| 1 1111 1111 1011 1011 | 1111 1111 1111 1111 1111 1111 1011 1011 |
| 0x45                    | 0 0000 0000 0100 0101 | 0000 0000 0000 0000 0000 0000 0100 0101 |
| "ab"                    | 0 0110 0001 0110 0010 | 0000 0000 0000 0000 0110 0001 0110 0001 |
| "a"                     | 0 0000 0000 0110 0001 | 0000 0000 0000 0000 0000 0000 0110 0001 |

*Note that Binary and Hexadecimal Values will be truncated (in this example) to 21 bits. If there is a negative sign infront of it, the MSB will be set to 1 (if it is not already).*

# Instructions

*In the case of parameters, supported types are listed as letters. They are as follows:*

- **R** Register
- **A** Address
- **I** Immediate
- **P** Pointer
- **C** Program Counter.

_Example: **RAIP** indicates the parameter supports Register/Address/Immediate & Pointer_

## Misc

| Opcode | Assembler Output                        | Title       |
|--------|-----------------------------------------|-------------|
| NOP    | 1000 0000 0000 0000 0000 0000 0000 0000 | No Operation|

## Memory Access
| Opcode | Parameter 1     | Parameter 2      | Title            |
|--------|-----------------|------------------|------------------|
| BYTE   | From: **RAIP**  | To: **RAP**      | Move 8 bits      |             
| DBYT   | From: **RAIP**  | To: **RAP**      | Move 16 bits     |
| QBYT   | From: **RAIPC** | To: **RAP**      | Move 32 bits     |
| PUSH   | From: **RIPC**  |                  | Push on to stack |
| POP    | To: **R**       |                  | Pop from stack   |
| PEEK   | To: **R**       |                  | Peek top of stack|

