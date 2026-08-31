# August 23 Class Work

## Introduction

This section presents the RTL design, synthesis, netlist generation, and post-synthesis verification activities performed during the August 23 class. The practical work focused on the BabySoC design, Yosys synthesis, SKY130 standard-cell libraries, synthesized netlist visualization, and post-synthesis simulation.

## Objectives

- To understand the BabySoC RTL design flow.
- To read and analyze Verilog RTL source files using Yosys.
- To understand the use of SKY130 standard-cell libraries.
- To perform RTL synthesis using Yosys.
- To generate and analyze the synthesized netlist.
- To visualize the synthesized BabySoC design.
- To understand cell and wire optimization.
- To perform post-synthesis simulation.
- To analyze post-synthesis waveforms using GTKWave.

## Tools and Technologies

- Verilog HDL
- Yosys Open Synthesis Suite
- ABC
- SKY130 Standard Cell Library
- Icarus Verilog
- GTKWave
- Linux / VSDSquadron Virtual Machine

---

## 1. BabySoC Design and Yosys

### Description

BabySoC is a small System-on-Chip design used to understand the RTL-to-netlist design flow. During the class, the BabySoC Verilog design was read and processed using Yosys.

Yosys was used to parse the RTL source code and generate an internal representation of the design.

### Commands

The RTL design was read using the Yosys `read_verilog` command.

The `show` command was used to generate a graphical representation of the design.

### Output

![BabySoC Yosys](babysoc.png)

### Result

The BabySoC RTL design was successfully loaded into Yosys and its design representation was generated.

---

## 2. BabySoC Design Visualization

### Description

After reading the BabySoC RTL design, Yosys was used to visualize the structure and connections between the different blocks of the design.

### Output

![BabySoC Yosys Design](babysoc%20vsd%20yosys.png)

### Result

The BabySoC design structure was successfully visualized using Yosys.

---

## 3. SKY130 Standard Cell Library and ABC

### Description

Technology mapping converts the synthesized logic into cells available in a target standard-cell library. The SKY130 standard-cell library provides the required cells for implementing digital logic.

ABC is used during the synthesis flow for logic optimization and technology mapping.

The SKY130 Liberty library was used to provide cell information during the synthesis process.

### Output

![ABC Liberty SKY130 Command](cells%20abc%20liberty%20sky130%20lib%20command.png)

### Result

The SKY130 standard-cell library and Liberty information were successfully used as part of the synthesis and technology-mapping flow.

---

## 4. Synthesis of BabySoC

### Description

Synthesis converts the RTL description into a gate-level representation through logic optimization and technology mapping.

During the class, the BabySoC RTL design was synthesized using Yosys and mapped to cells from the SKY130 standard-cell library.

### Output

![Synthesis](synthesis.png)

### Result

The BabySoC RTL design was successfully synthesized into a gate-level representation.

---

## 5. Synthesized BabySoC Netlist Visualization

### Description

After synthesis, the resulting design is represented as a netlist containing cells and their interconnections. The Yosys `show` command was used to visualize the synthesized BabySoC netlist.

### Output

![Synthesized BabySoC](show%20vsdbabysoc.png)

### Result

The synthesized BabySoC netlist was successfully generated and visualized.

---

## 6. Netlist Optimization

### Description

During synthesis and optimization, unnecessary logic elements and connections can be removed while preserving the functionality of the design. This helps reduce redundant hardware and produces an optimized implementation.

Yosys statistics were observed after the optimization process to understand the resulting wires, cells, and other design elements.

### Output

![After Removing Cells and Wires](after%20removing%20cells%20wires.png)

### Result

The optimized design statistics were successfully observed after removing unnecessary cells and wires.

---

## 7. Post-Synthesis Simulation

### Description

Post-synthesis simulation is used to verify the functional behavior of the synthesized design. The synthesized netlist is simulated using a testbench and the resulting signal activity is observed.

During the class, the synthesized BabySoC design was simulated and the generated VCD file was opened using GTKWave.

### Waveform Analysis

The post-synthesis waveform was observed to verify important signals such as clock, reset, output, and other design signals.

### Output

![Post Synthesis Simulation](post%20synth.png)

### Result

The post-synthesis simulation was successfully performed and the generated waveform was observed using GTKWave.

---

## Overall Result

The August 23 class provided practical experience with the BabySoC RTL-to-netlist flow. The BabySoC RTL design was processed using Yosys, the SKY130 standard-cell library was used for technology mapping, and the synthesized netlist was generated and visualized. Design optimization and post-synthesis simulation were also performed, followed by waveform analysis using GTKWave.

## Conclusion

The complete synthesis and verification flow of the BabySoC design was practiced during the August 23 class. The activities helped in understanding how RTL Verilog is processed through synthesis, technology mapping, netlist generation, optimization, and post-synthesis simulation using open-source VLSI tools.
