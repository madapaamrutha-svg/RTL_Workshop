# Sequence Detector – RTL Design, Synthesis & GLS

## 1. Project Overview

This project implements a digital sequence detector using Verilog HDL.
The design was developed at RTL level and verified through RTL simulation,
synthesis, and Gate-Level Simulation (GLS).

## 2. RTL Simulation

The RTL design was simulated and the input sequence and detected output
were verified using GTKWave.
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/d3eaae16-26af-43f2-af3b-f4a35c6c6c1a" />




## 3. Logic Synthesis

The RTL design was synthesized using Yosys.

### Synthesis Statistics

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/5de59635-78fb-4cd9-8901-4d2232581e10" />


### Synthesized Block Diagram
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/a8157509-57f3-4662-b8e2-20061c895942" />



## 4. Gate-Level Simulation

The synthesized netlist was used for Gate-Level Simulation (GLS).

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/318a7098-e4a7-4686-9376-725f3c965b2d" />




## 5. RTL vs GLS Comparison

The RTL and GLS waveforms were compared to verify that the synthesized
implementation preserves the functional behavior of the RTL design.



## 6. Conclusion

The sequence detector was successfully designed, simulated, synthesized,
and verified using Gate-Level Simulation. The GLS results confirm that
the synthesized implementation preserves the functional behavior of the
RTL design for the given testbench.

## Overall Result

The Sequence Detector successfully detected the target sequence `1010100` in the given testbench input. RTL simulation produced the expected detection pulses, and the synthesized design was verified using Gate-Level Simulation. The GLS simulation also produced 5 detection events, confirming the expected functional behavior.
