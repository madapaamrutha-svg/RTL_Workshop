# Session 2 – RTL Synthesis, Netlist Generation and Verification

## Overview

Session 2 was about RTL synthesis and verification using open-source EDA tools. The main tool was Yosys, supported by GTKWave and Graphviz.

It showed how a Verilog RTL design is processed, optimized, converted into a gate-level netlist, and then verified through simulation.

Steps covered:

1. RTL simulation
2. Synthesis with Yosys
3. Technology mapping
4. Standard-cell library files
5. Netlist generation
6. Graphviz visualization
7. Gate-level simulation
8. Waveform analysis

---

# 1. RTL Simulation Waveform

The first screenshot is the GTKWave waveform of the RTL design. GTKWave is a viewer that shows how digital signals change over time.

The signals displayed are the inputs `i0`, `i1`, `sel` and the output `y`. Changing the inputs changes the output, and this can be seen directly in the waveform.

### Key Takeaways

- Viewing RTL simulation waveforms.
- Seeing how inputs and outputs vary with time.
- Using waveforms to verify RTL functionality.
- Using GTKWave for debugging digital designs.

### Screenshot

<img width="933" height="592" alt="image" src="https://github.com/user-attachments/assets/6d8afbcc-4970-4b66-ad5c-31802dc7a21e?raw=true" />

---

# 2. Standard Cell Library – Liberty File

This screenshot shows part of a Liberty (`.lib`) standard-cell library file. Synthesis tools use it during technology mapping.

A Liberty file holds details such as:

- Cell characteristics
- Input and output pins
- Timing information
- Capacitance
- Power information
- Leakage power
- Operating conditions

The visible portion has `leakage_power()` entries for different logic conditions.

### Key Takeaways

The library gives the synthesis tool the information it needs to map RTL logic onto real, technology-specific cells.

### Screenshot

<img width="407" height="619" alt="image" src="https://github.com/user-attachments/assets/db2596cc-0c8d-455e-b217-40cec6a23ee9?raw=true" />

---

# 3. Yosys Synthesis and Optimization

This screenshot shows Yosys running in the terminal. Yosys is an open-source tool that converts RTL into a gate-level representation.

While synthesizing, it runs several optimization passes, including:

- OPT
- FSM optimization
- Memory optimization
- DFF optimization
- CLEAN
- Design hierarchy analysis
- Statistics generation
- CHECK

These passes simplify the design and strip out logic that is not needed.

### Key Takeaways

- How Yosys processes RTL code.
- How optimization works during synthesis.
- How unused cells and wires get removed.
- How Yosys reports design statistics.

### Screenshot

<img width="344" height="613" alt="image" src="https://github.com/user-attachments/assets/71eb1ba4-3e88-4fd9-983a-6a7838d95e03?raw=true" />

---

# 4. Loading the Standard Cell Library

Here the standard-cell library is being read as part of the synthesis flow. It contains the technology-specific data required to map generic logic onto physical standard cells.

It includes cells such as:

- Multiplexers
- Logic gates
- Flip-flops
- Buffers
- Other digital building blocks

Timing and power data for these cells is included as well.

### Key Takeaways

A synthesis tool needs a technology library so it knows which standard cells exist and what their characteristics are.

### Screenshot

<img width="1119" height="597" alt="image" src="https://github.com/user-attachments/assets/126ee03e-7d99-4361-8561-5d421dfab078?raw=true" />

---

# 5. Technology Mapping of a Multiplexer

This screenshot shows the synthesized `good_mux` design. The RTL multiplexer has inputs `i0` and `i1`, a select signal `sel`, and output `y`.

After synthesis, it is mapped to a technology-specific standard cell, and the diagram shows the inputs connected to that mapped multiplexer cell.

### Key Takeaways

RTL does not stay as high-level Verilog after synthesis; it becomes technology-specific standard cells.

### Screenshot

<img width="635" height="491" alt="image" src="https://github.com/user-attachments/assets/4b7e10ca-3deb-4a87-a7e8-d2ff34b9b336?raw=true" />

---

# 6. Synthesized Counter Representation

This screenshot shows the synthesized `good_counter` design. It combines sequential elements (flip-flops) with combinational logic.

The counter uses a clock and a reset, and its logic controls the counter state. After synthesis, the RTL is expressed as flip-flops and logic cells from the standard-cell library.

### Key Takeaways

- How sequential RTL becomes hardware.
- How flip-flops appear after synthesis.
- How combinational logic links to sequential elements.
- How a counter is built from hardware cells.

### Screenshot

<img width="937" height="539" alt="image" src="https://github.com/user-attachments/assets/f316ef4b-55cc-42e3-85e5-93ea26cdee0c?raw=true" />

---

# 7. Detailed Synthesized Counter Netlist

This is a second view of the synthesized `good_counter`. It shows how flip-flops, logic gates, multiplexers and other standard cells are interconnected.

Such a representation is called a gate-level netlist. A netlist describes how the individual hardware cells are wired together to form the complete circuit.

### Key Takeaways

The gate-level netlist gives a lower-level look at the hardware generated from the RTL.

### Screenshot

<img width="1062" height="557" alt="image" src="https://github.com/user-attachments/assets/7d7ea202-7620-4e8e-8871-d0979e5ef65c?raw=true" />

---

## 8. Multiple-Module Design

The design was split into several Verilog modules, where one module does a specific job and its output feeds another module.

This is hierarchical RTL design: complex designs are built from smaller, reusable modules.

<img width="1050" height="591" alt="image" src="https://github.com/user-attachments/assets/90c330be-5d2f-4899-9bea-b6663da0ddbb?raw=true" />

---

## 9. Synthesized Multiple-Module Design

After synthesis, the multi-module RTL design is shown as hardware cells and their interconnections. The diagrams show how the individual modules are connected.

<img width="320" height="505" alt="image" src="https://github.com/user-attachments/assets/4dc9f752-bbcc-4b4d-a433-d79f4592bb1f?raw=true" />

<img width="1051" height="581" alt="image" src="https://github.com/user-attachments/assets/4a29fafa-cccd-4ca0-b124-1e6d45aa966a?raw=true" />

---

## 10. Graphviz Representation

Yosys can also produce a Graphviz view of the synthesized circuit, showing modules, cells and connections graphically.

This makes the structure and signal flow of the circuit much easier to follow.

---

## 11. Pre-Synthesis Simulation

Before synthesis, the RTL was simulated to check its functional behaviour.

The waveform shows how the clock, reset, inputs and outputs change over time. This is the first verification of the RTL before it is turned into a gate-level implementation.

<img width="1059" height="597" alt="image" src="https://github.com/user-attachments/assets/fabf5732-9862-4f13-bb33-64cddca51248?raw=true" />

---

## 12. Detailed Waveform Analysis

The waveform was examined in GTKWave at a finer time scale, which makes the relationship between the clock and the other signals clear.

GTKWave lets us find the exact time a signal changes and check whether the design behaves as expected.

<img width="996" height="600" alt="image" src="https://github.com/user-attachments/assets/e844e72a-ba1f-41d3-a035-34b698cd3c47?raw=true" />

---

## 13. Post-Synthesis / Gate-Level Simulation

The generated gate-level netlist was simulated again after synthesis.

Its waveform can be compared with the RTL simulation waveform to confirm that synthesis preserved the intended functionality of the original design.

<img width="1061" height="595" alt="image" src="https://github.com/user-attachments/assets/0aafe99a-b97b-41af-a531-bfed38c2836a?raw=true" />

---

## 14. Final Waveform Verification

The last GTKWave screenshot shows several internal and output signals changing over time. The clock is the timing reference, and the other signals show the internal state transitions of the synthesized circuit.

Studying these waveforms verifies the functionality of the synthesized design.

### Key Takeaways

- Opening and analysing simulation waveforms.
- Observing clock and signal transitions.
- Verifying RTL behaviour before synthesis.
- Verifying the design again after synthesis.
- Comparing waveforms to confirm functional correctness.

<img width="1065" height="598" alt="image" src="https://github.com/user-attachments/assets/965d06a3-14da-4389-93ee-b02e3b226a19?raw=true" />

---

# Overall Flow

```
RTL Verilog Code
        ↓
RTL Simulation
        ↓
Yosys Synthesis
        ↓
Optimization
        ↓
Technology Mapping
        ↓
Standard Cell Library
        ↓
Gate-Level Netlist
        ↓
Graphviz Visualization
        ↓
Gate-Level Simulation
        ↓
GTKWave Verification
```

---

# Conclusion

In Session 2, I learned how Yosys converts an RTL design into a technology-specific gate-level implementation.

I also covered Liberty standard-cell files, synthesis optimization, technology mapping, gate-level netlists, hierarchical modules, Graphviz visualization and waveform analysis in GTKWave.

Overall, the session gave me a clear picture of the flow from Verilog RTL to synthesized digital hardware and its verification.

