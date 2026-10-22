# Digital Equipment Status and Fault Indicator Using Verilog HDL

A compact synthesizable digital circuit that monitors the status of an equipment unit and shows normal, warning, and fault conditions on three LEDs. The design is taken from RTL through simulation, synthesis, static timing analysis, physical design (OpenLane), and signoff to a final GDS layout, with an ngspice check at the end.

**Author:** MADAPA AMRUTHA

**College:** ANURAG UNIVERSITY

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
<img width="1300" height="934" alt="gds simulation 28th image" src="https://github.com/user-attachments/assets/39c78034-c0d7-4907-8519-2f3e76b3a566" />



---

## 10. Waveform

**Command:**

```bash
gtkwave dump.vcd
```

The waveform shows `ack`, `persist_cnt`, and the three LED outputs.
<img width="1300" height="934" alt="gtkwave gds 29th image" src="https://github.com/user-attachments/assets/8e6fed38-40bf-4321-a92e-8111b420faa4" />



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
<img width="1259" height="934" alt="synthesized netlist 6th" src="https://github.com/user-attachments/assets/b54c1386-f538-4123-ac9c-ba99239e3ed3" />

<img width="1259" height="934" alt="schematic yosys 7th" src="https://github.com/user-attachments/assets/b938ab37-6a6e-4cb1-bb1e-ad3d4fcd2e10" />

<img width="1259" height="934" alt="8th" src="https://github.com/user-attachments/assets/43765503-ecb8-4bcb-bc1d-8ce7acdbb415" />

<img width="1259" height="934" alt="21st yosys stat count cells" src="https://github.com/user-attachments/assets/0c439c86-6aa2-44ac-832f-e12812a5640e" />


---

## 12. Pre-Layout STA

**Command (inside the OpenLane shell):**

```tcl
run_sta
```
<img width="1259" height="934" alt="22nd prelayout slack" src="https://github.com/user-attachments/assets/d5274955-898b-4a9a-ab78-abe5405547da" />



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
<img width="1259" height="934" alt="25th" src="https://github.com/user-attachments/assets/22058f24-efdc-46a2-b18b-8180b246a996" />





### 13.2 Placement
<img width="1259" height="934" alt="placement 24th" src="https://github.com/user-attachments/assets/58c9323e-192f-40ae-8c71-9a589cf6534f" />


### 13.3 Clock Tree Synthesis (CTS)

<img width="1259" height="934" alt="floorplan  23rd" src="https://github.com/user-attachments/assets/e568626c-3267-4c4a-9be7-c41e0eeb7d71" />



### 13.4 Routing
<img width="1259" height="934" alt="26th" src="https://github.com/user-attachments/assets/37232991-1db6-4f0c-a239-2a04e5ca0912" />



---

## 14. Post-Route STA

Timing is checked at three corners after routing. Reports are in `runs/run2/reports/`.
<img width="1259" height="934" alt="17 sta running 3 corners" src="https://github.com/user-attachments/assets/c6a2da84-c084-4931-88b3-c90cdb4dbd62" />

<img width="1259" height="934" alt="18th image detailed path report" src="https://github.com/user-attachments/assets/af23a051-0c02-4d63-afff-9b2b85761528" />



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
<img width="1259" height="934" alt="layout 9th" src="https://github.com/user-attachments/assets/b7f72a17-d565-4eb4-bda8-8db7570ba997" />



---

## 16. Signoff Summary (Run 2)

**Command:**

```bash
cat runs/run2/reports/final_summary_report.csv
```

The report is saved in `physical_design/run2_final_summary_report.csv`.

<img width="1259" height="934" alt="antenna log 15" src="https://github.com/user-attachments/assets/0c30ca6f-0c00-48e5-8fac-159955961f8c" />



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

<img width="1259" height="934" alt="10" src="https://github.com/user-attachments/assets/b93c468c-a486-4b88-a9ce-df116e01e7f6" />

<img width="1259" height="934" alt="11 layout results" src="https://github.com/user-attachments/assets/db7cd09c-ac49-417d-9005-f980151be159" />

<img width="1259" height="934" alt="layout final 12th" src="https://github.com/user-attachments/assets/af346b0d-268c-46d0-8314-d373c321be15" />

<img width="1259" height="934" alt="lvs report verify 13" src="https://github.com/user-attachments/assets/a0a39e2d-37fc-483b-96a7-98651cbfc9ba" />

<img width="1259" height="934" alt="drc report check 13th" src="https://github.com/user-attachments/assets/7a2b2cf1-3db3-4bd8-9ddf-28352634b06e" />

<img width="1259" height="934" alt="antenna log 15" src="https://github.com/user-attachments/assets/179da6d0-4e3e-4458-8ed6-8cd1656710ab" />



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
<img width="1259" height="934" alt="20th image ngspice" src="https://github.com/user-attachments/assets/e0d42e93-6660-4a84-bd4c-8129496798f7" />

<img width="1300" height="934" alt="gdk ngspice 31st image" src="https://github.com/user-attachments/assets/4cb2a5ae-b3e6-47ab-ae68-5628b9753468" />

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
