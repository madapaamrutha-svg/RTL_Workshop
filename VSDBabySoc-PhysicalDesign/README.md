# VSDBabySoC — SKY130 HD Physical Design and STA

## 1. Project Overview

This repository records what I learned and analysed about the VSDBabySoC physical design flow and multi-corner Static Timing Analysis (STA) using the SKY130 HD standard-cell library.

My earlier RTL workshop documentation covers MUX design, BabySoC architecture, synthesis, netlist analysis and waveform verification. This repository concentrates on physical design concepts and timing analysis.

## 2. Physical Design Flow

The RTL-to-GDSII flow consists of these stages:

1. Synthesis
2. Floorplanning
3. Power planning
4. Placement
5. Clock Tree Synthesis (CTS)
6. Routing
7. Parasitic extraction
8. Static Timing Analysis
9. Physical verification
10. GDSII layout generation

This list describes the overall flow. Only the stages backed by the available screenshots or reports should be treated as completed.

### Physical Design Screenshots

<img width="1919" height="1079" alt="Screenshot 2026-10-10 215236" src="https://github.com/user-attachments/assets/bf8b8862-08d4-41b0-94ea-e0033a9290aa?raw=true" />

## 3. Multi-Corner Static Timing Analysis

Static Timing Analysis checks whether a design meets its timing constraints, without needing simulation test vectors.

Multi-corner STA checks timing under different process, voltage and temperature (PVT) conditions.

The updated report I was given covers 16 SKY130 HD corners with an 11 ns clock constraint, roughly 90.91 MHz.

### Reported Setup Results

- Total corners analysed: 16
- Corners with positive setup WNS: 10
- Corners with negative setup WNS: 6
- Best reported setup WNS: +8.22 ns
- Worst reported setup WNS: -31.85 ns

Negative setup slack means a timing violation. These results do not show setup timing closure across all 16 corners.

### STA Report Screenshots

<img width="1338" height="747" alt="image" src="https://github.com/user-attachments/assets/8bc64a12-c768-41c4-bb8d-d4f194ba209d?raw=true" />

<img width="642" height="450" alt="image" src="https://github.com/user-attachments/assets/6183cc76-6b61-458b-8da9-38db51745fd1?raw=true" />

## 4. Setup and Hold Timing

**Setup timing:** checks that data arrives early enough before the active clock edge.

**Hold timing:** checks that data stays stable for the required time after the active clock edge.

**WNS:** Worst Negative Slack.

**TNS:** Total Negative Slack.

Positive slack means the checked path meets its timing requirement; negative slack means a timing violation.

### Timing Analysis Pictures

<img width="604" height="341" alt="image" src="https://github.com/user-attachments/assets/f2bda23e-3d80-48dd-bb35-20603e092040?raw=true" />

## 5. Results and Observations

The updated STA report shows setup violations in six of the 16 corners. The worst reported setup WNS is -31.85 ns, at `ss_n40C_1v28`.

Understanding the causes would need a closer look at the critical timing paths, clock and I/O constraints, cell and net delays, and parasitics.

I have not independently confirmed these updated values by re-running the full STA flow. They are documented as results that were supplied to me, not as independently verified signoff results.

## 6. Tools and Technologies

These tools and technologies are part of the VSDBabySoC physical design and timing analysis workflow.

| Tool / Technology | Purpose |
|---|---|
| Verilog HDL | Hardware description and RTL design |
| VSDBabySoC | Reference SoC design |
| SKY130 HD | Open-source standard-cell library |
| Yosys | RTL synthesis and logic optimization |
| OpenLANE | RTL-to-GDSII implementation flow |
| OpenROAD | Physical design implementation |
| OpenSTA | Static Timing Analysis |
| Magic | Layout editing and design rule checking |
| GTKWave | Waveform visualization |
| ngspice | Circuit simulation |
| Linux Terminal | Running EDA tools and managing the workflow |
| Git | Version control |
| GitHub | Repository hosting and documentation |

## 7. Clock Configuration

The multi-corner timing analysis used an 11 ns clock period.

### Clock Configuration Details

- Clock Period: 11 ns
- Target Frequency: approximately 90.91 MHz
- Technology: SKY130 HD
- Analysis Type: Multi-Corner Static Timing Analysis
- PVT Conditions: multiple process, voltage and temperature corners

The clock period sets the requirement against which setup timing is judged. The analysis shows whether the design meets the given timing constraints under different operating conditions.

## 8. Critical Path Analysis

Critical path analysis is a key part of STA. It finds the timing paths that have the least timing margin.

The STA reports are used to understand:

- Startpoints and endpoints of timing paths.
- Cell propagation delays.
- Interconnect delays.
- Setup slack and hold slack.
- Worst Negative Slack (WNS).
- Total Negative Slack (TNS).
- Timing violations across PVT corners.

The negative setup slack in the report means some paths do not meet the clock constraint.

To find the causes of these violations, the critical paths, clock constraints, cell delays, net delays and parasitic effects need to be studied further.

## 9. Multi-Corner Timing Analysis

Multi-Corner STA evaluates circuit timing under different process, voltage and temperature conditions.

Each operating corner can change standard-cell delay, interconnect behaviour and overall timing performance. The analysis shows whether the design meets its timing requirements across the chosen operating conditions.

### Key Parameters

| Parameter | Description |
|---|---|
| Process | Variations in semiconductor manufacturing |
| Voltage | Operating supply voltage |
| Temperature | Operating temperature |
| WNS | Worst Negative Slack |
| TNS | Total Negative Slack |
| Setup | Checks data arrival before the active clock edge |
| Hold | Checks data stability after the active clock edge |

The report contains results from 16 SKY130 HD timing corners.

## 10. Timing Closure Considerations

Timing closure means making sure a digital design meets its specified timing requirements.

The STA results show negative setup slack in six of the sixteen corners analysed.

Points to consider when investigating further:

- Examine the critical timing paths.
- Review clock and input/output constraints.
- Evaluate cell and interconnect delays.
- Understand setup and hold violations.
- Study the effect of different PVT conditions.
- Re-check timing reports after implementation changes.

The available results are timing observations and do not establish complete timing closure.

## 11. Learning Outcomes

Through this practical work, I gained an understanding of:

- VSDBabySoC architecture and its physical design exploration.
- SKY130 HD standard-cell library concepts.
- The overall ASIC RTL-to-GDSII implementation flow.
- Basics of floorplanning and placement.
- Power Distribution Network (PDN) concepts.
- Clock Tree Synthesis (CTS).
- Global and detailed routing concepts.
- Static Timing Analysis fundamentals.
- Setup and hold timing requirements.
- Multi-corner timing analysis under different PVT conditions.
- Reading WNS and TNS reports.
- Timing violations and the challenges of timing closure.
- Using open-source EDA tools for physical design.

## 12. Conclusion

This repository presents the physical design concepts and multi-corner timing analysis I studied for VSDBabySoC using the SKY130 HD standard-cell library.

The results show why setup timing must be checked across multiple PVT corners before claiming timing closure.



