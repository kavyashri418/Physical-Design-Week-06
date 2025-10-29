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
