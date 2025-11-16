# Inception of Open-Source EDA, OpenLANE and sky130PDK

## 1 How to talk to Computers
## 1.1 Introduction to QFN-48 Package, Chips, Pads, Core, Die and IPs

- Package - A package on a chip board is the integrated assembly where a semiconductor die is encapsulated within a protective package and electrically interfaced with the printed circuit board (PCB) for system-level functionality. The package acts as a mechanical support, electrical interface, and thermal path between the silicon and the external environment. Internally, the die is attached to a package substrate using die-attach materials (such as epoxy or solder), and interconnections are established through wire bonding or flip-chip bumps. The package substrate provides signal redistribution, impedance control, and isolation through multiple metal and dielectric layers, often fabricated using high-density interconnect (HDI) technology.

<img width="1621" height="1311" alt="Screenshot 2025-10-27 213545" src="https://github.com/user-attachments/assets/ca5b9eb7-1272-45b2-b6ca-6e43ce23e284" />

- SoC Processor - A System-on-Chip (SoC) processor is an integrated circuit that consolidates all the essential components of a complete computing system onto a single silicon chip. Unlike traditional architectures where the CPU, memory, and peripheral controllers exist as separate chips, an SoC integrates multiple functional blocks—including the processor cores (CPU and sometimes GPU), memory interfaces, I/O controllers, digital signal processors (DSPs), hardware accelerators, and power management circuits—into one compact unit.

<img width="2944" height="1673" alt="Screenshot 2025-10-27 213623" src="https://github.com/user-attachments/assets/87678d79-e4c7-46a9-84d6-dcd720eccc33" />

- Pads, Core, Die - Inside a chip, all electrical communication between the external world and the internal circuitry occurs through specialized input/output terminals known as pads. These pads are located along the periphery of the silicon die and serve as the physical connection points for signals such as power, ground, clocks, and data I/Os. The area enclosed by the pads is referred to as the core, which houses all the digital logic—including standard cells, memory blocks, and interconnect networks—that implement the chip’s functionality. The core is where the actual computation and signal processing take place, while the pads act as the interface enabling interaction with other components on the board or within the system.

<img width="1853" height="1636" alt="Screenshot 2025-10-27 213710" src="https://github.com/user-attachments/assets/d2ba99a1-69df-4109-af73-7af74c19dce3" />

Together, the core and the pad frame constitute the die, which is the fundamental unit produced during the semiconductor manufacturing process. The die is later encapsulated within a package to form the complete integrated circuit (IC) device.

<img width="2361" height="1616" alt="Screenshot 2025-10-27 213752" src="https://github.com/user-attachments/assets/88f891c2-ce78-41c2-9725-9938477117ca" />

- Marcos - Macros are pre-designed, silicon-proven functional blocks like SRAMs, PLLs, ADCs, DACs, and I/O cells, optimized for performance, area, and power. Implemented as hard IPs, they have fixed physical and timing characteristics, enabling designers to integrate complex functions quickly without redesign, thus reducing design time and ensuring reliability.
- Foundry IPs - Foundry IPs are process-specific libraries and components provided by semiconductor foundries to ensure design compatibility with a given technology node (e.g., 7nm, 28nm). They include standard cells, I/O libraries, memory compilers, and analog IPs, all pre-validated and optimized to meet electrical, timing, and reliability requirements during chip manufacturing.

<img width="2912" height="1623" alt="Screenshot 2025-10-27 213824" src="https://github.com/user-attachments/assets/03012761-f2e2-4973-afb7-eb46e18a13a6" />

## 1.2 Introduction to RISC-V

## RISC-V Instruction Set Architecture (ISA)
It is a language of computer, the way how we communicate with the computer. If we have a C program and that needs to be runned on a hardware in the particular layout in certain terms. C program first needs to be compiled to assembly level program which is RISC-V assembly program that is then converted to machine learning program that is binary language program '0' and '1's. Then those bits run in the layout and we get desired output.

Starts with RISC-V architecture implemented through picorv32 cpu core and set to layout (qflow)

<img width="2399" height="1524" alt="Screenshot 2025-10-27 214932" src="https://github.com/user-attachments/assets/776eac41-267d-4456-9c56-bcbe6e710e68" />

## 1.3 From Software Applications to Hardware

Operating System - handle I/O operations
                   allocate memory
                   low level system functions
Instr1, Instr2 acts as an abstract interface between the hardware and C, C++, Java

<img width="3425" height="2159" alt="Screenshot 2025-10-27 220426" src="https://github.com/user-attachments/assets/3ac34451-3b19-43ad-907d-a6a1f687a6f9" />

## Abstract Interface ( Instruction Set Architecture) 
A C program which has to be run on a specific hardware layout which is the interior of a chip in your laptop, there is certain flow to be followed.
Initially, this particular C program is compiled in it's assembly language program which is nothing but RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture).
Following this, the assembly language program is then converted to machine language program which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
Directly after this, we've to implement this RISC-V specification using some RTL (a Hardware Description Language). Finally, from the RTL to Layout it is a standard PnR or RTL to GDSII flow.
For an application software to be run on a hardware there are several processes taking place. To begin with, the apps enters into a block called system software and it converts the application program to binary language. There are various layers in system software in which the major layers or components are OS (Operating System), Compiler and Assembler.
At first the OS outputs are small function in C, C++, VB or Java language which are taken by the respective compiler and converted into instructions and the syntax of these instructions varies with the hardware architecture on which the system is implemented.
Then, the job of the assembler is to take these instructions and convert it into it's binary format which is basically called as a machine language program. Finally, this binary language is fed to the hardware and it understands the specific functions it has to perform based on the binary code it receives.

<img width="3404" height="2149" alt="Screenshot 2025-10-27 220318" src="https://github.com/user-attachments/assets/48df1abe-751b-4de1-bf00-a89487d2f578" />

## 2 SoC Designs and OpenLANE

## 2.1 Introduction to all components of Open Source Digital Asic Design

For open-source ASIC design implemantation, we require the following enablers to be readily available as open-source versions. They are:-
- RTL Designs
- EDA Tools
- PDK Data
Initially in the early ages, the design and fabrication of IC's were tightly coupled and were only practiced by very few companies like TI, Intel, etc.

<img width="1601" height="908" alt="Screenshot 2025-10-29 222645" src="https://github.com/user-attachments/assets/2f1931ad-5df5-4dec-a622-7bc87caa7aaf" />

What is a PDK?
- In the "age of gods" the designs of an Ic was tightly integrated with the manufacturing, process available within each company.
  - Those who controlled the physics controlled the creative agenda!
- Lynn conway and Carver made envisioned the need for separating the design from technology
  - Pioneered the "structred" design methodology based on λ-based rules.
- Since then, we started to see pure play fabs and fabless design companies.
- PDK the interface between the FAB and the designers
- PDK = Process Design Kit
- Collection of files used to model a fabrication process for the EDA tools used to model a fabrication process for the EDA tools used to design an IC.
- Process design rules :- DRC, LVS, PEX

Is 130nm fast?
Yes, Intel P4EE @ 3.46 (Q4'04), OSU team reported 327Mhz post-layout clock frequency for a single cycle RV32i CPU.
 - A pipelined version can achieve > 1GHz clock!

Simplified RTL to GDSII Flow

<img width="1672" height="611" alt="Screenshot 2025-10-27 223020" src="https://github.com/user-attachments/assets/863c2eaa-e27b-4c86-9251-dba8a2594f83" />

- Synthesies
- Floor/Power Planning
- Placement
- Clock Tree Synthesies
- Routing
- Sign Off

Converts RTL to a Circuit out of components from the Standard Cell Library (SCL)

<img width="1646" height="485" alt="Screenshot 2025-10-27 223758" src="https://github.com/user-attachments/assets/17e8ab06-3d66-4aa7-8414-78cee7336238" />

- SYNTHESIS
"Standard Cells" have regular layout
Each has different views/models.
 - Electrical, HDL, SPICE
 - Layout (Abstract and Detailed)

<img width="959" height="660" alt="Screenshot 2025-10-27 231310" src="https://github.com/user-attachments/assets/114ed019-37e3-41e0-97c6-ea7c4e4f9bfd" />

- FLOOR & POWER PLANNING
Chip - Floor Planning :- partition the chip die between different system building blocks and place the I/O pads.

<img width="2323" height="564" alt="Screenshot 2025-10-27 233726 - Copy" src="https://github.com/user-attachments/assets/4ed81c8a-22c2-4af0-8169-c6afbde40e7b" />

Macro - Floor Planning :- dimensions, pin locations, rows and definition.

<img width="797" height="631" alt="Screenshot 2025-10-27 234018" src="https://github.com/user-attachments/assets/5050addd-083f-45f2-b861-cce86349c4e6" />

- POWER PLANNING
Power Planning typically uses upper metal layers for power distribution since thay are thicker than lower metal layers and so have lower resistance and PP is done to avoid electron migration and IR drops.

<img width="1327" height="675" alt="Screenshot 2025-10-27 234055" src="https://github.com/user-attachments/assets/ff35d3fb-ace5-4170-83c0-46259c7c9cd1" />

- PLACEMENT
Place the cells on the floorplan rows, aligned with the sites.

<img width="1824" height="639" alt="Screenshot 2025-10-27 234246" src="https://github.com/user-attachments/assets/fd87a0d4-c39f-48cc-ab37-68ec8bf84407" />

Usually done in two steps :- Global and Detailed

<img width="1640" height="686" alt="Screenshot 2025-10-27 234436" src="https://github.com/user-attachments/assets/340f86ab-d402-4211-b710-f735bfec7d58" />

- CLOCK TREE SYNTHESIS
Create a clock distribution network
 - To deliver the clock to all sequential element.
 - With minimum skew (zero is hard to achieve)
 - Usually a tree (H,X,...)

<img width="681" height="521" alt="Screenshot 2025-10-27 234516" src="https://github.com/user-attachments/assets/bf14f054-d339-49d6-8f3a-ea1e86cc2f49" />

- ROUTING
Implement the interconnect using the available metal layers.
 - Metal tracks from a routing grid
 - Routing grid is huge
 - Divide and Conquer
   - Global routing :- generates routing guides.
   - Detailed routing :- uses the routing guides to implement the actual writing.
 
 <img width="2068" height="790" alt="Screenshot 2025-10-27 234936" src="https://github.com/user-attachments/assets/d840e589-aef9-49c7-8650-5e56b67a4ae3" />
 
- SIGN OFF
Physical Verification
 - Design Rules Checking (DRC)
 - Layout vs Schematic (LVS)
Timing Verification
 - Static Timing Analysis (STA)

<img width="2210" height="933" alt="Screenshot 2025-10-28 000738" src="https://github.com/user-attachments/assets/764d7752-6ff9-4687-8698-acc2fe444381" />

Open Source ASIC Flow
OpenLANE started as an Open-source flow for a true Open source tape out experiments.
Strive is a family of open everything SoCs.
- Open PDK, Open EDA, Open RTL

<img width="1976" height="819" alt="Screenshot 2025-10-28 001146" src="https://github.com/user-attachments/assets/de087183-afd9-4095-b5b1-6ddc48827296" />

Main Goal - produce a clean GDSII with no human intervention (no-human in the loop)
Clean means - No LVS violations
            - No DRS violations
            - Timing violations
- Tuned for skywater 130nm Open PDK
  - also supports XFAB180 and GF130G
- Containerized
  - Functional out of the box
  - Instructions to build and run natively will follow
- Can be used to harden macros and chips
- Two modes of operation
  - Autonomous or Interactive
- Design space exploration
  - Find the best set of flow configuration
- Large number of design examples
  - 43 designs with their best configurations

## Introduction to OpenLANE detailed ASIC Design Flow
 
<img width="2380" height="1325" alt="Screenshot 2025-10-28 002400" src="https://github.com/user-attachments/assets/7f6a4823-eafb-4d95-970f-0c432f068298" />

OpenLane Regression Testing
The design exploration utility is also used for regression testing.
We run OpenLane on ~70 designs and compare the results to the best known ones.

DESIGN FOR TEST (DFT)
- Scan Insertion
- Automatic Test Pattern Generation (ATPG)
- Test Patterns Compaction
- Fault Coverage 
- Fault Simulation

<img width="947" height="649" alt="Screenshot 2025-10-28 012011" src="https://github.com/user-attachments/assets/8067d2dd-03f4-4cb1-8bb2-62fffe8bf08f" />

PHYSICAL IMPLEMENTATION
Also called automated PnR (Place and Route)
- Floor/Power Planning
- End Decoupling capacitors and Tap cells insertion
- Placement
- Post Placement optimization
- Clock Tree Synthesis (CTS)

<img width="864" height="602" alt="Screenshot 2025-10-28 012958" src="https://github.com/user-attachments/assets/d01bb028-2826-4040-a0b1-274c8e040a03" />

Dealing with Antenna Rules Violations
- When a metal wire segment is fabricated, it can act as an antenna.
  - Reactive ion etching causes charge to a accumulate on the wire.
  - Transistor gates can be damaged during fabrication.

<img width="1073" height="476" alt="Screenshot 2025-10-28 013130" src="https://github.com/user-attachments/assets/7c0ca792-3cf0-4ca6-b43b-d62b51d04bcd" />

- Two solutions
  - Bridging attaches a higher layer immediately.
    - requires router awareness.
  - Add antenna diode cell to leak away charges.
    - antenna diodes are provided by the SCL.
   
<img width="1600" height="449" alt="Screenshot 2025-10-28 013300" src="https://github.com/user-attachments/assets/b779c49c-b2bc-463e-836a-a41d0e9b48f1" />

- We took a prevention approach
  - Add a fake antenna diode next to every cell input after placement.
  - Run the antenna checker (Magic) on the routed layout.
  - If the checker reports a violation on the cell input pin, replace the fake diode cell by a real one.
 
PHYSICAL VERIFICATION DRC & LVS
- Magic is used for design rules checking and SPICE extraction from layout.
- Magic and Netgen are used for LVS.
  - extracted SPICE by MAGIC vs Verilog Netlist.

<img width="628" height="583" alt="Screenshot 2025-10-28 013742" src="https://github.com/user-attachments/assets/b147d3a2-c4c0-45f6-9a81-92db554d3995" />

## LAB-01 Familiarize with OpenLANE flow

In order to access the OpenLane tool, we will be needing some basic linux commands.They are listed below

- ls – List files and directories
- pwd – Show the current directory path
- cd – Change directory
- mkdir – Create a new directory
- rmdir – Remove an empty directory
- rm – Remove files or directories
- cp – Copy files or directories
- mv – Move or rename file

Using a sample design included with OpenLANE, the goals are:
- To understand the OpenLANE directory structure and the purpose of different input files
- To get familiar with how the OpenLANE flow works
- To observe and study the results produced at each stage of the flow
- To learn about the various settings, options, and parameters that can be adjusted to explore different design possibilities

## Design Preparation Step
To work inside the OpenLane environment, you first need to start a Bash shell using Docker while being in the OpenLane directory. The Docker command launches a container that provides the proper environment for running OpenLane tools.
Once you are inside the container’s Bash shell, the next step is to run the flow.tcl script. This script defines the entire OpenLane flow and manages all stages from RTL to GDSII. If you want to run the flow step-by-step and have control over each stage, you must use the -interactive option. Without this option, the script will automatically run the complete flow in one go and directly produce the final results.

1. To invoke OpenLANE, cd to the home directory of OpenLANE and run docker:
```
docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21
```

2. The entry point for OpenLANE is the ./flow.tcl script. This script is used to run the flow, start interactive sessions, select the configuration and create OpenLane design files.

- To run the automated flow for a design:
```
./flow.tcl -design <design_name>
```

- To start an interactive session:
```
./flow.tcl -interactive
```

<img width="1818" height="1003" alt="Screenshot 2025-11-15 235001" src="https://github.com/user-attachments/assets/fcbca7bd-59cb-450f-a84d-1edf4c48476a" />

3. We will be using the interactive mode to learn about the different steps in the flow.

The commands to start an interactive session and run the synthesis of the picorv32a example design are given below:
```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```

## Synthesis Result

<img width="1819" height="978" alt="Screenshot 2025-11-15 235450" src="https://github.com/user-attachments/assets/866c1613-dc0b-4ee3-89e2-d2222824727f" />

## Synthesis Statistics

![Web_Photo_Editor (10)](https://github.com/user-attachments/assets/da5680f9-3d7f-4b99-ac37-6ac8fe3daf01)

Flop Ratio Calculation:
```
Flop Ratio = (Total no. of Flops/ Total no. of cells in the design)
           = 1613/ 14876
           = 0.108429685 (OR) 10.8429 %
```







  









