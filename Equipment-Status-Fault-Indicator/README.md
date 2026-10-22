# Digital Equipment Status and Fault Indicator Using Verilog HDL

A compact synthesizable digital circuit that monitors the status of an equipment unit and shows normal, warning, and fault conditions on three LEDs. The design is taken from RTL through simulation, synthesis, static timing analysis, physical design (OpenLane), and signoff to a final GDS layout, with an ngspice check at the end.

**Author:** MADAPA AMRUTHA
**College:** Your College Name
**Environment:** Ubuntu on VirtualBox, Icarus Verilog, GTKWave, Yosys, OpenSTA, OpenLane (Sky130 PDK), Magic, KLayout, ngspice

---

## Table of Contents

1. Project Overview
2. Inputs and Outputs
3. Sequential Logic Used
4. Tools Used
5. Project Folder Structure
6. Test Cases
7. RTL Design
8. Testbench
9. Simulation
10. Waveform
11. Synthesis
12. Pre-Layout STA
13. Physical Design (OpenLane)
14. Post-Route STA
15. Final Layout (GDS)
16. Signoff Summary
17. Additional Run (Run 3)
18. ngspice Verification
19. Feasibility
20. Conclusion

---

## 1. Project Overview

**Real-world problem:** In machines, motors, power supplies, and control panels, a fault is often a brief glitch that disappears before an operator notices it. Operators also cannot tell a short disturbance from a real, persistent failure. As a result, faults get missed or false alarms get raised.

**Proposed solution:** A small dedicated chip that watches the equipment fault signal, confirms the fault only if it persists for a set number of clock cycles, latches it, and shows the state on LEDs until the operator acknowledges it.

**Users and where it is used:** Technicians and operators of industrial machines, control panels, lab instruments, and embedded systems that need a simple, always-on status display.

**Why dedicated hardware:** The function is small and always-on. A fixed-function circuit responds in a few clock cycles, needs no processor, software, or operating system, uses very little area and power, and cannot hang or crash.

> My project is a **status and fault indicator** that solves **missed or false fault alarms in equipment monitoring** by taking **a clock, reset, equipment fault input, and an operator acknowledge input** as inputs and producing **three LED outputs (normal, warning, fault)** as outputs. It uses **an FSM with a persistence counter** as its main sequential logic.

---

## 2. Inputs and Outputs

| Signal | Direction | Description |
|--------|-----------|-------------|
| clk | Input | System clock |
| rst | Input | Reset, returns the design to the normal state |
| fault | Input | Fault condition from the equipment |
| ack | Input | Operator acknowledge, clears a latched fault |
| led_normal | Output | Equipment is working normally |
| led_warning | Output | Fault detected, not yet confirmed (persistence counting) |
| led_fault | Output | Fault confirmed and latched until acknowledged |

---

## 3. Sequential Logic Used

- **FSM:** NORMAL, WARNING, and FAULT states.
- **Persistence counter (`persist_cnt`):** Counts consecutive clock cycles with the fault present. A fault is confirmed only after the count reaches the threshold, which filters short glitches.
- **State register:** Holds the latched fault until `ack` is received.

---

## 4. Tools Used

| Stage | Tool |
|-------|------|
| Simulation | Icarus Verilog (`iverilog`, `vvp`) |
| Waveform | GTKWave |
| Synthesis | Yosys (inside OpenLane) |
| STA | OpenSTA (inside OpenLane) |
| Physical design | OpenLane (Sky130) |
| Layout viewing / DRC | Magic, KLayout |
| LVS | Netgen |
| Circuit simulation | ngspice |

---

## 5. Project Folder Structure

```
Equipment-Status-Fault-Indicator/
├── README.md
├── rtl/                  # Verilog design
├── tb/                   # Self-checking testbench
├── physical_design/      # config.tcl and run summary reports
├── gds/                  # Final GDS layout
├── ngspice/              # ngspice netlist
└── images/               # Screenshots used in this README
```

---

## 6. Test Cases

1. Reset behaviour: all outputs go to the normal state.
2. Normal operation: no fault, only the normal LED is on.
3. Short glitch: a fault shorter than the threshold is ignored.
4. Persistent fault: the fault is confirmed and the fault LED turns on.
5. Latching: the fault stays latched after the input returns to normal.
6. Acknowledge: `ack` clears the latched fault.
7. Boundary: fault lasting exactly the threshold count, and one cycle less.
8. Reset in the middle of a fault.

---

## 7. RTL Design

File: `rtl/equipment_status_indicator.v`

![RTL code 1](images/1.png)

![RTL code 2](images/2.png)

---

## 8. Testbench

File: `tb/tb_equipment_status_indicator.v`. It is self-checking and prints PASS or FAIL for every check.

![Testbench 3](images/3.png)

![Testbench 4](images/4.png)

![Testbench 5](images/5.png)

![Testbench 6](images/6.png)

---

## 9. Simulation

**Commands:**

```bash
cd ~/RTL_Workshop/Equipment-Status-Fault-Indicator
iverilog -o sim.out rtl/equipment_status_indicator.v tb/tb_equipment_status_indicator.v
vvp sim.out
```

**Result:** All 18 self-checks passed.

![Simulation result](images/34.png)

---

## 10. Waveform

**Command:**

```bash
gtkwave dump.vcd
```

The waveform shows `ack`, `persist_cnt`, and the three LED outputs.

![Waveform](images/35.png)

---

## 11. Synthesis

**Commands (OpenLane, interactive mode):**

```bash
cd ~/Desktop/work/tools/openlane_working_dir/openlane
make mount
./flow.tcl -interactive
```

```tcl
package require openlane 0.9
prep -design equipment_status_indicator -tag run2
run_synthesis
```

The synthesis report shows the cell count and area.

![Synthesis 12](images/12.png)

![Synthesis 13](images/13.png)

![Synthesis 14](images/14.png)

![Synthesis 27](images/27.png)

---

## 12. Pre-Layout STA

**Command (inside the OpenLane shell):**

```tcl
run_sta
```

![Pre-layout STA](images/28.png)

---

## 13. Physical Design (OpenLane)

**Commands (same interactive session):**

```tcl
run_floorplan
run_placement
run_cts
run_routing
```

**Or run the whole flow in one go:**

```bash
./flow.tcl -design equipment_status_indicator -tag run2
```

### 13.1 Floorplan

![Floorplan](images/31.png)

### 13.2 Placement

![Placement](images/30.png)

### 13.3 Clock Tree Synthesis (CTS)

![CTS](images/29.png)

### 13.4 Routing

![Routing](images/32.png)

---

## 14. Post-Route STA

Timing is checked at three corners after routing. Reports are in `runs/run2/reports/`.

![Post-route STA 23](images/23.png)

![Post-route STA 24](images/24.png)

---

## 15. Final Layout (GDS)

The GDS file is in `gds/`.

**Commands:**

```bash
cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/equipment_status_indicator/runs/run2/results/final/gds
magic -T $PDK_ROOT/sky130A/libs.tech/magic/sky130A.tech equipment_status_indicator.gds
```

Or with KLayout:

```bash
klayout equipment_status_indicator.gds
```

![Final layout](images/15.png)

---

## 16. Signoff Summary (Run 2)

**Command:**

```bash
cat runs/run2/reports/final_summary_report.csv
```

The report is saved in `physical_design/run2_final_summary_report.csv`.

![Signoff summary](images/21.png)

| Check | Result |
|-------|--------|
| DRC | 0 violations |
| LVS | Match |
| Antenna | 0 violations |
| WNS | 0.00 |
| TNS | 0.00 |

---

## 17. Additional Run (Run 3)

Reports from Run 3 (LVS, DRC, and report files). Its summary is saved in `physical_design/run3_final_summary_report.csv`.

```bash
ls runs
```

![Run 3 - 16](images/16.png)

![Run 3 - 17](images/17.png)

![Run 3 - 18](images/18.png)

![Run 3 - 19](images/19.png)

![Run 3 - 20](images/20.png)

---

## 18. ngspice Verification

The layout netlist was simulated in ngspice to check input and output switching and the propagation delays (tphl and tplh). The netlist is in `ngspice/`.

**Command:**

```bash
ngspice <your_netlist_file>.spice
```

Inside ngspice:

```
run
plot v(in) v(out)
```

![ngspice netlist and delays](images/26.png)

![ngspice waveform](images/37.png)

---

## 19. Feasibility as a Compact Circuit

- Uses only a small FSM, one counter, and a few registers.
- No processor, memory, operating system, or external software.
- Very few I/O pins (4 inputs, 3 outputs).
- Fully synthesizable Verilog.
- Reached GDS with clean DRC, LVS, and antenna results and zero WNS/TNS in Run 2.

---

## 20. Conclusion

The Digital Equipment Status and Fault Indicator detects persistent faults, filters short glitches, latches the fault until acknowledged, and displays the state on three LEDs. The design passes all self-checking simulation tests and completes the full flow from RTL to GDS with clean DRC, LVS, and antenna results.
