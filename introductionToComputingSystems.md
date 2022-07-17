# This is a note for 《Introduction to Computing Systems》 2005 by Yale Patt and Sanjay Patel

# Chapter 5 LC-3 ISA
> ISA is the *Interface* between the *software commands* and *what the hardware really do*. The ISA determines the computer's **Machine Language**. Once we have determined the ISA, we can begin to design the hardware to implement the ISA, so we say ISA detemines the chip.

1. Memory
- address space is: $2^{16}$
- addressability is 16 bits, so we refer to 16 bits as a word
- word addressable
2. Register
- length of register is also 16 bits which is the length of word in LC-3
- there are 8 general purpose registers(GPR) in LC-3, using 3 bits to identify them.
- there 3 single-bit-resister: N, Z and P for negative, zero and positive. The control instruction can use these 3 registers as condition code to decide what to do.
3. ISA
- instruction is composed of *opcode* and *operand*, the first one determine what the instruction will do. 
- instruction is define by 3 components: opcode, data type(only one data type: 2's complement integers) and addressing mode(define how to get the operand)
- its hard to decide which instruction to be included in ISA, different ISA cares about different application situations.
- there 15 instructions in LC-3, for 3 kinds of purpose: operates, data movement and control. Use 4 bits [15:12] wo distinguish them. All the 15 instructions can be found on Page 142.
- the LC-3 has 5 kind of data addressing modes: immediate, register, 3 memory related(PC-realtive, indirect, Base+offset).
4. operate instructions in LC-3
- NOT: [15:12] operate code is `1001`, [11:9] destination register, [8:6] source register. [5:0] set to 11111.
	> The note operate is *unary operation*, its source and destination is the same
- ADD and AND: both are binary operation. [15:12] `0001` for ADD, `0101` for AND. [11:9] destination regitster. [8:6] first source register. 
5. data movement instructions
> the data movement instructions use all 5 kinds of data accessing modes. Move data between register&memeroy by load and store, between register&IO. There are *7* data move instructions, the format is:

[15:12]|[11:9]|[8:0] --> opcode|registerID|address generating bits(AGB). 
The AGB is used to generate the second operand for the move instructions and it ueses 4 kinds of address accessing modes. The opcode determines which address accessing mode is used.
- PC-Relative Mode
There are two instructions `LD: 0010` and `ST: 0011` which are PC-relative. The AGB of these two instructions means the *Offset* to the PC+1: first do sign-extending to 16 bits then AND with `PC+1`(one if for next PC after fetch this instruction).
The possible range of this offset is (-256,+255).
- Indirect Mode: The difference to PC-relative mode is that *After get PC+1+Offset, we can't use this value to fetch the operand, but the location of the operand*. There are two instructions using indirect mode: `LDI: 0110` and `STI: 0111`.
- Base+Offset Mode: The difference to Indirect Mode is that: *The least 9 bits is not used to add with PC+1. The first 3 bits infer the ID of GPR which used as base register, the remaining 6 bits is sign-extended to 16 bits, then ADD with the base register*. The range of offset is (-32,+31).
There are two instructions using base+offset mode: `LDR: 0110` and `STR: 0111`.
- Immediate Mode: Don't need to access memory when calculating the operand to be stored in register. `LEA: 1110` is short for load effective address. The [11:9] bits of this instruction shown the destination register, then sign-extending the [8:0] bits to 16 bits, ADD with incremented-PC, finally store the value to destination register.



  
