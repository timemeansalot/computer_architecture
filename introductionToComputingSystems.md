# This is a note for <<Introduction to Computing Systems>> 2005 by Yale Patt and Sanjay Patel

# Chapter 5 LC-3 ISA
> ISA is the *Interface* between the *software commands* and *what the hardware really do*. The ISA determines the computer's **Machine Language**.

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
[15:12]|[11:9]|[8:0]
opcode|registerID|address generating bits