# VLSI Physical Design for ASICs
## Objective
The objective of VLSI (Very Large Scale Integration) physical design for ASICs (Application-Specific Integrated Circuits) is to transform a logical design description (RTL - Register Transfer Level) into a physical layout that can be fabricated as an integrated circuit. This involves translating the high-level functional representation of the circuit into a physical implementation that meets design constraints, performance targets, and manufacturability requirements.

## SKILL OUTCOMES
+ Architectural Design
+ RTL Design / Behavioral Modeling
+ Floorplanning
+ placement
+ clock Tree Synthesis
+ Routing

## INSTALLATION
https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh
+ Download the run.sh
+ Open terminal
+ cd Downloads
+ ./run.sh
  
## COURSE CONTENT COVERAGE

# DAY 1 

## Theory

<details> 
<summary>Introduction to Basic Keywords</summary>
	
**ISA (Instruction Set Archhitecture)**
  - ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.
  - It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.

**RISC-V (Reduced Instruction Set Computing - Five)**.
  - It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
  - RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions. 

<img width="536" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e31d7c49-7160-443f-b73f-585cde8f3419">
</details>

<details>
<summary>From Apps to Hardware</summary>

1. **Apps:** Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.
2. **System software:** System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'
3. **Operating System:** The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

4. **Compiler:** A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

5. **Assembler:** An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

6. **RTL:** RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

 7. **Hardware:** Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.


**Detail Description of Course Content**

**Pseudo Instructions:** Pseudo-instructions are used to simplify programming, improve code readability, and reduce the number of explicit instructions a programmer needs to write. They are especially useful for common programming patterns that involve multiple instructions.
`Ex: li, mv`.

**Base Integer Instructions:** The term "base integer instructions" refers to the fundamental set of instructions that form the foundation for performing basic arithmetic, logical, and data movement operations.
`Ex: add, sub, and, or, xor, sll`.

**Multiply Extension Intructions:** The RISC-V architecture includes a set of multiply and multiply-accumulate (MAC) extension instructions that enhance the instruction set to perform efficient multiplication and multiplication-accumulate operations.
`Ex: mul, mulh, mulhu, mulhsu`.

**Single and Double Precision Floating Point Extension:** The RISC-V architecture includes floating-point extensions that provide support for both single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations. These extensions are often referred to as the "F" and "D" extensions, respectively. Floating-point arithmetic is essential for handling real numbers with fractional parts and for performing accurate calculations involving decimal values.

**Application Binary Interface:** ABI stands for "Application Binary Interface." It is a set of rules and conventions that govern how software components interact with each other at the binary level. The ABI defines various aspects of program execution, including how function calls are made, how parameters are passed and returned, how memory is allocated and managed, and more.

**Memory Allocation and Stack Pointer** 
- Memory allocation refers to the process of assigning and managing memory segments for various data structures, variables, and objects used by a program. It involves allocating memory space from the system's memory pool and releasing it when it is no longer needed to prevent memory leaks.
- The stack pointer is a register used by a program to keep track of the current position of the program's execution on the call stack. 
</details>

<details>
<summary>Integer Number Representation </summary>

**Unsigned Numbers**
	
- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
- Range: [0, (2^n)-1 ]


**Signed Numbers**
	
- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
- Range : Positive : [0 , 2^(n-1)-1]
          Negative : [-1 to 2^(n-1)]
  
</details>

## Labwork for RISCV Toolchain
<details>
<summary>C Program</summary>

We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.

`leafpad sumton.c`
``` c
#include<stdio.h>

int main(){
	int i, sum=0, n=111;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}
```
Using the gcc compiler, we compiled the program to get the output.

`gcc sumton.c`
`.\a.out`

![Screenshot from 2023-08-20 19-54-45](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/5160f5dc-0d92-42c1-9383-2ddc4770535b)

![Screenshot from 2023-08-20 19-55-25](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/7e1ddd07-05ee-4f07-bf76-8f05ce31b79b)


<summary>RISCV GCC Compiler and Dissemble</summary>

Using the riscv gcc compiler, we compiled the C program.

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`

Using `ls -ltr sum1ton.c`, we can check that the object file is created.

To get the dissembled ALP code for the C program, 

`riscv64-unknown-elf-objdump -d sum1ton.o | less` .

In order to view the main section, type 
`/main`.
Here, since we used -O1 optimisation, the number of instructions are 15.

![Screenshot from 2023-08-20 21-16-47](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/61d6ec00-0ea2-49fa-af58-4f08a9297197)

When we use -Ofast optimisation, we can see that the number of instructions have been reduced to 12.

![Screenshot from 2023-08-20 21-20-30](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/bf6d2202-d05d-42dc-8335-6d3221d27e59)


- -Onumber : level of optimisation required
- -mabi : specifies the ABI (Application Binary Interface) to be used during code generation according to the requirements
- -march : specifies target architecture

In order to view the different options available for these fields, use the following commands

go to the directory where riscv64-unkonwn-elf is present

- -O1 : ``` riscv64-unkonwn-elf --help=optimizer```
- -mabi : ```riscv64-unknown-elf-gcc --target-help```
- -march : ```riscv64-unknown-elf-gcc --target-help```

For different instances,
- use the command ```riscv64-unknown-elf-objdump -d 1_to_N.o | less```
- use ``` /instance``` to search for an instance 
- press ENTER
- press ```n``` to search next occurance
- press ```N``` to search for previous occurance. 
- use ```esc :q``` to quit


<summary>Spike Simulation and Debug</summary>

`spike pk sum1ton.o` is used to check whether the instructions produced are right to give the correct output.

![Screenshot from 2023-08-20 21-22-48](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/96053eaf-0ea6-42f6-9deb-396e1b4ff7c7)


`spike -d pk sum1ton.c` is used for debugging.

The contents of the registers can also be viewed.

![Screenshot from 2023-08-20 21-43-23](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/2db681f1-d0cf-47a6-a38d-22bee6813bf7)

- press ENTER : to show the first line and successive ENTER to show successive lines
- reg 0 a2 : to check content of register a2 0th core
- q : to quit the debug process
</details>

<details>
<summary>Labwork-signed and unsigned numbers</summary>

We wrote a C program that shows the maximum and minimum values of 64bit unsigned numbers.

``` c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```
![Screenshot from 2023-08-20 22-11-56](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/c33e952f-3a79-4665-a240-00a2128597bc)

![Screenshot from 2023-08-20 22-11-30](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/b6418cf7-5ede-4cf7-8ad0-fb2ae02b9dfe)


We wrote a C program that shows the maximum and minimum values of 64bit signed numbers.
``` c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```

![Screenshot from 2023-08-20 22-15-08](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/31cca5f3-1466-4548-a77d-73baf1c684a0)

![Screenshot from 2023-08-20 22-14-46](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/0642867f-ccb3-4ea6-8fbe-30b88c2a9bd5)
</details>

# DAY - 2
## Theory

<details>
<summary>Introduction to ABI</summary>
	
+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
</details>

<details>
<summary>Memmory Allocation for Double Words</summary>
	
64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly
1. **Little-Endian:**
In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. **Big-Endian:**
In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
#### For example, consider the 64-bit hexadecimal value 0x0123456789ABCDEF. 
In Little-Endian representation, it would be stored as follows in memory:

<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8c63e751-8882-4b1e-a2f8-84da628ee604">

In Big-Endian representation, it would be stored as follows in memory:

<img width="454" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3954540e-800f-4503-97ef-6c77daacd058">
</details>

<details>
<summary>Load, Add and Store Instructions</summary>
	
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.

Example `ld x6, 8(x5)`

In this Example
- `ld` is the load double-word instruction.
- `x6` is the destination register.
- `8(x5)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x8, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x8` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x9` is the destination register.
- `x10` and `x11` are the source registers.
</details>

<details>
<summary>2-Registers and their ABI Names</summary>
	
The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.
#### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components. 

<img width="430" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3b7aed64-37cd-492f-b9b5-cd840103566a">
</details>

## Labwork using ABI Function Calls
<details>
<summary>Algorithm for C Program using ASM</summary>
	
- Incorporating assembly language code into a C program can be done using inline assembly or by linking separate assembly files with your C code.
- When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
- The program executes the assembly function, following the assembly instructions you've provided.

<summary>Review ASM Function Calls</summary>
	
- We wrote C code in one file and your assembly code in a separate file.
- In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.

**C Program**
`1to9_custom.c`
  ``` c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
```
![Screenshot from 2023-08-21 21-29-29](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/fa84c6c8-ab12-4aba-831e-e34f04f1ce11)

`load.s`
``` s
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```
![Screenshot from 2023-08-21 21-29-58](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/8146a3a0-dd7d-4137-8ecf-11f02d263f97)


<summary>Simulate C Program using Function Call</summary>
	
**Compilation:** To compile C code and Asseembly file use the command

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o 1to9_custom.o 1to9_custom.c load.s` 

this would generate object file `1to9_custom.o`.

**Execution:** To execute the object file run the command 

`spike pk 1to9_custom.o`

![Screenshot from 2023-08-21 21-31-24](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/63e68a8b-35ff-4110-b90c-7145d42391e5)
</details>

# DAY - 3
## Theory

<details>
<summary>Introduction to open-source simulator iverilog</summary>
	
### Introduction to iverilog design testbench
	
- **Simulator**
  - Simulator is the tool used for simulating the design and iverilog is the tool used for this course.
  - RTL design is checked for adherence to the spec by simulating the design.

- **Design**
  - Design is the actual Verilog code or set of verilog codes which has the intended functionality to meet with required specifications.

- **Testbench**
  - Testbench is the setup to apply stimulus(test_vectors) to the design to check its functionality.
<img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/eb806b04-e6c0-4b03-8214-80cf0183ad76">

- **How simulator works?**.
  - simulator looks for the changes on the input signals.
  - Upon changes to the input the output is evaluated.
 
- **GTKWave**
  - Used for viewing the simulated waveforms.
    
- **iverilog based simulation flow**
<img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/0bbdc2e2-0b2a-4b26-8ed0-7eae4c7e3bf6">
</details>

## Labs using iverilog and gtkwave

<details>
<summary>Introduction to iverilog and gtkwave</summary>
	
- **Simulating 2:1 mux using iverilog and gtkwave**
- **Design**

![Screenshot from 2023-08-30 17-49-55](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/c7a2996b-34f3-4eb6-aed7-6828cdd3c299)

- **Testbench**

![Screenshot from 2023-08-30 17-50-08](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/6769cf92-2457-4f42-8ccd-fdb7c6b221f1)


- **Simulated waveform in gtkwave**
![Screenshot from 2023-08-30 17-48-10](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/ce7c54b0-164f-47d6-a7e2-5f7fa0a61fbc)


</details>

<details>
<summary>Introduction to yosys and logic synthesis </summary>

 <img width="600" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/d35aae33-f873-4e82-a052-b111a9f6d733">
 
- **Synthesizer**
- A tool used for converting the RTL to netlist.
- Yosys is the synthesizer tool used in this course.

- **Synthesis**
- RTL to Gate level translation.
- The design is converted into gates and the connections are made between the gates.
- This is given out as a file called netlist.

- **What is .lib?**
- Collection of logic modules.
- Includes basic logic gates like AND, OR, NOT,etc.
- Different flavours of same gate.

- **Faster cells vs slow cells**
- load in digital logic circuit-> Capacitance
- Faster the charging/discharging of capacitance -> lesser the cell delay
  	- to charge/discharge the capacitance fast, we need transistors capable of sourcing more current.
  	- Wider transistors -> Low Delay -> More area and power as well.
  	- Narrow transistors -> More delay -> Less area and power
  	- Faster cells do not come free, they come at penalty of area and power.
</details>

## Labs using Yosys and Sky130 PDKs
<details>
<summary>Lab-1</summary>
	
- **Invoking yosys**

![Screenshot from 2023-08-30 22-38-35](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/acd4c2cf-1375-47b3-99e1-fbf9c25c1a64)


- **Synthesizing 2:1 mux**

![Screenshot from 2023-08-30 22-49-34](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/50138810-e5a7-4482-9ef6-35e7db98445f)

![Screenshot from 2023-08-30 22-50-48](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/e8f784db-e1b3-4237-9279-9bc1d4b24c1c)


- **Synthesis result**

![Screenshot from 2023-08-30 22-52-24](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/4017a0a8-8fae-4d50-ab71-b3be916acde1)

</details>

<details>
<summary>Lab-2</summary>
	
- **Netlist with extra information**

![Screenshot from 2023-08-31 00-11-02](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/88323a7a-055f-420b-aa93-d817571b6249)


- **Smaller netlist**

![Screenshot from 2023-08-31 00-11-52](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/fc1db078-66e4-4b93-884f-0d498dff55d5)

</details>

# DAY - 4
## Introduction to timing .libs

<details>
<summary> Introduction to dot .lib </summary>

- **Contents in .lib file**

![Screenshot from 2023-09-03 00-02-09](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/256f4346-5114-4fd6-99ec-a0296c3f0323)

- Frst line the .lib file contains
	- tt : indicates variations due to process and here it indicates Typical Process.
  	- 025C : indicates the variations due to temperatures where the silicon will be used.
  	- 1v80 : indicates the variations due to the voltage levels where the silicon will be incorporated.

- **Various parameters**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/b7527017-3e60-4c79-a5a8-3612c8555dd7">

- **Power consumption and area comparison**
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/a6dc1db5-f6ab-4d84-8cab-7c6062e2a6b6">

</details>

## Hierarchical vs Flat Synthesis
<details>
<summary> Hierarchical Synthesis Flat Synthesis </summary>

- **Hierarchical Synthesis** - Hierarchical synthesis is an approach in digital design and logic synthesis where complex designs are broken down into smaller, more manageable modules or sub-circuits, and each module is synthesized individually. These synthesized modules are then integrated back into the overall design hierarchy. This approach helps manage the complexity of large designs and allows designers to work on different parts of the design independently.
- Here we use mutiple module.v and invoke yosys
![Screenshot from 2023-09-03 00-12-02](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/2f435c7d-91cb-4d83-bdcb-80940c283df8)

- synth -top multiple_modules to set it as top module
![Screenshot from 2023-08-31 17-00-56](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/9aa69c10-2eb2-4e36-9ed4-6d968dd9dbe3)

- To view the netlist show multiple_modules
![Screenshot from 2023-08-31 17-07-00](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/4f47333f-1504-49d5-80b3-b0560628e863)

- !gvim multiple_modules_hier.v
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/5c9256a2-06bf-4995-bd38-1437ba883b46">

- **Flattened Synthesis** - Flattened synthesis is the opposite of hierarchical synthesis. Instead of maintaining the hierarchical structure of the design during synthesis, flattened synthesis combines all modules and sub-modules into a single, flat representation
- netlist
![Screenshot from 2023-08-31 22-52-05](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/77fb4ea3-6af6-464a-9c77-611624e3da5d)

- !gvim multiple_modules_flat.v
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/87e0ba3b-156a-41cb-bc54-8f93e8f9ab60">

- **Sub Module level Synthesis** - Sub-module level synthesis is preferred when there are multiple instances of same module. Sythesizing the same module over several times may not be advantageous with respect to time. Instead, synthsis can be performed for one module, its netlist can be replicated and then stitched together in the top module. This is also used particulary in massive designs using divide and conquer method.

- Statistics
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1bd7dda1-37e5-43f3-8854-ae3f4f9b5626">

- Netlist

![Screenshot from 2023-08-31 22-57-05](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/869f01d5-08e5-4ca3-b8ea-226c390c15ec)

</details>

## Various Flop Coding Styles and Optimization

<details>
<summary>Why Flops and Flop Coding Styles</summary>

**Why do we need a Flop?** 
- A flip-flop (often abbreviated as "flop") is a fundamental building block in digital circuit design.
- It's a type of sequential logic element that stores binary information (0 or 1) and can change its output based on clock signals and input values.
- In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed.
- During the propagation of data, if there are different paths with different propagation delays, then a glitch might occur.
- There will be multiple glitches for multiple combinational circuits.
- Hence, we need flops to store the data from the combinational circuits.

**D Flip-Flop with Asynchronous Reset** 
-  When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
-  Else, on the positive edge of the clock, the stored value is updated at the output.
  
+ `gvim dff_asyncres_syncres.v`
![Screenshot from 2023-09-03 00-31-46](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/e7fc9b45-1e8c-4338-a2c4-20fec9f47250)

**D Flip_Flop with Asynchronous Set** 
-  When the set is high, the output of the flip-flop is forced to 1, irrespective of the clock signal.
-  Else, on positive edge of the clock, the stored value is updated at the output.
  
+ `gvim dff_async_set.v`

![Screenshot from 2023-09-03 00-30-21](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/ad00e3d7-c6ca-4ef3-ac1f-63e6de402ebc)


**D Flip-Flop with Synchronous Reset** 
-  When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
-  Else, on the positive edge of the clock, the stored value is updated at the output.
  
+ `gvim dff_syncres.v`

![Screenshot from 2023-09-03 00-29-37](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/246ff733-1c02-411d-abd7-4a3d36e97997)

**D Flip-Flop with Asynchronous Reset and Synchronous Reset** 
-  When the asynchronous resest is high, the output is forced to 0.
-  When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
-  Else, on the positive edge of the clock, the stored value is updated at the output.
-  Here, it is a combination of both synchronous and asynchronous reset DFF.

+ `gvim dff_asyncres_syncres.v`
![Screenshot from 2023-09-03 00-31-46](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/e7fc9b45-1e8c-4338-a2c4-20fec9f47250)

</details>


<details>
<summary>Lab Flop Synthesis Simulations </summary>

**D Flip-Flop with Asynchronous Reset** 
-  Simulation
![Screenshot from 2023-09-01 00-20-39](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/603c6fc1-1e97-4ceb-bc83-6f4388989cb3)

-  Synthesis
![Screenshot from 2023-09-01 16-04-19](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/5d0a2e0f-0301-4d2a-ae20-728967cb8332)


**D Flip_Flop with Asynchronous Set** 
-  Simulation
![Screenshot from 2023-09-01 00-22-47](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/1dee7cfb-c266-4fe1-b36e-026ede2af219)

-  Synthesis
![Screenshot from 2023-09-01 16-08-37](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/2ec656eb-8331-4fe4-a7b0-156da5a88628)


**D Flip-Flop with Synchronous Reset** 
-  Simulation
![Screenshot from 2023-09-01 00-24-55](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/78964629-5516-4620-94cb-ef5e79f2bda6)

-  Synthesis
![Screenshot from 2023-09-01 16-10-31](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/38b18137-91a4-41be-98ef-efc46004bffb)

</details>


<details>
<summary>Interesting optimisations </summary>


   **mult_2** 
   
-  gvim mult_2.v

![Screenshot from 2023-09-03 00-47-47](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/a2ca75c8-4f7f-4af1-a849-eefbad97ec6e)

-  Statistics

![Screenshot from 2023-09-01 22-45-29](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/8d8e38b4-7d19-489f-a09e-2bde43131abc)

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/7e3ba671-c5ef-4bcb-aac6-7ab95b02c87e">

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/6ff861d3-adc6-4488-9d97-0cd65eb049e5">

   **mult_8** 
   
-  gvim mult_8.v

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1c87e450-e8e8-45fd-8171-38e3f9f83e6c">

-  Statistics

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/a347f5ad-b9d2-445e-acd2-f14c68b4d835">

-  Netlist
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e4cde78b-26c5-4d28-a23f-4dd6bbf435c9">

<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/8c1d0c7e-3da1-4ff2-91fd-bb75fc88eabd">

</details>


# DAY - 5
## Introduction to Logic Optimizations

<details>
<summary> Combinational Logic Optimization </summary>
	
- **Combinational logic**
- Combinational logic refers to logic circuits where the outputs depend only on the current inputs and not on any previous states.

- **Types of Combinational Optimizations**
- Constant Propagation
- Boolean Logic Optimization. 

</details>


<details>
<summary> Sequential Logic Optimization </summary>
	
- **Sequential Logic**
- Sequential logic optimizations involve improving the efficiency, performance, and resource utilization of digital circuits that include memory elements like flip-flops and latches.

- **Types of Sequential Optimizations**
- Sequential Constant Propagation
- State Optimization
- Retiming
- Sequential Logic cloning(Floorplan aware synthesis)

</details>

## Combinational Logic Optimisations

<details>
<summary> opt_check </summary>
	
-  gvim opt_check.v
  
![Screenshot from 2023-09-03 02-02-26](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/c549ce79-442a-449a-a16b-4931d14e2c4f)

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f81b6c38-982a-487f-a4c4-4afa2cf86a50">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f2d45e9a-87f4-4fd8-b670-d4bee7d06750">

</details>

<details>
<summary> opt_check2 </summary>
	
-  gvim opt_check2.v
  
![Screenshot from 2023-09-03 02-02-49](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/3562abe2-4d55-4c8a-9193-51143f8b8864)

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/02ae9ced-5e9a-4aea-b92a-bc9c6cfd6463">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/9f964c30-fa98-48bb-bac9-fe8b18758ad7">

</details>

<details>
<summary> opt_check3 </summary>
	
-  gvim opt_check3.v
  
![Screenshot from 2023-09-03 02-03-15](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/278de9dc-1054-4a2a-96e8-855283a8f830)

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/e2a968e2-8878-496e-86d2-716de521113a">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/a6ad0d4f-e15d-4a02-95b1-6a859559fee1">

</details>

<details>
<summary> opt_check4 </summary>
	
-  gvim opt_check4.v
  
![Screenshot from 2023-09-03 02-03-25](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/51ab29e7-9fe9-429a-993f-63e15f63fdb9)

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/f1113645-47f1-4131-ad17-852795422647">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/4340cb4a-41b7-42ea-a6b5-760891410967">

</details>


## Sequential Logic Optimisations

<details>
<summary> dff_const1 </summary>
	
-  gvim dff_const1.v
  
![Screenshot from 2023-09-03 11-14-43](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/d980a6ae-4aeb-4ea8-a4bb-f3d048610e11)

-  Simulation

![Screenshot from 2023-09-03 11-19-16](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/c09ace95-a308-47c6-a6ce-412a3691dd8e)

-  Statistics
  
![Screenshot from 2023-09-03 11-23-38](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/a791c85d-9ca0-48b8-a93d-6ef082e2e253)

-  Netlist

![Screenshot from 2023-09-03 11-25-04](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/e69199fa-f3fd-40e7-ab26-9ad819715b57)

</details>

<details>
<summary> dff_const2 </summary>
	
-  gvim dff_const2.v
  
![Screenshot from 2023-09-03 11-14-48](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/8fe7b164-b0bb-49f8-933a-5ae8949f29b7)

-  Simulation

![Screenshot from 2023-09-03 11-21-22](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/a969ce49-7a3e-4a0f-ba0c-1a023a0de216)

-  Statistics
  
![Screenshot from 2023-09-03 11-27-21](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/0d11d078-7465-4439-9367-bcdc306fa007)

-  Netlist

![Screenshot from 2023-09-03 11-27-43](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/783a623a-1dd6-4c5b-a552-708ce7c88d76)

</details>



<details>
<summary> dff_const3 </summary>
	
-  gvim dff-const3.v
  
![Screenshot from 2023-09-03 11-14-57](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/3b2bd556-16ae-4da4-ae0f-9ca9672e72e3)

-  Simulation

![Screenshot from 2023-09-03 11-35-03](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/f17a00a6-acc0-402e-98c6-e1932273afbe)

-  Statistics
  
![Screenshot from 2023-09-03 11-29-39](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/3e894d39-e9c2-448a-ae2e-87ab281a49bc)

-  Netlist

![Screenshot from 2023-09-03 11-32-28](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/17584892-fd61-4273-8502-dd41bd8bfcb6)

</details>


<details>
<summary> dff_const4 </summary>
	
-  gvim dff_const4.v
  
![Screenshot from 2023-09-03 11-15-03](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/8dd06a08-6779-4446-86da-dd2feefb7c56)

-  Simulation

![Screenshot from 2023-09-03 11-53-23](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/0a8fd494-efd1-4af5-bd1e-cb5094b28304)

-  Statistics
  
![Screenshot from 2023-09-03 11-56-32](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/a70f90a5-9679-42d3-ada6-20f4e95db526)

-  Netlist

![Screenshot from 2023-09-03 11-55-38](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/23686b31-8f01-4f1d-bda5-4ca4f0289b00)

</details>


<details>
<summary> dff_const5 </summary>
	
-  gvim dff_const5.v

![Screenshot from 2023-09-03 11-15-21](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/143544ea-cc1f-41df-9ae9-1fda8e16955a)


-  Simulation

![Screenshot from 2023-09-03 11-54-15](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/ac81f8ce-20ed-4b6b-8a3b-3d20dab7884f)

-  Statistics
  
![Screenshot from 2023-09-03 11-56-48](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/3872bc35-8dd2-4002-93a6-3a944eaea513)

-  Netlist

![Screenshot from 2023-09-03 11-57-32](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/e927ab71-cb98-4fa9-9bf6-1471e0952421)

</details>

## Sequential Optimisations for Unused Outputs

<details>
<summary> counter_opt </summary>
	
-  gvim counter_opt.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/9869250b-d8b6-4b58-930c-b4a7bab31c27">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/6cbe7b44-d6eb-4bd9-86cf-ba63d362ae2f">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/8a74443f-c492-4c6b-b354-45fcd416bdfc">

</details>


<details>
<summary> counter_opt2 </summary>
	
-  gvim counter_opt2.v
  
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/771a532b-2363-4e04-bb7c-402352913348">

-  Statistics
  
<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/487f3e7e-8df4-4d4c-a457-ce983a5544d5">

-  Netlist

<img width="350" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/ba5bc039-54cb-440e-94d4-0f2be4eda2d2">

</details>

# Day - 6
## GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements

<details>
<summary>GLS Concepts and Flow using Iverilog</summary>
	
**Gate Level Simulation (GLS)**
- Running the testbench against the synthesized netlist ouput as a DUT is known as Gate Level Simulation (GLS). The Output netlist should logically be same as the RTL code so that the testbench will align itself when we simulate both the files to obtain the waveforms.
- GLS is required to verify the logical correctness of the design post synthesis with the help of the netlist file. It ensures whether the timing of the design is met and for thi, the GLS used to run with delay annotations.
<img width="500" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/1aebc269-44a0-4426-bab9-f55c2fe2ade5">

**Synthesis and simulation mismatch**
- If netlist is a true reciprocation of RTL, what is the need to validate the functionality of netlist? There may be synthesis and simulation mismatch due to the following reasons:
	-  Missing sensitivity list
 	-  Blocking vs non-blocking assignments
   	-  Non standard verilog coding

**Blocking statements**
- Executes the statements in the order in which they are coded

  ``` v
   module BlockingExample(input A, input B, input C, output Y, output Z);
    wire temp;

    // Blocking assignment
    assign temp = A & B;

    always @(posedge C) begin
        // Blocking assignment
        Y = temp;
        Z = ~temp;
    end
   endmodule
  ```
**Non - blocking statements**
- Executes the RHS of all such assignments when the always block is entered and assigned to LHS in a parallel evaluation.

  ``` v
    module NonBlockingExample(input clock, input D, input reset, output reg Q);

    always @(posedge clock or posedge reset) begin
        if (reset)
            Q <= 0;  // Reset the flip-flop
        else
            Q <= D;  // Non-blocking assignment to update Q with D on clock edge
    end
  endmodule
   ```
**Caveats with Blocking Statements**
- Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. Here are some important caveats associated with using blocking statements:
    - Procedural Execution: Blocking statements are executed sequentially in the order they appear within a procedural block (such as an always block). This can lead to unexpected behavior if the order of execution matters and is not well understood.
    - Lack of Parallelism: Blocking statements do not accurately represent the parallel nature of hardware. In hardware, multiple signals can update concurrently, but blocking statements model sequential behavior. As a result, using blocking statements for modeling complex concurrent logic can lead to incorrect simulations.
    - Race Conditions: When multiple blocking assignments operate on the same signal within the same procedural block, a race condition can occur. The outcome of such assignments depends on their order of execution, which might lead to inconsistent or unpredictable behavior.
    - Limited Representation of Hardware: Hardware systems are inherently concurrent and parallel, but blocking statements do not capture this aspect effectively. Using blocking assignments to model complex combinational or sequential logic can lead to models that are difficult to understand, maintain, and debug.
    - Combinatorial Loops: Incorrect use of blocking statements can lead to unintentional combinational logic loops, which can result in simulation or synthesis errors.
    - Debugging Challenges: Debugging code with many blocking assignments can be challenging, especially when trying to track down timing-related issues.
    - Not Suitable for Flip-Flops: Blocking assignments are not suitable for modeling flip-flop behavior. Non-blocking assignments (<=) are generally preferred for modeling flip-flop updates to ensure accurate representation of concurrent behavior.
    - Sequential Logic Misrepresentation: Using blocking assignments to model sequential logic might not capture the intended behavior accurately. Sequential elements like registers and flip-flops are better represented using non-blocking assignments.
    - Synthesis Implications: The behavior of blocking assignments might not translate well during synthesis, leading to potential mismatches between simulation and synthesis results.

</details>

## Labs on GLS and Synthesis-Simulation Mismatch

<details>
<summary> ternary_operator_mux </summary>	

+ `gvim teranry_operator_mux.v`

![Screenshot from 2023-09-03 14-34-30](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/7f741757-a00c-43d3-95a7-ba184c6ae41a)

**Simulation**

![Screenshot from 2023-09-03 14-33-49](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/bcc1e193-82fd-4af9-865d-46bc4c2285cf)

**Synthesis**

![Screenshot from 2023-09-03 14-36-01](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/0bd2e37c-c682-4fcb-bd89-f4180c32b257)

![Screenshot from 2023-09-03 14-40-51](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/bb0f64b0-f49c-4485-aabc-a2b19d75e623)


**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`

![Screenshot from 2023-09-03 15-03-39](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/8ab1476f-fa15-40a1-bacf-498a56fa3cdc)

</details>


<details>
<summary> bad_mux </summary>	

 + `gvim bad_mux.v`

![Screenshot from 2023-09-03 15-05-57](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/b6247916-a08a-413d-aaf3-1f54d4df9009)

**Simulation**

![Screenshot from 2023-09-03 15-07-32](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/68734e7b-13d6-425b-b516-d74796aba6fd)

**Synthesis**

![Screenshot from 2023-09-03 15-08-45](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/3e0b6cff-6f0e-4e52-a67b-b7bcdc7c74e5)

<img width="400" alt="image" src="https://github.com/PoojaR07/pes_asic_class/assets/135737910/142a9b05-579b-4036-8462-0bdf7bc6a706">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`

![Screenshot from 2023-09-03 16-06-19](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/765abc09-4a27-4175-b766-87d0246ba217)

</details>

## Labs on Synth-Sim Mismatch for Blocking Statement

<details>
<summary> blocking_caveat </summary>	

+ `gvim blocking_caveat.v`

![Screenshot from 2023-09-03 16-07-11](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/33e7f07c-3f34-4f6b-8bf4-af12c9ee84be)

**Simualtion**

![Screenshot from 2023-09-03 16-08-49](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/01f04161-87e0-4167-b0dc-3cc1736b74d5)

**Synthesis**

![Screenshot from 2023-09-03 16-09-45](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/9ea41962-3006-46c3-bba0-568f745a17e3)

![Screenshot from 2023-09-03 16-10-30](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/f4f13492-7622-4619-956e-ffbbeb89cadf)

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v`

![Screenshot from 2023-09-03 16-13-35](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/fe6fdb2e-ce15-4648-9e28-23acc3667484)

</details>
