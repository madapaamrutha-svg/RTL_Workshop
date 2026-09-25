# MODULE-5
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
# Table of Contents

- [Introduction](#introduction)
- [Overview](#overview)
- [Tools and Technologies](#tools-and-technologies)
- [1. Routing](#1-routing)
  - [1.1 Route](#11-route)
- [2. Maze Routing – Lee's Algorithm](#2-maze-routing--lees-algorithm)
- [3. Design Rule Checking](#3-design-rule-checking)
  - [3.1 DRC Clean Layout](#31-drc-clean-layout)
- [4. DRC – Wire Width](#4-drc--wire-width)
- [5. DRC – Via Spacing](#5-drc--via-spacing)
- [6. Parasitic Extraction](#6-parasitic-extraction)
- [7. OpenLane Physical Design Flow](#7-openlane-physical-design-flow)
- [8. Floorplanning and Power Planning](#8-floorplanning-and-power-planning)
- [9. OpenLane Physical Design Execution](#9-openlane-physical-design-execution)
- [10. OpenLane Configuration Parameters](#10-openlane-configuration-parameters)
- [11. Routing Output](#11-routing-output)
- [12. Fast Route and Detailed Route](#12-fast-route-and-detailed-route)
- [13. TritonRoute](#13-tritonroute)
- [14. Preprocessed Route Guides](#14-preprocessed-route-guides)
- [15. Intra-Layer Parallel and Inter-Layer Sequential Routing](#15-intra-layer-parallel-and-inter-layer-sequential-routing)
- [16. TritonRoute Problem Statement](#16-tritonroute-problem-statement)
- [17. Handling Connectivity](#17-handling-connectivity)
- [18. Routing Topology Algorithm](#18-routing-topology-algorithm)
- [19. OpenLane TritonRoute Execution](#19-openlane-tritonroute-execution)
- [20. Routing Data Generation](#20-routing-data-generation)
- [21. SPEF / Parasitic Extraction](#21-spef--parasitic-extraction)
- [22. OpenLane Synthesis and Routing Results](#22-openlane-synthesis-and-routing-results)
- [Physical Design Flow Summary](#physical-design-flow-summary)
- [Key Learning Outcomes](#key-learning-outcomes)
- [Tools and Technologies](#tools-and-technologies)
- [Conclusion](#conclusion)

# Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| **OpenLane** | Automated RTL-to-GDSII physical design flow |
| **SKY130** | Open-source 130 nm semiconductor process technology |
| **TritonRoute** | Detailed routing and design-rule-aware routing |
| **OpenROAD** | Physical design implementation and optimization |
| **OpenSTA** | Static Timing Analysis (STA) |
| **Magic** | Layout viewing and physical verification |
| **LEF** | Library Exchange Format containing physical library information |
| **DEF** | Design Exchange Format containing physical design information |
| **SPEF** | Standard Parasitic Exchange Format for extracted parasitic data |
| **Linux / Ubuntu** | Execution environment for the physical design tools |
| **Oracle VM VirtualBox** | Virtual machine environment used to run the Linux-based flow |
| **GitHub** | Version control and documentation of the workshop work |

# Introduction

Physical Design is an important stage in the VLSI design flow where the synthesized circuit is converted into a physical layout that can be fabricated on silicon.

In this module, the SKY130 technology and OpenLane-based physical design flow are explored with a focus on routing and post-routing analysis. The module covers global and detailed routing, maze routing using Lee's Algorithm, Design Rule Checking (DRC), wire-width and via-spacing verification, parasitic extraction, SPEF generation, and detailed routing using TritonRoute.

The practical work also covers route-guide preprocessing, intra-layer parallel routing, inter-layer sequential routing, connectivity handling, routing topology optimization, and inspection of OpenLane-generated synthesis and routing results.

The objective of this module is to understand how routing is performed while satisfying physical design rules, maintaining connectivity, and preparing the design for post-layout timing and physical verification.

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
<img width="1920" height="1080" alt="Screenshot (198)" src="https://github.com/user-attachments/assets/db68b38b-d354-4555-bd63-b95fe62f1a29" />



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
<img width="1920" height="1080" alt="Screenshot (200)" src="https://github.com/user-attachments/assets/15e3377e-5072-4200-abb9-38afd8bac285" />



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

<img width="1920" height="1080" alt="Screenshot (201)" src="https://github.com/user-attachments/assets/bccabd9e-d1c6-434a-9548-b3f874a72dba" />


The image shows the routed design after DRC verification.

A DRC-clean design indicates that the layout satisfies the checked physical design rules.

---

# 4. DRC – Wire Width

Wire width is an important physical design constraint.

If a metal wire is narrower than the minimum allowed width, it may violate the manufacturing rules and can affect the reliability of the interconnect.

### 4th Image – Wire Width Design Rule

<img width="1920" height="1080" alt="Screenshot (202)" src="https://github.com/user-attachments/assets/b3858f26-b0f2-4519-8291-9c65e025c507" />

The image illustrates the wire-width rule applied during physical verification.

The metal wire must maintain the required minimum width according to the technology design rules.

---

# 5. DRC – Via Spacing

Vias provide electrical connections between different metal layers.

Correct spacing between vias and surrounding metal structures is necessary to prevent manufacturing violations and unintended shorts.

### 5th Image – Via Spacing

<img width="1920" height="1080" alt="Screenshot (203)" src="https://github.com/user-attachments/assets/10fa4ecb-0b70-4f6c-9267-d02414e309cb" />

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
<img width="1920" height="1080" alt="Screenshot (204)" src="https://github.com/user-attachments/assets/09b81418-a790-41ae-9fbd-64557e484113" />


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
```
<img width="1274" height="548" alt="Screenshot (205)" src="https://github.com/user-attachments/assets/b9eba7d7-78b9-43e2-b8aa-ccf61341b5df" />

7th Image – OpenLane Terminal Output

The terminal output shows the execution of the OpenLane physical design flow and the generation of technology and design-related files.

## 8. Floorplanning and Power Planning
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
<img width="1279" height="729" alt="Screenshot (206)" src="https://github.com/user-attachments/assets/6dfe1e79-5181-485b-aabf-ed24cc199bb2" />


The image shows the physical floorplan containing:
Standard-cell rows
Standard-cell power connections
Power stripes
Block power ring
I/O and corner pads
Macro cell
Block halo
Power planning ensures that the power and ground networks can reliably distribute VPWR and VGND throughout the design.

## 9. OpenLane Physical Design Execution
The OpenLane flow generates intermediate and final physical-design files during different stages.
9th Image – OpenLane Execution Output
<img width="1225" height="572" alt="Screenshot (207)" src="https://github.com/user-attachments/assets/1f3d7d6b-11ae-44ea-9c34-a742d00f00ac" />

The terminal output shows OpenLane processing the design and generating the required physical-design information.
The output includes technology data, design data, grid information, and routing-related information.

## 10. OpenLane Configuration Parameters
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
<img width="1294" height="580" alt="Screenshot (208)" src="https://github.com/user-attachments/assets/2dde76e7-6423-498d-831a-ced5b6558db6" />

The image shows configuration parameters used to control placement, CTS, routing, and related physical-design operations.
These parameters influence:
Cell placement density
Clock-tree generation
Routing layers
Routing optimization
Layout generation

## 11. Routing Output
After the routing stage, the generated routing information can be inspected from the OpenLane run directories.
11th Image – Routing Output
<img width="1308" height="606" alt="Screenshot (209)" src="https://github.com/user-attachments/assets/72d4445b-8cc2-4b1e-a8cf-8da2c843a991" />

The terminal output shows the generated routing-related files and the completion of the routing stage.

## 12. Fast Route and Detailed Route
Routing can be divided into different stages.
Fast Route
Fast routing provides an initial routing solution and generates route guides.
Detailed Route
Detailed routing converts the initial routing information into actual physical routing while satisfying detailed design rules.
12th Image – Fast Route and Detailed Route
<img width="1291" height="700" alt="Screenshot (210)" src="https://github.com/user-attachments/assets/8902f729-47f1-4c2e-9fc3-f56161ffe0bf" />

The image illustrates the routing process divided into:
Fast Route
Detailed Route
Fast routing generates an approximate routing solution, while detailed routing performs the final physical implementation.

## 13. TritonRoute
TritonRoute is a detailed routing engine used in modern physical design flows.
It performs detailed routing while considering:
Routing guides
Design rules
Connectivity
Metal layers
Via placement
Routing constraints
13th Image – TritonRoute
<img width="1257" height="722" alt="Screenshot (211)" src="https://github.com/user-attachments/assets/0dd0f4e0-32e1-4296-94ef-798fadb253d2" />

The image introduces TritonRoute and its role in the detailed routing stage.
TritonRoute performs the initial detailed routing while attempting to follow the preprocessed route guides.

## 14. Preprocessed Route Guides
Route guides provide information about the preferred regions and directions in which nets should be routed.
Preprocessing can simplify the routing problem by transforming the original routing guides into a form suitable for detailed routing.
14th Image – Preprocessed Route Guides
<img width="1289" height="681" alt="Screenshot (212)" src="https://github.com/user-attachments/assets/36472224-79f3-475b-9977-f131d822c29d" />

The image demonstrates the preprocessing of route guides.
Important requirements include:
Route guides should have unit width.
Route guides should follow the preferred routing direction.


## 15. Intra-Layer Parallel and Inter-Layer Sequential Routing
Routing can be performed using different strategies across and within metal layers.
Intra-Layer Parallel Routing
Multiple routing tasks can be handled in parallel within the same metal layer.
Inter-Layer Sequential Routing
Routing can proceed sequentially across different metal layers to establish complete connectivity.
15th Image – Intra-Layer Parallel & Inter-Layer Sequential Panel Routing
<img width="1307" height="724" alt="Screenshot (214)" src="https://github.com/user-attachments/assets/2fa62e0e-d5d9-44e0-bfd7-5e142f326db1" />

The image illustrates the panel-based routing approach involving:
Intra-layer parallel routing
Inter-layer sequential routing
Multiple metal layers
Panel decomposition

## 16. TritonRoute Problem Statement
The detailed routing problem can be formulated using input design information, route guides, and routing constraints.
16th Image – TritonRoute Problem Statement
<img width="1920" height="1080" alt="Screenshot (215)" src="https://github.com/user-attachments/assets/ef77fdf2-ebaf-4100-bb15-160a0060864f" />

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

## 17. Handling Connectivity
Connectivity is a critical requirement during detailed routing.
Every net must be physically connected to all required pins and routing segments without introducing unwanted shorts.
17th Image – Handling Connectivity
<img width="1306" height="730" alt="Screenshot (217)" src="https://github.com/user-attachments/assets/67e57a23-4b35-41a2-9d60-8db4540e3291" />

The image explains the concept of Access Points (APs) and Access Point Clusters (APCs).
Access Point (AP)
An Access Point is an on-grid point on the metal layer of a route guide used to connect lower-layer segments, upper-layer segments, pins, or I/O ports.
Access Point Cluster (APC)
An Access Point Cluster is a union of access points derived from the same lower-layer segment, upper-layer guide, pin, or I/O port.

## 18. Routing Topology Algorithm
Routing topology determines how multiple connection points of a net are connected efficiently.
The topology optimization process attempts to minimize routing cost while maintaining complete connectivity.
18th Image – Routing Topology Algorithm
<img width="1279" height="698" alt="Screenshot (220)" src="https://github.com/user-attachments/assets/5b30a487-c456-49f4-9296-ecf71abd57e7" />

The image shows an algorithm for optimizing routing topology.
The algorithm evaluates connectivity and routing cost and produces an optimized routing tree.
The objective is to obtain an efficient routing topology with reduced routing cost.

## 19. OpenLane TritonRoute Execution
The TritonRoute stage can be executed from the OpenLane working directory.
19th Image – TritonRoute/OpenLane Terminal
<img width="1381" height="708" alt="Screenshot (221)" src="https://github.com/user-attachments/assets/c4dcd2aa-2956-4ab4-9809-350c5b9911b0" />

The terminal output shows the execution environment and OpenLane working directories used for the physical design flow.

## 20. Routing Data Generation
After routing, routing-related information is stored in the corresponding OpenLane run directories.
20th Image – Routing Output Data
<img width="1373" height="721" alt="Screenshot (222)" src="https://github.com/user-attachments/assets/c6f68722-dd0f-49f0-a89d-a0da154d132b" />

The terminal output shows generated routing data and related files produced during the physical design process.
These files can be used for further analysis and verification.

## 21. SPEF / Parasitic Extraction
Standard Parasitic Exchange Format (SPEF) is used to represent extracted parasitic information.
SPEF contains information related to:
Resistance
Capacitance
Nets
Interconnect parasitics
Connectivity
21st Image – SPEF Extraction
<img width="1297" height="717" alt="Screenshot (224)" src="https://github.com/user-attachments/assets/d783ac0f-a440-4cba-b1e1-9b2321e3e0ad" />

The terminal shows the execution of the SPEF extraction process.
The extraction script processes the routed DEF and generates parasitic information required for post-layout analysis.

## 22. OpenLane Synthesis and Routing Results
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
<img width="1063" height="571" alt="Screenshot (225)" src="https://github.com/user-attachments/assets/8a2a1fe0-58f0-4f91-b324-334bc33ea409" />

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

# Key Learning Outcomes
-Through this module, the following concepts were studied and demonstrated:
-Understanding physical design routing
-Understanding maze routing and Lee's Algorithm
-Understanding global and detailed routing
-Understanding fast routing and detailed routing
-Understanding TritonRoute
-Understanding route guides and route-guide preprocessing
-Understanding intra-layer and inter-layer routing
-Understanding access points and access point clusters
-Understanding routing topology optimization
-Understanding DRC verification
-Understanding wire-width and via-spacing constraints
-Understanding parasitic extraction
-Understanding SPEF generation
-Understanding OpenLane routing results
-Understanding OpenLane physical-design directories and outputs


# Conclusion
This module provided practical exposure to the physical design stages following placement, with particular emphasis on routing, detailed routing, design-rule verification, and parasitic extraction.
The experiments demonstrated how OpenLane and TritonRoute can be used to generate and verify physical routing while considering connectivity, design rules, routing guides, wire width, via spacing, and parasitic effects.
The generated routing, DRC, parasitic extraction, and OpenLane result files provide the necessary information for subsequent timing analysis and final physical-design verification.

## 👤 Author

**Amrutha Madapa**  
B.Tech – Electronics & Communication Engineering  
Anurag University  
[RTL Workshop Repository](https://github.com/madapaamrutha-svg/RTL_Workshop)

