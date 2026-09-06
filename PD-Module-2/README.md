# PHYSICAL DESIGN

## Module 1 – Chip Floorplanning and Power Integrity

This module covers the fundamental concepts of ASIC physical design, including netlist understanding, core and die dimensions, cell area calculation, utilization factor, aspect ratio, pre-placed cells, floorplanning, switching current, noise margin, and decoupling capacitors.

---

# 1. Define Width and Height of Core and Die

The first step in physical design is to understand the netlist and convert the logical representation of the design into physical dimensions.

A netlist describes the connectivity between different components of an electronic design.

The example netlist contains:

* Flip-Flops (FF)
* AND gate
* OR gate
* Clock connection
* Data connections

The standard cells and flip-flops in the netlist are later converted into physical dimensions during floorplanning.

---

# 2. Convert Netlist Symbols into Physical Dimensions

After understanding the netlist, the logical components are represented as physical standard cells.

The highlighted elements include:

* Flip-Flops
* Standard cells
* AND/OR logic cells

Each logical cell occupies a certain physical area on the silicon.

Therefore, the total area occupied by all cells must be calculated before determining the core dimensions.

---

# 3. Calculate Area Occupied by the Netlist

For the given example, each standard cell and flip-flop is represented as a unit square.

For example:

```text
Width  = 1 unit
Height = 1 unit

Area = Width × Height
     = 1 × 1
     = 1 sq. unit

The total area occupied by the netlist is calculated by adding the area of all standard cells and flip-flops.
This gives the total cell area required inside the core.
4. Utilization Factor and Aspect Ratio
Two important parameters used to define the core dimensions are:
Utilization Factor

Utilization Factor =
Area Occupied by Netlist
-------------------------
Total Area of Core

The utilization factor indicates how much of the core area is occupied by the placed cells.
Aspect Ratio
Aspect Ratio = Height / Width
For the example shown, the core and die dimensions are selected based on the required utilization factor and aspect ratio.
The diagram illustrates a core of approximately 4 units × 2 units with the die surrounding the core.
5. Core and Die Dimension Example
Another example demonstrates how the dimensions of the core and die change according to the utilization factor.
The physical dimensions are selected so that sufficient space is available for:
Standard-cell placement
Routing
Power distribution
Decoupling cells
Other physical-design requirements
A lower utilization factor provides more free area inside the core, which can help in reducing placement and routing congestion.
6. Define Locations of Pre-placed Cells
Some cells or blocks cannot be freely placed by the automated placement tool.
These cells are known as pre-placed cells.
Examples include:
Memory
Clock-gating cells
Comparators
Multiplexers
Other large IP blocks
These blocks have user-defined locations and are placed before automated placement and routing.
7. Placement of Pre-placed Cells
The location of pre-placed cells is important because their position affects the rest of the physical design.
The example shows two blocks containing multiple logic cells.
The cells and their connections are arranged so that the required input/output connections can be maintained.
I/O pins can be extended to make the connectivity between blocks clear.
Proper placement helps reduce:
Routing congestion
Wire length
Timing problems
Unnecessary routing detours
8. IP Blocks and Floorplanning
Modern ASIC designs may contain several pre-designed IP blocks.
Examples include:
Memory
Clock-gating cells
Comparator
Multiplexer
The arrangement of these IPs or blocks inside the chip is called floorplanning.
These IPs have user-defined locations and are placed in the chip before automated placement and routing.
Therefore, floorplanning determines the physical organization of major blocks inside the chip.

9. Surround Pre-placed Cells with Decoupling Capacitors
Pre-placed blocks may experience high switching activity and can require a large instantaneous current.
To improve power integrity, decoupling capacitors can be placed around the pre-placed cells.
The floorplan contains:
Core
Die
Block A
Block B
Block C
Decoupling capacitor regions
The decoupling capacitors provide a local source of charge near the blocks.
This helps reduce supply voltage fluctuations during switching.
10. Switching Current and Voltage Drop
During switching operation, a complex digital circuit may demand a large amount of instantaneous current.
This is called peak switching current.
The power supply network contains parasitic resistance and inductance.
When switching current flows through these elements, a voltage drop occurs.
The resistive voltage drop is:
V = I × R
The inductive voltage variation is:
V = L × di/dt
Therefore, because of the resistance and inductance of the power network, the voltage available at the circuit can become lower than the ideal supply voltage.
11. Noise Margin Summary
Noise margin represents the ability of a digital circuit to tolerate unwanted voltage disturbances without changing the interpreted logic value.
The two important noise margins are:
Noise Margin High
NMH = VOH(min) − VIH(min)
Noise Margin Low
NML = VIL(max) − VOL(max)
The diagram shows different noise-induced bumps and their relationship with the noise-margin levels.
A small noise bump remains within the acceptable region and does not cause a logic error.
If the noise exceeds the available noise margin, it may be interpreted as an unwanted logic transition.
12. Solution: Add Decoupling Capacitors
One solution for reducing the effect of switching-current demand is to add a decoupling capacitor.
The decoupling capacitor is connected in parallel with the circuit.
When the circuit switches and requires a large current, the capacitor can provide charge locally.
The power network then replenishes the charge stored in the capacitor.
Switching occurs
       ↓
Circuit demands current
       ↓
Decoupling capacitor supplies charge
       ↓
Power network replenishes the charge
This reduces the effect of sudden current demand on the supply voltage.
13. Decoupling Capacitor Placement Around Blocks
Decoupling capacitors can be placed around important pre-placed blocks.
For example:
+--------------------------------+
|                                |
|        DECAP1                  |
|        Block A   Block B       |
|        DECAP2                  |
|        Block C                 |
|        DECAP3                  |
|                                |
+--------------------------------+
The purpose is to keep the decoupling capacitors close to the blocks that require additional instantaneous current.
This provides a local current source and improves power integrity.
14. Decoupling Capacitor Placement in the Floorplan
The floorplan can be organized using different regions for blocks and decoupling capacitors.
The example shows:
DECAP1
Block A
Block B
DECAP2
Block C
DECAP3
The decoupling capacitors are strategically placed around the pre-placed cells.
Proper placement helps reduce the distance between the capacitor and the switching circuit.
A shorter current path helps reduce the impact of parasitic resistance and inductance.
15. Power Network, Driver, Load and 16-bit Bus
The final example illustrates the power network connecting multiple driver and load circuits.
The power distribution network contains resistance and inductance.
Each circuit has associated capacitance and switching requirements.
The diagram also illustrates a signal path representing a multi-bit bus.
For the given example, the blue path represents a 16-bit bus.
The key concept is that switching activity across multiple signals can create a large instantaneous current demand.
Therefore, proper power-network design and decoupling are required to maintain stable supply voltage and reliable circuit operation.
Key Learnings
Through this module, the following concepts were studied:
Understanding a netlist
Converting logical cells into physical dimensions
Cell area calculation
Core and die dimensions
Utilization factor
Aspect ratio
Pre-placed cells
IP blocks
Floorplanning
Placement of pre-placed cells
Switching current
Peak current
IR/voltage drop due to resistance and inductance
Noise margin
Noise-induced voltage bumps
Decoupling capacitors
Decoupling capacitor placement
Power integrity
Driver and load connectivity
Multi-bit bus considerations
Conclusion
Chip floorplanning is a critical stage of ASIC physical design. The dimensions of the core and die must be selected based on cell area, utilization factor, and aspect ratio.
Pre-placed cells and IP blocks must be positioned carefully to achieve good connectivity and efficient routing.
During switching, large instantaneous current demand can cause voltage fluctuations because of resistance and inductance in the power network. Noise margin determines the ability of the circuit to tolerate such disturbances.
Decoupling capacitors provide local charge during high-current switching events and help maintain supply stability.
Thus, proper floorplanning, pre-placed-cell placement, power planning, noise-margin analysis, and decoupling-capacitor placement are essential for reliable physical design.
