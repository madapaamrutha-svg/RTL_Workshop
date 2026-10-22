# 🚀 RTL Design Workshop

> Complete RTL Design Workshop using Verilog HDL, Simulation, Synthesis, Optimization and Physical Design.

---

# 📖 Overview

This repository contains all the modules completed during the RTL Design Workshop. It demonstrates the complete RTL design flow using Verilog HDL, simulation, synthesis, timing analysis, optimization techniques, and the physical design flow. The workshop ends with a final project, the **Digital Equipment Status and Fault Indicator**, which is taken from RTL to a final GDS layout.

---

# 🎥 Training Video

A 3 minute 50 second video explaining my RTL training experience:

[▶ Watch / Download the RTL Training Video](https://github.com/madapaamrutha-svg/RTL_Workshop/blob/main/RTL_Training_Video.mp4)

---

# 🏆 Final Project

### [Digital Equipment Status and Fault Indicator Using Verilog HDL](Equipment-Status-Fault-Indicator/README.md)

A compact synthesizable digital circuit that monitors an equipment fault signal, confirms a fault only if it persists for a set number of clock cycles, latches it, and shows normal, warning, and fault states on three LEDs until the operator acknowledges it.

| Stage | Result |
|-------|--------|
| Simulation | All 18 self-checks passed |
| Synthesis | Yosys (SKY130) |
| Physical design | OpenLane: floorplan, placement, CTS, routing |
| DRC | 0 violations |
| LVS | Match |
| Antenna | 0 violations |
| WNS / TNS | 0.00 / 0.00 |
| Final output | GDS layout |
| Extra check | ngspice (tphl, tplh) |

👉 Full documentation with commands and screenshots: [Equipment-Status-Fault-Indicator](Equipment-Status-Fault-Indicator/README.md)

---

# 🎯 Objectives

- Learn Verilog HDL
- Design RTL circuits
- Perform simulation
- Analyze waveforms
- Perform logic synthesis
- Understand timing analysis
- Optimize digital circuits
- Understand the physical design flow
- Take a design from RTL to GDS with DRC, LVS, and timing signoff

---

# 🛠 Tools and Technologies Used

| Tool | Purpose |
|------|---------|
| Verilog HDL | RTL Design |
| Icarus Verilog | Simulation |
| GTKWave | Waveform Viewer |
| Yosys | Logic Synthesis |
| SKY130 PDK | 130nm Process Design Kit / Standard Cell Library |
| sky130_fd_sc_hd | High-density standard-cell library |
| Ubuntu Linux | Development Environment |
| Git & GitHub | Version Control |
| OpenLane | RTL-to-GDSII ASIC design flow |
| OpenROAD | Physical Design implementation |
| OpenSTA | Static timing analysis |
| LEF Files | Physical abstraction of standard cells, pins and layers |
| Tcl | Configuration of OpenLane flow |
| SDC | Timing and Clock Constraint Definition |
| Magic | Layout viewing and DRC |
| Netgen | LVS |
| KLayout / Layout Viewer | Visualization and inspection of physical layouts |
| ngspice | Circuit-level simulation of the layout netlist |

---

# 📂 Repository Structure

```
RTL_Workshop/
├── Assesment-1/
├── August-22-Class-Work/
├── August-23-Class-Work/
├── PD-Module-1/
├── PD-Module-2/
├── PD-Module-3/
├── PD-Module-4/
├── PD-Module-5/
├── module-0/
├── module-1/
├── module-2/
├── module-3/
├── module-4/
├── module-5/
├── Equipment-Status-Fault-Indicator/
├── RTL_Training_Video.mp4
└── README.md
```

---

# 📚 Table of Contents

- Module 0 – Workshop Introduction
- Module 1 – Introduction to Verilog RTL Design & Synthesis
- Module 2 – Timing Libraries, Synthesis Methods & Flip-Flop RTL
- Module 3 – Combinational and Sequential Optimization
- Module 4 – Blocking vs Non-Blocking Assignments & Simulation Mismatch
- Module 5 – Optimization in Synthesis
- August 22 Class Work – RTL Design, Yosys Synthesis & GTKWave Simulation
- August 23 Class Work – BabySoC Synthesis, SKY130 Mapping & Post-Synthesis Simulation
- Assessment 1 – Sequence Detector RTL Design, Synthesis, GLS & Verification
- PD Module 1 – Physical Design Flow
- PD Module 2 – Chip Floorplanning and Power Integrity
- PD Module 3 – RTL to Physical Design / CMOS Technology
- PD Module 4 – Timing Analysis, Clock Tree Synthesis & Physical Design
- PD Module 5 – SKY130 Physical Design – Routing, DRC, Parasitic Extraction & TritonRoute
- Final Project – Digital Equipment Status and Fault Indicator (RTL to GDS)

---

# 📘 Modules Covered

## Module 0
Workshop Introduction and Tool Setup.

## Module 1
Verilog Basics, RTL Coding, Simulation and Testbench.

## Module 2
Timing Libraries, SKY130 PDK and Flip-Flops.

## Module 3
Combinational and Sequential Logic Optimization.

## Module 4
Blocking vs Non-Blocking Assignments and Synthesis-Simulation Mismatch.

## Module 5
Optimization Techniques, Multiplexer, Demultiplexer and Ripple Carry Adder.

## August 22 Class Work
RTL Design, Yosys Synthesis & GTKWave Simulation.

## August 23 Class Work
BabySoC Synthesis, SKY130 Mapping & Post-Synthesis Simulation.

## Assessment 1
Sequence Detector RTL Design, Synthesis, GLS & Verification.

## PD Module 1
Physical Design Flow.

## PD Module 2
Chip Floorplanning and Power Integrity.

## PD Module 3
CMOS Inverter Design, Characterization, SKY130A Standard-Cell Layout & 16-Mask CMOS Fabrication

## PD Module 4
Timing Analysis, Clock Tree Synthesis & Physical Design

## PD Module 5
SKY130 Physical Design – Routing, DRC, Parasitic Extraction & TritonRoute

## Final Project
Digital Equipment Status and Fault Indicator: RTL, simulation, synthesis, STA, OpenLane physical design, GDS and ngspice verification. See [Equipment-Status-Fault-Indicator](Equipment-Status-Fault-Indicator/README.md).

---

# 📊 Overall Results

- Successfully completed all workshop modules.
- Simulated RTL designs using Icarus Verilog.
- Verified outputs using GTKWave.
- Synthesized RTL using Yosys.
- Applied optimization techniques.
- Learned the complete RTL design flow.
- Explored the physical design flow using OpenLane and OpenROAD.
- Completed the final project from RTL to GDS with DRC 0, LVS match, antenna 0, and zero WNS/TNS.

---

# 🎓 Learning Outcomes

- RTL Coding
- Testbench Writing
- Simulation
- Waveform Analysis
- Logic Synthesis
- Timing Analysis
- Optimization
- Physical Design Basics
- DRC and LVS Signoff
- GitHub Documentation

---

# 🚀 Future Scope

- FSM Design
- Pipelining
- Arithmetic Units
- Processor Design
- Complete ASIC Design Flow

---

# ✅ Conclusion

This workshop provided practical experience in Verilog HDL, simulation, synthesis, timing analysis, optimization and physical design. The final project demonstrated the complete journey from a real-world application idea to a verified RTL design and a successfully generated GDS layout. It strengthened my understanding of the complete RTL design flow using open-source EDA tools.

---

# 👩‍💻 Author

**Name:** MADAPA AMRUTHA

**Course:** RTL Design Workshop

**Platform:** VSD-IAT
