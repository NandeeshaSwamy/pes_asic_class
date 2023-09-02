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
## Introduction to open-source simulator iverilog

<details>
<summary>Introduction to iverilog design testbench</summary>
	
- **Simulator**
  - Simulator is the tool used for simulating the design and iverilog is the tool used for this course.
  - RTL design is checked for adherence to the spec by simulating the design.

- **Design**.
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
- **Design*
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
![Screenshot from 2023-08-31 00-11-02](https://github.com/NandeeshaSwamy/pes_asic_class/assets/135755149/c4e0b7a7-6e5b-4e31-97fc-14de51e9a7a8

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
