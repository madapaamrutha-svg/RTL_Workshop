# August 22 Class Work

## Introduction

This section documents the RTL design and verification activities performed during the class on August 22. The work includes designing and understanding multiple Verilog modules, using case statements for combinational logic, synthesizing the designs using Yosys, generating netlists, performing RTL simulation, and analyzing waveforms using GTKWave.

## Objectives

- To understand the structure of Verilog RTL designs.
- To work with multiple Verilog modules and module instantiation.
- To understand combinational logic using case statements.
- To synthesize RTL designs using Yosys.
- To visualize the synthesized design and netlist.
- To perform RTL simulation using Icarus Verilog.
- To generate VCD waveform files.
- To analyze simulation waveforms using GTKWave.

## Tools and Technologies

- Verilog HDL
- Icarus Verilog
- Yosys
- GTKWave
- Linux / VSDSquadron Virtual Machine
- Git and GitHub

## Table of Contents

1. [Multiple Module Design](#1-multiple-module-design)
2. [Multiple Module Netlist](#2-multiple-module-netlist)
3. [Combinational Logic using Case Statement](#3-combinational-logic-using-case-statement)
4. [RTL Simulation](#4-rtl-simulation)
5. [Waveform Generation and Analysis](#5-waveform-generation-and-analysis)
6. [Git and RTL Workshop Repository](#6-git-and-rtl-workshop-repository)
7. [Overall Result](#overall-result)
8. [Conclusion](#conclusion)

---

## 1. Multiple Module Design

### Description

A Verilog design can be divided into multiple modules, where each module performs a specific function. These modules can be instantiated and connected together to form a larger hierarchical design.

During the class, a multiple-module RTL design was created and synthesized. The design structure was viewed using Yosys to understand the relationship between the different modules.

### Synthesis and Visualization

Yosys was used to read the Verilog source files, perform synthesis, and generate a graphical representation of the design.

### Output

The synthesized multiple-module design was successfully visualized using the Yosys `show` command.

<img width="1920" height="940" alt="multple modules" src="https://github.com/user-attachments/assets/45842274-d883-4f0a-b8d9-0266b22b2996" />




### Result

The hierarchical structure and connections between multiple Verilog modules were successfully verified.

---

## 2. Multiple Module Netlist

### Description

After synthesis, the RTL design is converted into a gate-level representation called a netlist. The netlist shows the logic elements and their interconnections after synthesis.

The multiple-module design was synthesized and its resulting netlist was observed using Yosys.

### Output

<img width="1920" height="940" alt="mult mod netlist" src="https://github.com/user-attachments/assets/e72f7b32-909f-4cd8-896b-d53382ee1f56" />



### Result

The synthesized netlist of the multiple-module design was successfully generated and analyzed.

---

## 3. Combinational Logic using Case Statement

### Description

The Verilog `case` statement is commonly used to describe combinational logic when the output depends on different input conditions. It provides a clear way to represent selection logic and multiplexer-type circuits.

A combinational design using a case statement was synthesized using Yosys. The synthesized circuit was then visualized to understand the resulting hardware structure.

### Synthesis and Visualization

The design was processed using Yosys and the synthesized representation was viewed using the `show` command.

### Output

<img width="1920" height="940" alt="comp_case" src="https://github.com/user-attachments/assets/f8023819-45d5-4ce0-8e95-71e0b71a67f2" />



### Result

The combinational logic described using the case statement was successfully synthesized and its hardware representation was verified.

---

## 4. RTL Simulation

### Description

RTL simulation is performed to verify the functional behavior of a Verilog design before hardware implementation. A testbench is used to provide input stimulus and observe the corresponding outputs.

The design was compiled and simulated using Icarus Verilog. The simulation generated a VCD file containing the signal transitions.

### Simulation Flow

The general simulation flow followed during the class was:

1. Compile the Verilog design and testbench.
2. Run the simulation.
3. Generate the VCD waveform file.
4. Open the VCD file using GTKWave.
5. Observe and verify the signal transitions.

### Output

<img width="1920" height="940" alt="simulation" src="https://github.com/user-attachments/assets/d999f753-81d9-494d-8ede-410d8921899c" />



### Result

The RTL design was successfully simulated and the generated signals were observed for functional verification.

---

## 5. Waveform Generation and Analysis

### Description

Waveform analysis helps verify the behavior of a digital design by displaying the changes in signals with respect to simulation time.

GTKWave was used to open the generated VCD file and observe signals such as clock, reset, inputs, and outputs.

### Commands

The simulation and waveform analysis involved commands such as:

```bash
iverilog
vvp
gtkwave
```

### Output

<img width="1920" height="940" alt="VirtualBox_vsdworkshop_22_08_2026_12_25_00" src="https://github.com/user-attachments/assets/9369ba5e-2db4-4bff-8d04-96ebd2cdf107" />


### Result

The generated waveform was successfully opened in GTKWave and the signal transitions were analyzed.

---

## 6. Git and RTL Workshop Repository

### Description

Git and GitHub were used to organize and maintain the RTL design work. The designs, simulation files, and related outputs were maintained in the RTL Workshop repository.

The class work was organized systematically so that the RTL designs and verification results could be tracked and documented.

### Result

The RTL workshop work was successfully organized and maintained using Git and GitHub.

---

## Overall Result

The August 22 class provided practical experience in RTL design, multiple Verilog modules, combinational logic using case statements, Yosys synthesis, netlist visualization, RTL simulation, and waveform analysis using GTKWave.

## Conclusion

The complete RTL design and verification flow was practiced, starting from Verilog RTL design and continuing through synthesis, netlist visualization, simulation, and waveform analysis. The practical exercises helped in understanding the relationship between RTL code, synthesized hardware, and simulation results.
