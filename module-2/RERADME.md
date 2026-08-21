# 🛠️ Module 2 — Timing Libraries, Synthesis Methods & Flip-Flop RTL

## 🎯 Objectives

This module focuses on understanding timing libraries, the SKY130 PDK, different synthesis approaches, and RTL coding styles for D flip-flops.

The main activities covered in this module are:

- Understanding the SKY130 timing library
- Examining `.lib` files and operating conditions
- Comparing hierarchical and flattened synthesis
- Implementing different D flip-flop coding styles
- Simulating RTL designs using Icarus Verilog
- Viewing waveforms using GTKWave
- Synthesizing RTL designs using Yosys
- Mapping the synthesized design to SKY130 standard cells


## 🔧 Tools and Technologies

- **HDL:** Verilog
- **Simulator:** Icarus Verilog
- **Waveform Viewer:** GTKWave
- **Synthesis Tool:** Yosys
- **PDK:** SKY130


## 📚 Table of Contents

1. [Timing Libraries](#1-timing-libraries)
2. [Hierarchical and Flattened Synthesis](#2-hierarchical-and-flattened-synthesis)
3. [Flip-Flop Coding Styles](#3-flip-flop-coding-styles)
4. [RTL Simulation and Synthesis Flow](#4-rtl-simulation-and-synthesis-flow)
5. [Optimization](#5-optimization)
6. [Overall Result](#6-overall-result)
7. [Conclusion](#7-conclusion)


# 1. 📚 Timing Libraries

## 1.1 SKY130 PDK

The SKY130 PDK provides the technology files and standard-cell information required for designing digital circuits using 130 nm CMOS technology.

For this module, the following timing library was used:

```bash
sky130_fd_sc_hd__tt_025C_1v80.lib
```

## 1.2 🔍 Timing Library Operating Conditions

The timing library name provides information about the process corner, operating temperature, and supply voltage used for cell characterization.

The selected library is:

```bash
sky130_fd_sc_hd__tt_025C_1v80.lib
```

## 1.3 📂 Examining the `.lib` File

The Liberty (`.lib`) file contains detailed information about the standard cells available in the selected technology library.

It provides important data such as:

- Cell definitions
- Input and output pins
- Timing information
- Power characteristics
- Operating conditions
- Functional behavior

The file was inspected to understand how standard-cell information is represented and used during the synthesis process.

> 🖼️ **Figure:** SKY130 `.lib` file contents

### Result

The Liberty file was successfully examined, and the available standard-cell and characterization information was studied.

# 2. 🏗️ Hierarchical and Flattened Synthesis

Synthesis converts the RTL description into a gate-level hardware representation. In this module, both hierarchical and flattened synthesis approaches were studied to understand how the design structure changes during synthesis.

## 2.1 📁 Hierarchical Synthesis

Hierarchical synthesis keeps the original module structure of the RTL design.

The individual modules remain separate, making it easier to identify the relationship between different blocks and debug the synthesized design.

### Result

The design was synthesized while preserving the module hierarchy and the connections between the submodules.

> 🖼️ **Figure:** Hierarchical synthesis result

## 2.2 🌐 Flattened Synthesis

Flattened synthesis removes the individual module boundaries and combines the complete RTL design into a single representation.

This allows the synthesis tool to analyze and optimize logic across different modules instead of treating each module separately.

The following command is used in Yosys to flatten the design:

```bash
flatten
```
## 2.3 ⚖️ Comparison of Synthesis Methods

Hierarchical and flattened synthesis differ mainly in how the original RTL module structure is handled during the synthesis process.

- **Hierarchical synthesis** preserves the individual modules and their boundaries.
- **Flattened synthesis** combines the modules into one unified design.
- Hierarchical designs are generally easier to trace and debug.
- Flattened designs provide more scope for optimization across module boundaries.

### Result

Both approaches were studied to understand the effect of module hierarchy on synthesis, optimization, and design representation.

# 3. 🔄 Flip-Flop Coding Styles

Flip-flops are sequential logic elements used to store binary data. In this section, different D flip-flop implementations are developed and verified using Verilog HDL.

The following coding styles are covered:

- Asynchronous Reset D Flip-Flop
- Asynchronous Set D Flip-Flop
- Synchronous Reset D Flip-Flop

## 3.1 🔴 Asynchronous Reset D Flip-Flop

An asynchronous reset allows the flip-flop output to be cleared immediately when the reset signal is activated, without waiting for a clock transition.

### Verilog Code

```verilog
module dff_asyncres (
    input clk,
    input async_reset,
    input d,
    output reg q
);

always @(posedge clk, posedge async_reset)
    if (async_reset)
        q <= 1'b0;
    else
        q <= d;

endmodule
```
### Working
When async_reset is high, the output q is immediately driven to 0.
When the reset is inactive, the input d is captured at the rising edge of the clock.
### Simulation Commands
```bash
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```

### Result
The asynchronous-reset D flip-flop was successfully simulated, and the waveform was verified using GTKWave.

## 3.2 🟢 Asynchronous Set D Flip-Flop

An asynchronous set forces the flip-flop output to logic `1` immediately when the set signal is asserted, independent of the clock.

### Verilog Code

```verilog
module dff_async_set (
    input clk,
    input async_set,
    input d,
    output reg q
);

always @(posedge clk, posedge async_set)
    if (async_set)
        q <= 1'b1;
    else
        q <= d;

endmodule
```
### Working
When async_set is high, the output q is immediately set to 1.
When the set signal is inactive, the input d is transferred to q at the rising edge of the clock.
### Simulation Commands
```bash
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```

### Result
The asynchronous-set D flip-flop was successfully simulated, and its expected behavior was confirmed through the generated waveform.
