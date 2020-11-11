# ARM Reverse Engineering


<!-- vim-markdown-toc GFM -->

* [Data Type](#data-type)
* [Endianess](#endianess)
* [States](#states)
* [Registers](#registers)

<!-- vim-markdown-toc -->

## Data Type

There are word(32 bit), halfword(16 bit), byte(8 bit) both can be signed and unsigned.

```asm
ldr ;load word
ldr(h) ;halfword
   (sh) ;signed halfword
   (b) ;byte
   (sb) ;signed byte

str #store
```

## Endianess

ARM is little-endian before v3.

## States
There are 3 states for ARM processors, ARM, THUMB and THUMB2

ARM: Operands in 4 bytes
Thumb: in 2 bytes
Thumb2: in 2 and some in 4 bytes

## Registers

There are two set of names for arm registers
1.$0~$31 (When using GCC)
2. Pseudoname. Like $ra($31) or $v0($2)(R0)

There are 30 general-purpose registers. From R0 to R15, they can work in user-level mode.

- $V0: stores return value of function
- $SP (Stack Pointer): points to the top of the stack
- $LR (Link Register): Link Register refers the next instruction where the function was initiated from.
- $PC (Program Counter): PC stores the address of the current instruction plus 8 (two ARM instructions) in ARM state (which means the next instruction from current one), and the current instruction plus 4 (two Thumb instructions) in Thumb(v1) state. When we directly read PC it follows the definition that PC points to the next instruction; but when debugging, PC points two instructions ahead of the current PC value.
- $cpsr (Current Program Status Registe), like EFLAGS on x86


