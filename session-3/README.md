# Session 3 – MUX and BabySoC Synthesis and Verification

## Overview

Session 3 was about synthesizing and verifying digital designs with open-source EDA tools. It had two parts:

1. Multiplexer (`good_mux`) synthesis and verification
2. BabySoC (`vsdbabysoc`) synthesis and verification

Yosys was used for synthesis, Graphviz for visualizing circuits, and GTKWave for waveform analysis.

Together, these steps showed how RTL code is converted into a technology-specific gate-level implementation, and how the synthesized design is checked through simulation.

---

# Part 1 – MUX Design

## 1. MUX RTL Simulation

The first screenshot is the RTL simulation waveform of the `good_mux` design.

A multiplexer is a combinational circuit that picks one of several inputs based on a select signal. `good_mux` has two inputs, `i0` and `i1`, a select signal `sel`, and an output `y`. When `sel` changes, the matching input is passed to the output.

The waveform was viewed in GTKWave, which shows signal transitions against time.

### Key Takeaways

- How a multiplexer works.
- The relationship between inputs, select and output.
- How to simulate an RTL design.
- How to observe digital signals in GTKWave.

<img width="961" height="529" alt="image" src="https://github.com/user-attachments/assets/7795d0b6-9a52-4f15-9049-6ad0c9da72da?raw=true" />

---

# 2. MUX Synthesized Representation

The second screenshot shows the synthesized `good_mux`.

After synthesis, the RTL multiplexer is turned into a hardware structure built from cells of the target standard-cell library. The inputs `i0` and `i1` and the select `sel` connect to the synthesized multiplexer cell, which drives the output `y`.

This shows how a simple RTL description becomes a technology-specific hardware implementation.

### Key Takeaways

- How RTL logic is converted into hardware cells.
- How technology mapping is carried out.
- How a synthesized design can be shown graphically.

<img width="949" height="534" alt="image" src="https://github.com/user-attachments/assets/6ea1b552-f68f-47b9-9d44-5c9b6046394c?raw=true" />

---

# 3. MUX Netlist and Simulation Flow

The third screenshot shows the terminal commands and flow used to simulate the `good_mux` netlist.

The synthesized netlist is the input to gate-level simulation. Because that netlist contains technology-specific standard-cell instances, the technology library is needed as well.

This step links synthesis with post-synthesis verification.

### Key Takeaways

- Working with synthesized netlists.
- Running gate-level simulation.
- Using technology libraries during simulation.
- How synthesis and simulation fit together in the design flow.

<img width="948" height="535" alt="image" src="https://github.com/user-attachments/assets/f9ed4477-ddc7-4c06-a9ac-744b48ed8d19?raw=true" />

---

# 4. MUX Gate-Level Waveform

The fourth screenshot is the waveform from gate-level simulation of the synthesized MUX.

The inputs and select signal change over time, and the output follows the selected input. GTKWave was used to check that the synthesized circuit behaves as expected.

### Key Takeaways

Gate-level simulation confirms that the synthesized implementation keeps the functionality of the original RTL.

<img width="956" height="540" alt="image" src="https://github.com/user-attachments/assets/8f023685-52b5-4e56-8c89-29b09f19415e?raw=true" />

---

# 5. Detailed MUX Waveform Verification

The fifth screenshot is a closer look at the MUX waveform.

Comparing the inputs, the select signal and the output over time verifies the operation of the multiplexer, and confirms how the select signal decides the output.

### Key Takeaways

- Analysing individual signal transitions.
- Verifying combinational logic with waveforms.
- Using GTKWave for debugging.
- Verifying the synthesized MUX.

---

# Part 2 – BabySoC Design

## 6. BabySoC Block Diagram

After the MUX example, we moved on to a larger SoC-level design, `vsdbabysoc`.

BabySoC consists of several functional blocks, including the RISC-V core, clock and reset logic, and PLL-related circuitry. The block diagram gives a high-level picture of the architecture and how the main blocks connect, which makes a complex design easier to understand before looking at its gate-level detail.

### Key Takeaways

- How an SoC is divided into functional blocks.
- How the hardware blocks communicate.
- How block diagrams represent complex digital systems.
- How the RISC-V core connects with the supporting blocks.

---

# 7. BabySoC Synthesis and Optimization

This screenshot shows Yosys synthesizing and optimizing the BabySoC design.

Yosys reads the Verilog RTL and converts it into an internal form that can be optimized and mapped to hardware cells. Its optimization passes remove unnecessary logic and simplify the design.

Examples of optimizations:

- Constant propagation
- Removal of unused logic
- Multiplexer optimization
- Flip-flop optimization
- Removal of unused wires and cells

### Key Takeaways

- How Yosys performs RTL synthesis.
- Why optimization is needed.
- How redundant logic gets removed.
- How synthesis improves the hardware implementation.

<img width="709" height="513" alt="image" src="https://github.com/user-attachments/assets/dea5d254-ee3b-49cb-a544-e6ef9fbaf288?raw=true" />

<img width="1919" height="1028" alt="Screenshot 2026-08-23 134319" src="https://github.com/user-attachments/assets/4c8c7f40-a9d6-4b95-ba43-0162297eacce?raw=true" />

---

# 8. BabySoC Synthesis Statistics

This screenshot shows the design statistics reported by Yosys, which describe the size and complexity of the synthesized design.

They include:

- Number of wires
- Number of wire bits
- Number of public wires
- Number of ports
- Number of cells
- Number of processes
- Number of memories
- Number of sequential elements

These numbers give a quantitative view of the hardware generated from the RTL.

### Key Takeaways

Design statistics show how complex a synthesized circuit is, and can be used to compare different synthesis results.

<img width="289" height="536" alt="image" src="https://github.com/user-attachments/assets/35361a94-8788-43f9-af42-d50f4823c575?raw=true" />

---

# 9. BabySoC Graphviz Representation

This screenshot is a large Graphviz view of the BabySoC design.

Graphviz draws the synthesized circuit as a graph: each block or cell is a node, and the lines between them are signal connections. Since BabySoC is far bigger than the MUX example, the graph has a very large number of connections.

### Key Takeaways

- How to visualize a synthesized circuit.
- How Graphviz shows hardware connectivity.
- How large designs contain many internal connections.
- How graphical views help in understanding netlists.

<img width="413" height="445" alt="image" src="https://github.com/user-attachments/assets/a8ca1edf-18e8-474b-920c-de17dbc06138?raw=true" />

---

# 10. BabySoC Cell Statistics

This screenshot lists the cells used in the synthesized BabySoC.

During technology mapping, generic logic is replaced by standard cells from the chosen library. The design can contain cell types such as:

- AND gates
- OR gates
- NAND gates
- NOR gates
- Multiplexers
- Buffers
- Flip-flops
- Other standard logic cells

The statistics show how the original RTL functionality is realised with actual hardware cells.

### Key Takeaways

Technology mapping ties the synthesized RTL to a specific semiconductor technology and its standard-cell library.

<img width="1040" height="535" alt="image" src="https://github.com/user-attachments/assets/5ead077f-0090-41ba-b7bd-23c7ab044fbd?raw=true" />

---

# 11. Generated Gate-Level Verilog Netlist

This screenshot shows the gate-level Verilog netlist generated for BabySoC.

After synthesis and technology mapping, the RTL becomes a lower-level description made of technology-specific standard-cell instances, wired together by internal nets to implement the BabySoC functionality.

### Key Takeaways

- How RTL is converted into gate-level Verilog.
- How standard-cell instances look in a netlist.
- How cells are connected through nets.
- How the synthesized design differs from the original RTL.

<img width="1065" height="531" alt="image" src="https://github.com/user-attachments/assets/94ef0294-883f-4e8c-b662-96f8bf006402?raw=true" />

---

# 12. BabySoC Synthesized Circuit Representation

This part shows the graphical representation of the synthesized BabySoC circuit.

The diagram has many hardware blocks and their interconnections, giving a lower-level view of how the SoC components are connected after synthesis. It makes the structure and signal flow easier to follow.

### Key Takeaways

- How synthesized hardware can be shown graphically.
- How the different cells are interconnected.
- How the RTL structure changes after synthesis.

---

# 13. BabySoC Simulation Waveform

This screenshot is the BabySoC simulation waveform in GTKWave.

It contains key signals such as the clock, reset and other internal or output signals. The clock is the timing reference for the sequential elements, while the other signals change according to the operation of the SoC blocks. GTKWave lets us watch them over time and verify the behaviour of the design.

### Key Takeaways

- Analysing SoC-level waveforms.
- How clock signals drive sequential circuits.
- How reset affects the design.
- Using GTKWave for hardware verification.

<img width="1919" height="1029" alt="Screenshot 2026-08-22 152416" src="https://github.com/user-attachments/assets/e5d38b3c-9f12-4a8a-969b-9365ff67b877?raw=true" />

<img width="1584" height="744" alt="image" src="https://github.com/user-attachments/assets/107173e1-a452-4ef7-8f33-2c5213f8d346?raw=true" />

---

# 14. Final BabySoC Waveform Analysis

The last screenshot is a detailed waveform with many internal BabySoC signals, showing the internal activity of the synthesized SoC.

By watching the clock, reset and internal signals, we can see how the different parts of the design behave over time. This is an important step in confirming that the synthesized implementation works as expected.

### Key Takeaways

- Analysing many digital signals together.
- Observing internal signal transitions.
- How clock and reset influence sequential logic.
- Using GTKWave for final verification.
- Verifying the synthesized SoC design.

<img width="1584" height="744" alt="image" src="https://github.com/user-attachments/assets/063abe4a-ab2c-42f3-9e11-ded267165ea1?raw=true" />

---

# Overall Session 3 Flow

```text
MUX RTL Design
      ↓
RTL Simulation
      ↓
MUX Synthesis
      ↓
Technology Mapping
      ↓
Gate-Level Simulation
      ↓
GTKWave Verification
      ↓
BabySoC RTL Design
      ↓
Yosys Synthesis
      ↓
Optimization
      ↓
Technology Mapping
      ↓
Standard-Cell Netlist
      ↓
Design Statistics
      ↓
Graphviz Visualization
      ↓
Gate-Level Simulation
      ↓
GTKWave Waveform Analysis
      ↓
Final Verification
```

## 👤 Author

**Amrutha Madapa**  
B.Tech – Electronics & Communication Engineering  
Anurag University  
[RTL Workshop Repository](https://github.com/madapaamrutha-svg/RTL_Workshop)

