Computer Organization and Architecture: Complete Study Notes
Based on Computer Organization and Architecture: Designing for Performance, 10th Edition by William Stallings

PART 1: INTRODUCTION AND TOP-LEVEL VIEW
1.1 What is a Computer System?
At the top level, a computer consists of processor (CPU), memory, and I/O components, with one or more modules of each type. These components are interconnected to achieve the main function of the computer, which is to execute programs.

1.2 The Four Main Structural Elements
According to Stallings, there are four main structural components of a computer:

Component	Function
CPU (Processor)	Controls the operation of the computer and performs data processing functions
Main Memory	Stores data and programs (volatile; also called real memory or primary memory)
I/O Modules	Move data between the computer and its external environment
System Interconnection	Provides communication among CPU, main memory, and I/O modules
1.3 Computer Functions
A computer performs four basic functions:

Data Processing - Data may take various forms; processing requirements are broad

Data Storage - Short-term and long-term storage

Data Movement - Input/Output (I/O) and Data Communications

Control - A control unit manages resources and orchestrates performance of functional parts in response to instructions

1.4 Architecture vs. Organization
Aspect	Architecture	Organization
Definition	Attributes visible to the programmer	Operational units and interconnections that realize architectural specifications
Examples	Instruction set, data representation, I/O mechanisms, addressing techniques	Control signals, hardware details, interfaces, memory technology
Analogy	What the computer does	How it does it
Family Example	All Intel x86 share same basic architecture	Organization differs between different versions
PART 2: CENTRAL PROCESSING UNIT (CPU)
2.1 CPU Structure
The CPU (Central Processing Unit) consists of three major components:

text
                    ┌─────────────────────┐
                    │      CPU            │
                    │  ┌───────────────┐  │
                    │  │   Control     │  │
                    │  │   Unit (CU)   │  │
                    │  └───────────────┘  │
                    │  ┌───────────────┐  │
                    │  │   ALU         │  │
                    │  └───────────────┘  │
                    │  ┌───────────────┐  │
                    │  │   Registers   │  │
                    │  └───────────────┘  │
                    │  Internal Bus       │
                    └─────────────────────┘
Control Unit (CU): Controls the operation of the CPU and hence the computer

Arithmetic and Logic Unit (ALU): Performs computation or processing of data

Registers: Provide fast, small memory within the processor

2.2 CPU Functions
The CPU must perform the following functions:

Fetch instructions - Read the next instruction from memory

Decode instructions - Interpret the opcode

Fetch operands - Get data needed for the instruction

Execute instructions - Process the data

Store data - Write results back to memory

Check (and possibly serve) interrupts

2.3 The Instruction Cycle
The basic function of a computer is the execution of a program, which consists of a set of instructions stored in memory. The instruction cycle has two main steps:

Instruction Fetch: The processor reads an instruction from memory

Instruction Execute: The processor performs the indicated operation

2.4 Processor Registers
Within the processor, there is a set of registers that provide a level of memory that is faster and smaller than main memory.

Two Categories of Registers:
A. User-Visible Registers - May be referenced by machine language instructions:

Register Type	Description
Data Registers	Can be assigned to various functions; may be general purpose or restricted
Address Registers	Contain main memory addresses of data and instructions
Condition Codes	Status bits (flags) set by ALU operations
B. Control and Status Registers - Used by processor to control operation:

Register	Purpose
Program Counter (PC)	Contains address of next instruction to fetch
Instruction Register (IR)	Contains the current instruction being executed
Memory Address Register (MAR)	Specifies address in memory for next read/write
Memory Buffer Register (MBR)	Contains data to be written or data read from memory
Program Status Word (PSW)	Contains condition codes, interrupt enable/disable, supervisor mode
2.5 Example: Register Organizations
Different architectures have different register organizations:

Intel x86 General Registers:

AX (Accumulator)

BX (Base)

CX (Count)

DX (Data)

SP (Stack Pointer)

BP (Base Pointer)

SI (Source Index)

DI (Destination Index)

PART 3: MEMORY SYSTEM
3.1 Memory Hierarchy
The memory hierarchy addresses the trade-off among capacity, access time, and cost:

text
        ┌─────────────────────────────────────────┐
        │  Faster, more expensive per bit          │
        │  ┌───────────────────────────────────┐  │
        │  │  CPU Registers                    │  │  ← Fastest, smallest
        │  ├───────────────────────────────────┤  │
        │  │  Cache Memory (L1, L2, L3)        │  │
        │  ├───────────────────────────────────┤  │
        │  │  Main Memory (RAM)                │  │
        │  ├───────────────────────────────────┤  │
        │  │  Magnetic Disk (Hard Drive)       │  │
        │  ├───────────────────────────────────┤  │
        │  │  Optical Disk, Tape               │  │  ← Slowest, largest
        │  └───────────────────────────────────┘  │
        └─────────────────────────────────────────┘
        Slower, cheaper per bit
Key Trade-offs:

Faster access time → Greater cost per bit

Greater capacity → Smaller cost per bit

Greater capacity → Slower access time

3.2 Characteristics of Memory Systems
Characteristic	Description
Location	Internal (registers, cache, main memory) vs. External (disk, tape)
Capacity	Expressed in bytes or words
Unit of Transfer	Word or block for internal memory
Access Method	Sequential, Direct, Random, Associative
Performance	Access time, cycle time, transfer rate
Physical Type	Semiconductor, Magnetic, Optical, Magneto-optical
Physical Characteristics	Volatile vs. Nonvolatile
3.3 Cache Memory
Cache memory is a small, fast memory located between the CPU and main memory. Its objective is to speed up memory access so that it is almost as fast as the processor.

Key Cache Concepts:
Hit: Desired data found in cache

Miss: Desired data not in cache; must be fetched from main memory

Hit Ratio: Percentage of memory accesses found in cache

Cache Levels: L1 (fastest, smallest), L2 (slower, larger), L3

Cache Mapping Techniques:
Technique	Description
Direct Mapped	Each block maps to exactly one cache location
Fully Associative	Any block can go anywhere in cache
Set Associative	Compromise; blocks map to a set of locations
3.4 Internal Memory Technology
Semiconductor memory is the most common form of internal memory and can be:

Volatile (e.g., RAM) - loses data when power is off

Nonvolatile (e.g., ROM) - retains data without power

Types of Semiconductor Memory:

RAM (Random Access Memory): Read/write memory

ROM (Read-Only Memory): Permanent storage

SRAM (Static RAM): Faster, more expensive, used for cache

DRAM (Dynamic RAM): Slower, cheaper, used for main memory

3.5 External Memory
External memory consists of peripheral storage devices accessible via I/O controllers:

Magnetic disks (hard drives)

Optical disks (CD, DVD, Blu-ray)

Magnetic tape

PART 4: INPUT/OUTPUT (I/O) SUBSYSTEM
4.1 I/O Problems and Need for I/O Modules
I/O devices present several challenges:

Wide variety of peripherals - different data amounts, speeds, and formats

All slower than CPU and RAM - speed mismatch

Need I/O modules to interface between CPU/memory and external devices

4.2 I/O Module Functions
An I/O module is the entity that controls external devices and exchanges data between CPU, memory, and external devices. Its functions include:

Control and timing - Coordinates the flow of traffic

Processor communication - Exchange data with processor

Device communication - Exchange data with peripheral device

Data buffering - Temporary storage to handle speed mismatches

Error detection - Detects and reports errors

4.3 I/O Module Structure
text
┌─────────────────────────────────────────────────────────┐
│                    I/O MODULE                           │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐│
│  │  Interface  │    │   Control   │    │  Interface  ││
│  │  to CPU &   │◄──►│   Logic     │◄──►│  to External││
│  │  Memory     │    │             │    │  Device(s)  ││
│  └─────────────┘    └─────────────┘    └─────────────┘│
│                           │                             │
│                     ┌─────────────┐                    │
│                     │   Data      │                    │
│                     │   Buffers   │                    │
│                     └─────────────┘                    │
└─────────────────────────────────────────────────────────┘
4.4 I/O Techniques
Stallings describes three techniques for I/O:

1. Programmed I/O
Processor drives I/O hardware modules to perform I/O

Processor sets appropriate bits in I/O status register

Processor continuously checks status until operation complete

Disadvantage: Processor is tied up (wastes CPU time)

2. Interrupt-Driven I/O
I/O module interrupts the processor when ready to exchange data

Processor executes data transfer, then resumes former processing

Advantage: Processor can do other work while waiting

I/O module gets data from peripheral while CPU does other work

3. Direct Memory Access (DMA)
DMA module controls exchange of data between main memory and I/O device

Processor initiates transfer, then continues other work

DMA transfers data directly to/from memory

Cycle stealing: DMA transfers one word at a time, then returns bus control

4.5 I/O Steps (Programmed I/O)
The basic I/O operation steps are:

CPU checks I/O module device status

I/O module returns status

If ready, CPU requests data transfer

I/O module gets data from device

I/O module transfers data to CPU

4.6 I/O Channels and Processors
For more complex systems, Stallings discusses:

I/O Channels: Specialized processors for I/O control

I/O Processors: Offload I/O processing from main CPU

PART 5: SYSTEM INTERCONNECTION
5.1 The System Bus
The system bus is a common mechanism for interconnection among CPU, main memory, and I/O.

A system bus consists of three sets of lines:

Bus Type	Purpose
Data Bus	Carries data between components
Address Bus	Carries memory/device addresses
Control Bus	Carries control signals (read/write, interrupt, etc.)
5.2 Top-Level View
text
                    ┌─────────────────────────────────────┐
                    │         SYSTEM BUS                  │
                    │  ┌─────────┬─────────┬──────────┐  │
                    │  │  Data   │ Address │ Control  │  │
                    │  │  Lines  │  Lines  │  Lines   │  │
                    │  └─────────┴─────────┴──────────┘  │
                    └─────────────────────────────────────┘
                           │    │    │
                    ┌──────┘    │    └──────┐
                    │           │           │
              ┌─────▼────┐ ┌────▼────┐ ┌────▼────┐
              │   CPU    │ │ Memory  │ │   I/O   │
              │          │ │ Module  │ │ Module  │
              └──────────┘ └─────────┘ └─────────┘
SUMMARY: KEY POINTS TO REMEMBER
Computer = CPU + Memory + I/O + Interconnection

CPU has Control Unit, ALU, and Registers - fetches, decodes, executes

Memory hierarchy balances speed, cost, and capacity

Cache memory bridges the CPU-memory speed gap

I/O modules handle the diversity and slowness of peripherals

Three I/O techniques: Programmed, Interrupt-driven, DMA

System bus provides communication among all components

Architecture = what is visible to programmer; Organization = how it's implemented