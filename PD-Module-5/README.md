Yes 👍 DONE received.
Ippudu all 22 images ni exact order lo kalipi, ONE complete README.md ga istunna. Direct ga GitHub README.md lo copy-paste cheyyachu.
Note: Images ni images/01.png → images/22.png ani assume chesa. Mee actual image filenames different unte, aa paths matrame replace cheyyali.
# SKY130 Physical Design – Routing, DRC, Parasitic Extraction & TritonRoute

## Overview

This module covers the major stages involved in the physical design flow using the SKY130 technology and OpenLane-based tools.

The work includes:

- Global and detailed routing
- Maze routing using Lee's Algorithm
- Design Rule Checking (DRC)
- Wire-width and via-spacing verification
- Parasitic extraction
- SPEF generation
- TritonRoute
- Preprocessed route guides
- Intra-layer and inter-layer routing
- Routing topology optimization
- Connectivity handling
- OpenLane routing and synthesis results
- Physical design flow verification

---

# 1. Routing

Routing is the process of establishing physical connections between the placed standard cells, pins, and other circuit components while satisfying design rules.

The routing process consists mainly of:

- Global routing
- Fast routing
- Detailed routing
- Design-rule-aware routing
- Connectivity verification

## 1.1 Route

The routing stage connects the input and output pins through physical metal layers using buffers, flip-flops, and routing tracks.

### 1st Image – Route

![1st Image](./images/01.png)

The image shows the routed design with multiple nets connecting the input pins (`Din1`, `Din2`, `Din3`, `Din4`, `CLK1`, `CLK2`) to the corresponding output pins.

The routed layout contains:

- Flip-flops
- Buffers
- Decap cells
- Standard-cell blocks
- Metal interconnects
- Clock and data paths

---

# 2. Maze Routing – Lee's Algorithm

Maze routing is a grid-based routing technique used to find a valid path between two points while avoiding obstacles.

Lee's algorithm works by:

1. Starting from the source point.
2. Expanding the routing grid.
3. Assigning distance values to reachable cells.
4. Continuing until the destination is reached.
5. Backtracking through the minimum-distance path.

### 2nd Image – Maze Routing using Lee's Algorithm

![2nd Image](./images/02.png)

The image demonstrates maze routing using **Lee's Algorithm (Lee 1961)**.

The routing grid is explored systematically and numbered according to the distance from the source.

This approach guarantees a valid shortest-path solution when a path exists, although it can require significant memory for large routing grids.

---

# 3. Design Rule Checking

Design Rule Checking (DRC) verifies whether the physical layout satisfies the manufacturing rules defined by the selected technology.

Typical design rules include:

- Minimum wire width
- Minimum spacing
- Via spacing
- Metal enclosure
- Layer-specific restrictions
- Connectivity constraints

## 3.1 DRC Clean Layout

### 3rd Image – DRC Clean

![3rd Image](./images/03.png)

The image shows the routed design after DRC verification.

A DRC-clean design indicates that the layout satisfies the checked physical design rules.

---

# 4. DRC – Wire Width

Wire width is an important physical design constraint.

If a metal wire is narrower than the minimum allowed width, it may violate the manufacturing rules and can affect the reliability of the interconnect.

### 4th Image – Wire Width Design Rule

![4th Image](./images/04.png)

The image illustrates the wire-width rule applied during physical verification.

The metal wire must maintain the required minimum width according to the technology design rules.

---

# 5. DRC – Via Spacing

Vias provide electrical connections between different metal layers.

Correct spacing between vias and surrounding metal structures is necessary to prevent manufacturing violations and unintended shorts.

### 5th Image – Via Spacing

![5th Image](./images/05.png)

The image shows the via-spacing rule and demonstrates how adequate spacing is maintained between vias and nearby structures.

---

# 6. Parasitic Extraction

After routing, parasitic elements introduced by physical interconnects must be extracted.

Parasitic extraction identifies effects such as:

- Resistance
- Capacitance
- Interconnect delay
- Coupling effects

These parasitic values are later used for accurate timing analysis.

### 6th Image – Parasitics Extraction

![6th Image](./images/06.png)

The image shows the layout after the parasitic extraction stage.

The extracted parasitic information can be used for post-layout timing analysis and sign-off activities.

---

# 7. OpenLane Physical Design Flow

OpenLane automates several stages of the RTL-to-GDSII physical design flow.

A simplified flow is:

```text
RTL
 ↓
Synthesis
 ↓
Floorplanning
 ↓
Power Planning
 ↓
Placement
 ↓
CTS
 ↓
Routing
 ↓
DRC / LVS
 ↓
Parasitic Extraction
 ↓
Timing Analysis
 ↓
GDSII
7th Image – OpenLane Terminal Output
�
The terminal output shows the execution of the OpenLane physical design flow and the generation of technology and design-related files.
8. Floorplanning and Power Planning
Floorplanning determines the overall physical organization of the design.
Important elements include:
Core area
Die area
Standard-cell rows
I/O placement
Power rings
Power straps
Macro placement
8th Image – Floorplan and Power Planning
�
The image shows the physical floorplan containing:
Standard-cell rows
Standard-cell power connections
Power stripes
Block power ring
I/O and corner pads
Macro cell
Block halo
Power planning ensures that the power and ground networks can reliably distribute VPWR and VGND throughout the design.
9. OpenLane Physical Design Execution
The OpenLane flow generates intermediate and final physical-design files during different stages.
9th Image – OpenLane Execution Output
�
The terminal output shows OpenLane processing the design and generating the required physical-design information.
The output includes technology data, design data, grid information, and routing-related information.
10. OpenLane Configuration Parameters
OpenLane uses configuration parameters to control different stages of the physical design flow.
Important categories include:
Placement
Clock Tree Synthesis (CTS)
Routing
Magic
Density
Timing
Routing optimization
10th Image – OpenLane Configuration
�
The image shows configuration parameters used to control placement, CTS, routing, and related physical-design operations.
These parameters influence:
Cell placement density
Clock-tree generation
Routing layers
Routing optimization
Layout generation
11. Routing Output
After the routing stage, the generated routing information can be inspected from the OpenLane run directories.
11th Image – Routing Output
�
The terminal output shows the generated routing-related files and the completion of the routing stage.
12. Fast Route and Detailed Route
Routing can be divided into different stages.
Fast Route
Fast routing provides an initial routing solution and generates route guides.
Detailed Route
Detailed routing converts the initial routing information into actual physical routing while satisfying detailed design rules.
12th Image – Fast Route and Detailed Route
�
The image illustrates the routing process divided into:
Fast Route
Detailed Route
Fast routing generates an approximate routing solution, while detailed routing performs the final physical implementation.
13. TritonRoute
TritonRoute is a detailed routing engine used in modern physical design flows.
It performs detailed routing while considering:
Routing guides
Design rules
Connectivity
Metal layers
Via placement
Routing constraints
13th Image – TritonRoute
�
The image introduces TritonRoute and its role in the detailed routing stage.
TritonRoute performs the initial detailed routing while attempting to follow the preprocessed route guides.
14. Preprocessed Route Guides
Route guides provide information about the preferred regions and directions in which nets should be routed.
Preprocessing can simplify the routing problem by transforming the original routing guides into a form suitable for detailed routing.
14th Image – Preprocessed Route Guides
�
The image demonstrates the preprocessing of route guides.
Important requirements include:
Route guides should have unit width.
Route guides should follow the preferred routing direction.
15. Intra-Layer Parallel and Inter-Layer Sequential Routing
Routing can be performed using different strategies across and within metal layers.
Intra-Layer Parallel Routing
Multiple routing tasks can be handled in parallel within the same metal layer.
Inter-Layer Sequential Routing
Routing can proceed sequentially across different metal layers to establish complete connectivity.
15th Image – Intra-Layer Parallel & Inter-Layer Sequential Panel Routing
�
The image illustrates the panel-based routing approach involving:
Intra-layer parallel routing
Inter-layer sequential routing
Multiple metal layers
Panel decomposition
16. TritonRoute Problem Statement
The detailed routing problem can be formulated using input design information, route guides, and routing constraints.
16th Image – TritonRoute Problem Statement
�
Inputs
LEF
DEF
Preprocessed route guides
Output
A detailed routing solution with optimized:
Wire length
Via count
Constraints
The routing solution must satisfy:
Route-guide constraints
Connectivity constraints
Design rules
17. Handling Connectivity
Connectivity is a critical requirement during detailed routing.
Every net must be physically connected to all required pins and routing segments without introducing unwanted shorts.
17th Image – Handling Connectivity
�
The image explains the concept of Access Points (APs) and Access Point Clusters (APCs).
Access Point (AP)
An Access Point is an on-grid point on the metal layer of a route guide used to connect lower-layer segments, upper-layer segments, pins, or I/O ports.
Access Point Cluster (APC)
An Access Point Cluster is a union of access points derived from the same lower-layer segment, upper-layer guide, pin, or I/O port.
18. Routing Topology Algorithm
Routing topology determines how multiple connection points of a net are connected efficiently.
The topology optimization process attempts to minimize routing cost while maintaining complete connectivity.
18th Image – Routing Topology Algorithm
�
The image shows an algorithm for optimizing routing topology.
The algorithm evaluates connectivity and routing cost and produces an optimized routing tree.
The objective is to obtain an efficient routing topology with reduced routing cost.
19. OpenLane TritonRoute Execution
The TritonRoute stage can be executed from the OpenLane working directory.
19th Image – TritonRoute/OpenLane Terminal
�
The terminal output shows the execution environment and OpenLane working directories used for the physical design flow.
20. Routing Data Generation
After routing, routing-related information is stored in the corresponding OpenLane run directories.
20th Image – Routing Output Data
�
The terminal output shows generated routing data and related files produced during the physical design process.
These files can be used for further analysis and verification.
21. SPEF / Parasitic Extraction
Standard Parasitic Exchange Format (SPEF) is used to represent extracted parasitic information.
SPEF contains information related to:
Resistance
Capacitance
Nets
Interconnect parasitics
Connectivity
21st Image – SPEF Extraction
�
The terminal shows the execution of the SPEF extraction process.
The extraction script processes the routed DEF and generates parasitic information required for post-layout analysis.
22. OpenLane Synthesis and Routing Results
OpenLane stores results from different stages of the physical design flow in separate directories.
Important result directories include:
results/
├── synthesis/
├── routing/
├── placement/
├── cts/
├── floorplan/
└── signoff/
22nd Image – OpenLane Results
�
The image shows the OpenLane run directories and generated synthesis/routing results.
The generated files can be inspected to verify the completion of the corresponding physical design stages.
Physical Design Flow Summary
The complete physical design process covered in this module can be summarized as:
RTL Design
    ↓
Synthesis
    ↓
Floorplanning
    ↓
Power Planning
    ↓
Placement
    ↓
Clock Tree Synthesis
    ↓
Global Routing
    ↓
Fast Route
    ↓
Route Guide Generation
    ↓
Route Guide Preprocessing
    ↓
Detailed Routing
    ↓
TritonRoute
    ↓
DRC Verification
    ↓
Parasitic Extraction
    ↓
SPEF Generation
    ↓
Timing Analysis
    ↓
Physical Verification
Key Learning Outcomes
Through this module, the following concepts were studied and demonstrated:
Understanding physical design routing
Understanding maze routing and Lee's Algorithm
Understanding global and detailed routing
Understanding fast routing and detailed routing
Understanding TritonRoute
Understanding route guides and route-guide preprocessing
Understanding intra-layer and inter-layer routing
Understanding access points and access point clusters
Understanding routing topology optimization
Understanding DRC verification
Understanding wire-width and via-spacing constraints
Understanding parasitic extraction
Understanding SPEF generation
Understanding OpenLane routing results
Understanding OpenLane physical-design directories and outputs
Tools and Technologies
Tool / Technology
Purpose
OpenLane
RTL-to-GDSII physical design flow
SKY130
Open-source semiconductor technology
TritonRoute
Detailed routing
OpenSTA
Static timing analysis
Magic
Layout and physical verification
LEF
Physical library information
DEF
Design exchange format
SPEF
Parasitic information
Linux / Ubuntu
Execution environment
VirtualBox
Virtual machine environment
Conclusion
This module provided practical exposure to the physical design stages following placement, with particular emphasis on routing, detailed routing, design-rule verification, and parasitic extraction.
The experiments demonstrated how OpenLane and TritonRoute can be used to generate and verify physical routing while considering connectivity, design rules, routing guides, wire width, via spacing, and parasitic effects.
The generated routing, DRC, parasitic extraction, and OpenLane result files provide the necessary information for subsequent timing analysis and final physical-design verification.

**Important:** Nee uploaded images exact order **1 → 22** lo README lo petta. Missing screenshots `(213), (215), (218), (219), (223)` ni include cheyyaledu because avi nuvvu upload cheyyaledu.
