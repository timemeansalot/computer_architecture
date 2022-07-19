# This is notes by reading 《Digital Design and Computer Architecture, RISC-V Edition》2021 by Sarah Harris and David Harris 
> The book information and supply can be found on [textboos.elsevier](https://textbooks.elsevier.com/web/product_details.aspx?isbn=9780128200643), especially the *Companion Material* part.

# Notes & Problems
## *2022.07.16*
### Notes
1. Power Comsumption
- Definition of Power: Energe used per second
- Dynamic Power: $P_{dynamic}=\alpha CV_{DD}^2 f$, capacitance is C, voltage is $V_{DD}$, frequncy if f, and the capacitor is charged $\alpha$ times per cycle. $\alpha,\alpha\leq 1$ is also called *Activity Factor*, it means the fraction of cycle than capacitor is charged, 
	> *discharging from 1 to 0 is free*
- Static Power: Power Consumed when no switch is charging. $P_{static}=I_{DD}V_{DD}$. Static Power is much smaller than Dynamic Power, it's the power used when we put the iPhone in our pocket(not use it at all!).
### Problems
1. Why NMOS is good for pass 0 while PMOS is good for pass 1?
2. What's the saturation voltage for MOSFET?
3. What is transmission gate?


# Chapter 1 notes
1. doing digital design we have to handle very complex tasks, so the ability to manage complexity is a key skill for engineer and scientist.
2. **Abstraction** is a way to hide anything which is not important. In this way a system can be views from different layers, each layer provide interface for adjacent layer and hide their inner side.

	The abstraction of computer systems is:
	- software
	- OS
	- Architecutre: like X86, ARM, RISC-V. The architecture is defined by **instructions and registers**, so when we compare the CISC with RISC archtecture, we mainly talk about their ISA and registers.
	- Microarchitecutre: Like AMD Athlon, Intel Core i7. These are different implementation of the X86 architecture.
	> Micro-Archtecture combine **Logic elements** to excute the instructions defined by archtecture.
	- Logic: doing some kind of logic like Adders and Memories.
	- Digital Circuit & Analog Circuit: ADD Gate, OR Gate, Amplifier, Filter
	- Device: Transistors
	- Physics: how electrons move from A to B.

 
