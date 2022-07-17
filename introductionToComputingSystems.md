# This is a note for 《Introduction to Computing Systems》 2005 by Yale Patt and Sanjay Patel

# Chapter 5 LC-3 ISA
> ISA is the *Interface* between the *software commands* and *what the hardware really do*. The ISA determines the computer's **Machine Language**. Once we have determined the ISA, we can begin to design the hardware to implement the ISA, so we say ISA detemines the chip.

##  Memory
1. address space is: $2^{16}$
2. addressability is 16 bits, so we refer to 16 bits as a word
3. word addressable
## Register
1. length of register is also 16 bits which is the length of word in LC-3
2. there are 8 general purpose registers(GPR) in LC-3, using 3 bits to identify them.
3. there 3 single-bit-resister: N, Z and P for negative, zero and positive. The control instruction can use these 3 registers as condition code to decide what to do.
## ISA
1. instruction is composed of *opcode* and *operand*, the first one determine what the instruction will do. 
2. instruction is define by 3 components: opcode, data type(only one data type: 2's complement integers) and addressing mode(define how to get the operand)
3. its hard to decide which instruction to be included in ISA, different ISA cares about different application situations.
4. there 15 instructions in LC-3, for 3 kinds of purpose: operates, data movement and control. Use 4 bits [15:12] wo distinguish them. All the 15 instructions can be found on Page 142.
5. the LC-3 has 5 kind of data addressing modes: immediate, register, 3 memory related(PC-realtive, indirect, Base+offset).
## operate instructions in LC-3
1. NOT: [15:12] operate code is `1001`, [11:9] destination register, [8:6] source register. [5:0] set to 11111.
      > The note operate is *unary operation*, its source and destination is the same
2. ADD and AND: both are binary operation. [15:12] `0001` for ADD, `0101` for AND. [11:9] destination regitster. [8:6] first source register. 
## data movement instructions
> the data movement instructions use all 5 kinds of data accessing modes. Move data between register&memeroy by load and store, between register&IO. There are *7* data move instructions, the format is:

[15:12]|[11:9]|[8:0] --> opcode|registerID|address generating bits(AGB). 
The AGB is used to generate the second operand for the move instructions and it ueses 4 kinds of address accessing modes. The opcode determines which address accessing mode is used.
1. PC-Relative Mode
There are two instructions `LD: 0010` and `ST: 0011` which are PC-relative. The AGB of these two instructions means the *Offset* to the PC+1: first do sign-extending to 16 bits then ADD with `PC+1`(one is for next PC after fetch this instruction). After the previous steps, we get the location in memory where the data is, then we can access the data in memory.
The possible range of this offset is (-256,+255).
2. Indirect Mode: The difference to PC-relative mode is that *After get PC+1+Offset, we can't use this value to fetch the operand, but the location of the operand*. There are two instructions using indirect mode: `LDI: 1010` and `STI: 1011`.
3. Base+Offset Mode: The difference to Indirect Mode is that: *The least 9 bits is not used to add with PC+1. The first 3 bits infer the ID of GPR which used as base register, the remaining 6 bits is sign-extended to 16 bits, then ADD with the base register*. The range of offset is (-32,+31).
There are two instructions using base+offset mode: `LDR: 0110` and `STR: 0111`.
4. Immediate Mode: Don't need to access memory when calculating the operand to be stored in register. `LEA: 1110` is short for load effective address. The [11:9] bits of this instruction shown the destination register, then sign-extending the [8:0] bits to 16 bits, ADD with incremented-PC, finally store the value to destination register.
## control instructions
1. there are 5 control instructions in LC-3: conditional branches, unconditional jump, trap, subroutine and return from interrupt.
2. for normal instructions, the PC will +1 after fetch, so the instructions are processed sequentially. In the EXECUTE phase, the processor will examine the 3 condition code mentioned above. If one of the 3 codes is 1, the PC will be revised, this is how the control happend in processor.
3. Conditional Branch(`BR: 0000`), the [8:0] bits is PCOffset, [11:9] is conditional codes for N, Z, P, if one of the 3 codes is set to 1, then the corresponding situation register will be checked to control the flow. For example, if Z=1, then the processor will check if the zero-register is 1, if so then the control instruction will take effect and change PC.
> The example on Page 157 showing how to add 12 integers is worth reading. It explaines how the control instructins works.
4. there are 2 ways to determine the end of loop: the first one is using a counter when we already know the length of input; the second one is using a sentinel which is a stop mark of the input, for example # could be a sentinel when we are input numbers.
5. the `jump: 1100` instruction. The limitaion of BR is that it can't reach all memory space because its PCOffset is only 9 bits, then we create the jump instruction to access all memory space. The [8:6] bits of jump instruction is the ID of register, then the PC is replaced by the value in that register. Because the register is 16 bits, the jump instruction can access all memory space.
