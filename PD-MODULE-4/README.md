# pd-Module 4: CMOS Inverter Design, Simulation, CMOS Fabrication

## 📌 Project Overview

This project presents a complete study of a CMOS inverter, beginning with
transistor-level circuit construction and SPICE-based electrical simulation.
The study is then extended to transistor sizing, switching behaviour, physical
layout, and CMOS fabrication concepts.

The complete flow followed in this project is:

CMOS Circuit → SPICE Netlist → DC Analysis → VTC → Switching Threshold →
Transistor Sizing → Layout → CMOS Fabrication

The project connects the electrical behaviour of a CMOS inverter with its
physical implementation and semiconductor fabrication process.

---

## 🎯 Objectives

The main objectives of this project are:

1. To study the operation of a CMOS inverter using complementary NMOS and
   PMOS devices.

2. To create and evaluate a transistor-level CMOS inverter using SPICE.

3. To investigate the influence of transistor dimensions on inverter
   characteristics.

4. To obtain and analyse the Voltage Transfer Characteristic (VTC) of the
   inverter.

5. To determine the switching threshold voltage (V_M) of the CMOS inverter.

6. To study inverter stability and understand the importance of transistor
   sizing.

7. To examine the influence of different (W/L) ratios on inverter behaviour.

8. To understand the physical realization of a CMOS standard cell.

9. To explore the major stages involved in the 16-mask CMOS fabrication
   sequence.

10. To study active-region formation, well formation, gate formation, LDD
    implantation, source/drain formation, contacts and metal interconnections.

11. To establish the relationship between circuit simulation and semiconductor
    fabrication technology.

---

## 🔧 Tools & Technologies

| Tool / Technology | Purpose |
|-------------------|---------|
| SPICE / NGSPICE | Simulation of transistor-level electrical circuits |
| CMOS Inverter | Circuit under investigation |
| NMOS & PMOS | Complementary MOS transistor devices |
| VTC Analysis | Analysis of static inverter characteristics |
| Magic VLSI | Creation and inspection of physical layouts |
| SKY130A PDK | CMOS technology files and layout design rules |
| Linux Terminal | Running simulation and design commands |
| Git & GitHub | Version control and project documentation |

---

## 🔬 Project Workflow

CMOS Inverter Design ↓ SPICE Netlist Creation ↓ DC Simulation ↓ VTC Generation
↓ Switching Threshold Analysis ↓ Transistor Sizing ↓ Physical Layout ↓
16-Mask CMOS Fabrication Study ↓ Contacts & Local Interconnect ↓ Higher-Level
Metal ↓ Complete CMOS Structure

---

# 1. SPICE CMOS Inverter Design

The first stage is the construction of a transistor-level CMOS inverter using
a SPICE circuit description.

The inverter consists of:

- One PMOS transistor connected to \(V_{DD}\)
- One NMOS transistor connected to \(V_{SS}\)
- A common input terminal for both transistor gates
- A common output node formed by the transistor drains
- A capacitive load connected to the output
- Defined NMOS and PMOS dimensions
- CMOS device model definitions
- DC simulation commands

The initial transistor dimensions are:

\[
W_n = W_p = 0.375\mu m
\]

\[
L_n = L_p = 0.25\mu m
\]

Therefore,

\[
\frac{W_n}{L_n} = \frac{W_p}{L_p} = 1.5
\]

The SPICE netlist describes the complete electrical circuit by specifying the
MOS devices, their dimensions, supply sources, input conditions, output load,
device models and simulation instructions.

<!-- INSERT YOUR IMAGE HERE -->

---

# 2. SPICE Simulation — Initial Device Configuration

The first simulation is performed with equal NMOS and PMOS dimensions. This
provides a reference response for studying the basic operation of the CMOS
inverter.

The fundamental signal relationship can be represented as:

Input Voltage → Transistor State → Output Voltage

The two MOS devices operate in a complementary manner:

- With a LOW input, the PMOS conducts while the NMOS remains switched OFF.
- With a HIGH input, the NMOS conducts while the PMOS becomes OFF.
- Around the transition region, both devices influence the output behaviour.

SPICE converts the transistor-level circuit description into electrical
simulation results. These results provide the required information before
moving towards physical layout implementation.
<img width="950" height="435" alt="image" src="https://github.com/user-attachments/assets/6296d211-ba5d-4171-8186-00f9ab236553" />



---

# 3. CMOS Inverter Voltage Transfer Characteristic

The DC simulation produces the Voltage Transfer Characteristic (VTC) of the
CMOS inverter.

The VTC describes the dependence of the output voltage on the applied input
voltage:

\[
V_{out}=f(V_{in})
\]

The characteristic can be broadly divided into three regions:

HIGH OUTPUT → TRANSITION → LOW OUTPUT

For the HIGH-output condition:

\[
V_{out} \approx V_{DD}
\]

For the LOW-output condition:

\[
V_{out} \approx 0
\]

The sharp change in the transition region indicates the high voltage gain
provided by the CMOS inverter around its switching point.

A relatively small change in input voltage can therefore result in a large
change in output voltage, which is one of the important properties of CMOS
logic circuits.
<img width="850" height="732" alt="image" src="https://github.com/user-attachments/assets/3e855295-0e05-455a-855e-93510db6d6a7" />



---

# 4. Transistor Sizing Comparison

Two different CMOS inverter sizing conditions are considered to observe the
effect of transistor dimensions on the inverter response.
<img width="844" height="392" alt="image" src="https://github.com/user-attachments/assets/57725b75-d546-4c97-8b30-1c566d6e1669" />


## Configuration 1

\[
W_n = W_p = 0.375\mu m
\]

\[
\frac{W_n}{L_n}=\frac{W_p}{L_p}=1.5
\]

In this configuration, both devices have identical width-to-length ratios.

<!-- INSERT YOUR IMAGE HERE -->

## Configuration 2

\[
W_n = 0.375\mu m
\]

\[
W_p = 0.9375\mu m
\]

\[
\frac{W_n}{L_n}=1.5
\]

\[
\frac{W_p}{L_p}=3.75
\]

Here, the PMOS width is increased while the NMOS dimensions remain unchanged.

Increasing the PMOS width modifies the relative drive capability of the two
transistors. Consequently, the switching characteristics of the inverter
also change.

This comparison shows that transistor dimensions influence not only the
physical size of the device but also its electrical performance.

<!-- INSERT YOUR IMAGE HERE -->

---

# 5. CMOS Inverter Robustness — Switching Threshold
<img width="847" height="393" alt="image" src="https://github.com/user-attachments/assets/66bec144-e615-4c42-a5f8-f075eab6d6c0" />


The switching threshold voltage \(V_M\) is defined as the input voltage at
which the inverter satisfies:

\[
V_{in}=V_{out}
\]

Different transistor sizing conditions produce different switching points.
Therefore, the switching threshold can be used to observe how the balance
between NMOS and PMOS strength affects inverter operation.

The obtained values are approximately:

\[
V_M \approx 0.98V
\]

and

\[
V_M \approx 1.2V
\]

depending on the selected transistor sizing configuration.

The switching threshold represents the point where the inverter changes from
one logic state to the other. Changing the relative strength of the PMOS and
NMOS devices shifts this point.



---

# 6. Mathematical Analysis of Switching Threshold
<img width="844" height="392" alt="image" src="https://github.com/user-attachments/assets/5b8cc541-9e97-4341-a5ae-7310af852c9f" />

The switching threshold can also be evaluated mathematically by considering
the relative drive strengths of the NMOS and PMOS transistors.

The important parameters involved in the analysis include:

1. \(W_n/L_n\)
2. \(W_p/L_p\)
3. \(K_n\)
4. \(K_p\)
5. Saturation voltage
6. Device threshold parameters

The switching point is therefore influenced by the relative strengths of the
two MOS devices rather than being an independent or fixed value.

The mathematical analysis helps explain the movement of the switching
threshold observed in the SPICE VTC when the transistor dimensions are
modified.

This also provides a theoretical basis for understanding the simulation
results obtained from the CMOS inverter.



---

# 7. Final Switching-Threshold Comparison
<img width="841" height="395" alt="image" src="https://github.com/user-attachments/assets/c247988b-b9aa-442e-9bbe-08fc6a3cbc12" />


The final characterization combines the inverter VTC with the selected
transistor sizing conditions and the corresponding timing-related results.

The comparison demonstrates how modifications in transistor dimensions affect
the electrical response of the CMOS inverter.

An important CMOS design principle observed from this analysis is that the
relative drive strength of NMOS and PMOS devices influences the switching
behaviour and timing characteristics of the inverter.

Thus, transistor sizing, device strength and simulation response are closely
related. The final SPICE plots provide a clear way to interpret these
relationships.



---

# 8. Physical CMOS Layout
<img width="856" height="422" alt="image" src="https://github.com/user-attachments/assets/deac7de5-a1e9-4f0c-b73e-5bcdda8cd759" />

After completing the electrical analysis, the CMOS inverter can be translated
into a physical layout using the required CMOS technology rules.

The physical layout represents the actual geometric arrangement of the
transistors and their interconnections.

The layout includes important structures such as:

- NMOS active region
- PMOS active region
- Polysilicon gate
- Source and drain regions
- Contacts
- Local interconnect
- Metal connections
- Power and ground connections

The layout must follow the design rules provided by the SKY130A process design
kit.

The physical representation connects the transistor-level schematic with the
actual semiconductor structure that would be manufactured.



---

## CMOS Layout Structure

The physical CMOS inverter consists of complementary NMOS and PMOS devices
placed in their respective regions.

The polysilicon gate forms the common input connection, while the drain regions
are connected to form the inverter output.

The PMOS source is connected towards \(V_{DD}\), whereas the NMOS source is
connected towards \(V_{SS}\).



---

## Contacts & Local Interconnect

Contacts provide electrical connections between the diffusion regions,
polysilicon and metal layers.

Local interconnect is used to establish short electrical connections within
the standard-cell structure.

Proper placement of contacts and interconnects is necessary to obtain a
functional and design-rule-compliant layout.



---

## Higher-Level Metal

Higher metal layers are used for longer-distance routing and for connecting
the standard cell to external power, ground, input and output connections.

The metal structure allows the CMOS inverter to communicate with other cells
in a larger digital circuit.



---

## Complete CMOS Structure

The complete CMOS inverter combines the electrical circuit, physical layout
and fabrication concepts into one design flow.

The overall relationship can be represented as:

SPICE Circuit
↓
Electrical Simulation
↓
VTC and Switching Analysis
↓
Transistor Sizing
↓
Physical Layout
↓
CMOS Fabrication Structure

This demonstrates how a simple CMOS inverter moves from a transistor-level
circuit description to a physical semiconductor implementation.

<!-- INSERT YOUR IMAGE HERE -->

---
# 9. 🏭 CMOS FABRICATION PROCESS

The following sections explain the major stages involved in the 16-mask CMOS
fabrication sequence used to understand the physical formation of CMOS
transistors.

---

## 9.1 Active Region Formation

The first fabrication stage identifies and separates the silicon regions where
the MOS transistors will eventually be formed.

The structure consists of:

- P-type silicon substrate
- Silicon nitride layer
- Photoresist layer
- Field oxide
- LOCOS isolation
- Bird's-beak region

The isolation technique used in this process is LOCOS, which stands for
**Local Oxidation of Silicon**.

Field oxide separates the transistor active areas from the surrounding silicon
and prevents unwanted conduction between neighbouring devices.

This step is important because it establishes the physical regions in which
the active transistor structures will be fabricated.
<img width="846" height="387" alt="image" src="https://github.com/user-attachments/assets/76992ce8-1f67-466f-9418-e37ba10b07a7" />



---

## 9.2 N-Well and P-Well Formation

CMOS circuits require both NMOS and PMOS transistors. Therefore, suitable
well regions with different conductivity types must be created inside the
silicon substrate.

Ion implantation is used to introduce the required dopants into selected
areas.

The well-formation stage provides the required body regions for the two types
of MOS devices.

The implanted regions determine the electrical environment in which the NMOS
and PMOS transistors are subsequently constructed.

Proper well formation is essential for obtaining complementary transistor
operation in a CMOS circuit.

<img width="860" height="389" alt="image" src="https://github.com/user-attachments/assets/c8b52911-73ae-45c3-8170-18c71b653e77" />


---

## 9.3 Threshold Voltage & Body Effect

This stage introduces the physical and electrical factors that determine the
threshold voltage of a MOS transistor.

The threshold voltage is influenced by parameters such as:

- \(V_{T0}\) – threshold voltage at zero body bias
- \(\gamma\) – body-effect coefficient
- \(V_{SB}\) – source-to-body voltage
- \(\Phi_F\) – Fermi potential
- \(N_A\) – substrate doping concentration
- \(C_{ox}\) – oxide capacitance

The body effect occurs when the voltage difference between the source and body
changes the threshold voltage of the MOS device.

Therefore, transistor behaviour depends not only on the gate voltage but also
on substrate doping, oxide properties and body bias conditions.

Understanding these parameters is important for predicting the actual
operation of MOS devices.

<img width="849" height="375" alt="image" src="https://github.com/user-attachments/assets/76cc7b3b-9ce4-4374-a23d-f4151ff1499d" />


---

## 9.4 Gate Formation — Initial Stage

The next step in the fabrication sequence is the formation of the MOS gate
structure.

The gate acts as the controlling terminal of the transistor. By applying a
suitable voltage to the gate, the conductivity of the channel between source
and drain can be controlled.

The fabrication sequence at this stage involves the required gate-processing
and implantation operations over the previously prepared well regions.

The gate structure plays a central role in determining whether current can
flow through the transistor channel.


---

## 9.5 Gate Formation — Completed Structure

This stage represents the completed gate structure after the required
processing operations.

The gate is positioned above the channel region and separates the source and
drain regions.

The gate controls the formation of the conducting channel underneath it.
Therefore, the physical gate structure determines how the transistor responds
to an applied gate voltage.

At the end of this stage, the essential gate-controlled structure of the MOS
transistor has been established.

<!-- INSERT YOUR IMAGE HERE -->

---

## 9.6 LDD Formation — Initial Implantation

The Lightly Doped Drain (LDD) step introduces lightly doped regions near the
source and drain areas.

These regions are useful for controlling the electric-field intensity near
the drain.

LDD structures improve the reliability of the MOS transistor by reducing the
effect of strong electric fields near the drain junction.

Controlled implantation is therefore used to create the required lightly
doped regions around the transistor channel.

<!-- INSERT YOUR IMAGE HERE -->

---

## 9.7 LDD Formation — Phosphorus Implantation

Phosphorus implantation is carried out as part of the LDD formation process.

During ion implantation, dopant atoms are introduced into selected silicon
regions to obtain the required conductivity characteristics.

The implantation conditions determine the resulting dopant concentration and
depth.

This controlled doping step establishes the required lightly doped regions
for proper transistor operation and helps control electric-field effects near
the drain.

<!-- INSERT YOUR IMAGE HERE -->

---

## 9.8 Side-Wall Spacer Formation

After the LDD implantation, side-wall spacers are formed around the gate
structure.

These spacers create a controlled separation between the gate edge and the
heavily doped source/drain regions that are formed in the next stages.

The spacer dimensions determine the position of the heavily doped regions
relative to the gate.

Thus, side-wall spacer formation is important for obtaining the required
transistor geometry and maintaining proper source/drain alignment.

<!-- INSERT YOUR IMAGE HERE -->

---

## 9.9 Source & Drain Formation

The source and drain regions are formed after the spacer formation stage.

Higher-concentration doping is introduced into the selected regions to create
the final source and drain terminals.

High-temperature processing is used to activate and establish the required
doped regions.

The resulting MOS structure contains:

```text
             Gate
              |
        -------------
        |  Channel  |
        -------------
       Source     Drain
```


The source and drain provide the terminals through which current enters and leaves the transistor.
After this stage, the fundamental semiconductor structure required for MOS transistor operation is established.
�

## 9.10 Contacts & Local Interconnect — Titanium Deposition
Once the transistor structures are formed, electrical connections must be created between the device terminals.
At this stage, titanium is deposited over the wafer surface using a sputtering process.
The deposited material prepares the structure for forming electrical connections between the semiconductor regions and the interconnect system.
Contact formation is necessary because the source, drain and gate regions must eventually be connected to the external circuit wiring.
This stage therefore provides the transition from isolated transistor structures to electrically connected devices.


## 9.11 Contact Formation
The next fabrication step defines the contact regions required to connect the transistor terminals to the local interconnect structure.
The important terminals are:
Source
Drain
Gate
These contact regions provide conductive paths between the transistor structures and the metal wiring above them.
Once the contacts are formed, the individual transistor terminals become electrically accessible and can be connected as part of a larger CMOS circuit.


## 9.12 Higher-Level Metal Formation
The CMOS fabrication process continues by building additional metal interconnection levels above the contact structures.
These metal layers provide routing paths for:
Signal connections
Power distribution
Ground connections
Higher-level metal allows different transistor and standard-cell structures to be connected across the chip.
The interconnect hierarchy therefore transforms the individually fabricated devices into a complete and functional circuit network.
The final metal structure provides the required electrical connectivity for the completed CMOS implementation.


## 9.13 Complete CMOS Structure

The final fabrication stage combines the individual semiconductor and
interconnect layers into the completed CMOS structure.

The final structure contains:

- Silicon substrate
- N-well and P-well regions
- Active regions
- Gate structures
- Source and drain regions
- Contacts
- Local interconnect
- Higher-level metal layers

These layers together form the complete physical CMOS implementation.

The fabrication sequence demonstrates how the transistor structures and
interconnect layers are progressively built to transform the silicon substrate
into a functional CMOS structure.

The completed structure provides the physical foundation required for
connecting the CMOS devices into an integrated circuit.

<!-- INSERT YOUR IMAGE HERE -->

---

# 10. Layout and Abstract View

The conversion from the transistor-level circuit into a physical silicon
implementation begins with the standard-cell layout.

Using the SKY130A technology, the CMOS inverter is represented using
technology-specific physical layers required for fabrication and routing.

The important physical layers include:

- **Metal layers** – used for electrical routing.
- **Polysilicon** – forms the transistor gate structures.
- **Diffusion** – represents the active source and drain regions.
- **Contacts** – provide connections between different physical layers.
- **Well regions** – define the transistor body regions.
- **Power and ground rails** – distribute VDD and GND throughout the cell.

Along with the detailed layout, the abstract view provides a simplified
representation of the standard cell.

The abstract view contains the essential physical information required by the
digital physical-design flow while hiding unnecessary layout details.

The detailed layout and abstract representation together describe the
physical identity and connectivity of the standard cell.

<!-- INSERT YOUR IMAGE HERE -->

**Figure: Layout and abstract representation of the standard cell**

This stage provides the first physical representation of the circuit and
converts the transistor-level design into an organized silicon structure.

---

# 11. Defining the Cell Boundary

A standard cell requires a clearly defined physical area in which all of its
transistors and routing structures are placed.

After completing the layout, a cell boundary is created to specify the exact
region occupied by the standard cell.

The boundary determines the width and height of the cell and establishes the
physical area available for device placement and routing.

A properly defined cell boundary supports:

- Consistent cell dimensions
- Accurate placement
- Alignment with neighbouring cells
- Correct VDD and GND rail locations
- Compatibility with the standard-cell library

This organized structure allows multiple standard cells to be placed next to
one another while maintaining proper alignment.

The cell boundary therefore acts as the physical framework that allows the
standard cell to integrate with other cells in a larger digital design.

<!-- INSERT YOUR IMAGE HERE -->

**Figure: Defined standard-cell boundary**

---

# 12. Power and Ground Connectivity

After defining the cell structure, the power and ground connections are
established.

The CMOS cell uses two primary supply connections:

- **VDD** – provides the positive operating supply.
- **GND** – provides the ground or reference potential.

These supply rails are connected to the appropriate transistor regions through
the required physical layers.

In a CMOS inverter, the PMOS network is connected towards the supply side,
while the NMOS network is connected towards ground.

Proper routing ensures that both complementary transistor networks receive the
required power connections and operate correctly.

Reliable power connectivity is also necessary for maintaining the expected
physical structure of the standard-cell library.

<!-- INSERT YOUR IMAGE HERE -->

**Figure: Power and ground connections in the layout**

Power provides the energy required by the cell, while ground completes the
electrical return path required for CMOS operation.

---

# 13. Layout Extraction

A physical layout contains geometric information, while circuit simulation
requires an electrical representation.

Layout extraction provides the connection between these two forms.

After the layout is completed, the extraction process interprets the physical
shapes and converts them into an electrical circuit representation.

The extraction process identifies:

- Transistors present in the layout
- Electrical nodes
- Connections between devices
- Physical device dimensions
- Power and ground paths
- Parasitic elements

The extracted information can be used to generate a SPICE-compatible
representation of the implemented circuit.

Unlike an ideal schematic, the extracted representation contains information
obtained directly from the physical implementation.

This makes layout extraction useful for analysing the circuit after physical
implementation.

<!-- INSERT YOUR IMAGE HERE -->

**Figure: Extraction of the layout**

Layout extraction converts the physical geometry into electrical information
that can be used for circuit simulation.

---

# 14. Generating the Extracted Netlist

After layout extraction, the generated files are inspected to verify that the
physical layout has been correctly converted into electrical connectivity.

The extracted netlist provides a text-based description of the devices,
nodes, and connections identified from the layout.

It contains the information required to represent the physical implementation
for further simulation and analysis.

The generated files are checked to ensure that the required device and
connectivity information is available.

Typical outputs include extracted layout information and SPICE-compatible
netlist data.

The netlist acts as an electrical representation recovered from the physical
layout and describes how the extracted devices and connections are linked
together.

<!-- INSERT YOUR IMAGE HERE -->

**Figure: Generated extracted files and netlist**

---

# 15. Creating the SPICE File

The extracted information is converted into a SPICE file that can be used for
electrical simulation.

The SPICE file combines the device models, circuit connections, and simulation
parameters required by NGSPICE.

The SPICE representation contains:

- Technology and device model information
- Standard-cell subcircuit definition
- Input and output nodes
- VDD connection
- GND connection
- Extracted transistor information
- Simulation parameters

The extracted transistor and connectivity information is organized into an
appropriate subcircuit so that the physically implemented CMOS inverter can be
analysed electrically.

This step creates the simulation-ready representation of the extracted
physical circuit.

<!-- INSERT YOUR IMAGE HERE -->

---

# 16. Transient Simulation using NGSPICE

Once the SPICE representation is prepared, the extracted CMOS inverter is
simulated using NGSPICE.

Transient analysis applies a time-varying input signal and observes the
corresponding output response over time.

The circuit is operated using the required supply conditions while monitoring:

- Input
- Output
- VDD
- GND
The changing input signal allows the simulator to observe the switching
behaviour of the CMOS inverter.

The simulation also helps verify that the extracted circuit is correctly
connected and can be successfully simulated.

This stage connects the physical implementation back to measurable electrical
behaviour and confirms the operation of the extracted CMOS circuit.

<!-- INSERT YOUR IMAGE HERE -->
# 17. Input and Output Waveforms

The transient simulation produces input and output waveforms that provide
direct evidence of the CMOS inverter operation.

When the input alternates between LOW and HIGH, the output changes in the
opposite manner, as expected from a CMOS inverter.

| Input | Output |
|-------|--------|
| LOW   | HIGH   |
| HIGH  | LOW    |

The fundamental inverter relationship is:

**Output = NOT(Input)**

The output also approaches the expected supply and ground levels, confirming
that the extracted standard cell continues to provide the required digital
logic behaviour.

<!-- INSERT YOUR IMAGE HERE -->

**Figure: Simulated input and output transient waveforms**

The waveforms demonstrate the complementary relationship between the input
and output during inverter switching.

---

# 18. Physical Verification and Layout Analysis

After creating the layout, the physical structure is inspected to ensure
that the CMOS cell has been implemented correctly.

Important layers and connections are checked, including:

- Transistor regions
- Diffusion
- Polysilicon
- Contacts
- Metal interconnections
- Power network

The verification process checks for:

- Correct electrical connectivity
- Proper VDD and GND distribution
- Correct cell boundary
- Appropriate technology-layer usage
- Correct PMOS and NMOS arrangement

A successful physical layout must not only appear correct geometrically but
should also preserve the electrical function of the original circuit.

---

# 19. Standard Cell Layout Structure

The CMOS inverter follows the conventional organization used in standard-cell
design.

The PMOS network is placed in the upper portion of the cell and is connected
towards the VDD rail. The NMOS network is placed below it and connects
towards GND.

The input signal is connected to the transistor gates, while the output is
obtained from the shared node between the pull-up and pull-down networks.

This arrangement produces a compact and repeatable cell structure that can be
integrated with other standard cells in a larger digital design.

The physical organization directly reflects the logic structure:

- PMOS pulls the output upward.
- NMOS pulls the output downward.
- The shared node forms the inverter output.

---

# 20. Extraction and Parasitic Information

A completed layout contains more than ideal transistor connections.
Physical dimensions and interconnect geometry introduce additional electrical
effects.

During layout extraction, the physical shapes are converted into an
electrical representation so that these real-world effects can be considered
during simulation.

Extracted parasitic information can influence:

- Propagation delay
- Rise time
- Fall time
- Output transition speed
- Dynamic switching behaviour

Therefore, post-layout simulation provides a more realistic view of circuit
performance compared with an ideal schematic-level simulation.

---

# 21. SPICE Model and Device Parameters

The extracted CMOS inverter uses the device and technology information
provided by the SKY130A PDK.

The transistor models provide NGSPICE with the electrical parameters
necessary to reproduce MOS-device behaviour during simulation.

Combining the extracted layout information with technology-specific device
models creates a simulation that more closely represents the physically
implemented circuit instead of an ideal transistor-level model.

This provides a suitable basis for evaluating the standard cell before it is
integrated into a larger digital system.

---

# 22. Simulation Setup

Before transient simulation is performed, the extracted circuit must be
supplied with the required operating conditions and input signal.

The supply is connected between VDD and GND, while the inverter input
receives a time-dependent digital waveform.

The simulator then observes the response of the output node.

The main characteristics examined are:

- Correct logical operation
- Expected HIGH and LOW voltage levels
- Output switching transitions
- Timing characteristics
- Stable circuit response

These conditions provide the basis for analysing the behaviour of the
extracted CMOS inverter.

---

# 23. CMOS Inverter Operation

The CMOS inverter performs its logic function through the complementary
switching behaviour of PMOS and NMOS transistors.

## Input LOW

When the input is LOW:

- The PMOS transistor turns ON.
- The NMOS transistor turns OFF.
- The output is pulled towards VDD.
- The output becomes HIGH.

## Input HIGH

When the input changes to HIGH:

- The PMOS transistor turns OFF.
- The NMOS transistor turns ON.
- The output is pulled towards GND.
- The output becomes LOW.

Thus, the CMOS inverter always produces the logical complement of its input.

---

# 24. Rise and Fall Behaviour

The output of a CMOS inverter does not change between logic states
instantaneously.

When the input changes from LOW to HIGH, the output changes from HIGH to LOW.

Similarly, when the input changes from HIGH to LOW, the output moves from LOW
to HIGH.

The slope observed during these transitions is affected by the charging and
discharging of capacitances within the circuit.

Physical interconnections and extracted parasitic components can further
influence these transition characteristics.

Therefore, the rising and falling sections of the waveform provide useful
information about the dynamic performance of the implemented cell.

---

# 25. Timing Behaviour

Transient simulation provides information about how quickly the standard cell
responds to changes at its input.

Important timing parameters include:

- Rise time
- Fall time
- Propagation delay
- Input transition time
- Output transition time

These parameters become increasingly important when multiple standard cells
are connected to build larger digital systems.

Transistor dimensions, physical layout, load conditions, and parasitic effects
can all affect the final timing performance.

Functionality explains what the cell does, while timing explains how quickly
it performs the operation.

---

# 26. Voltage Levels

The simulated waveform is also checked to determine whether the inverter
reaches the expected logic voltage levels.

For correct CMOS operation:

- The HIGH output should approach the supply voltage.
- The LOW output should approach the ground voltage.

The voltage levels indicate whether the CMOS inverter is correctly producing
the required digital logic states.

The observed output levels can also be used to evaluate the quality of the
post-layout implementation.

---

# 27. Transistor Sizing and Performance

The physical dimensions of the PMOS and NMOS transistors significantly
influence CMOS inverter performance.

Changing transistor dimensions can affect:

- Drive strength
- Rise time
- Fall time
- Propagation delay
- Power consumption
- Switching characteristics

Proper sizing is therefore required to obtain a balanced response between the
pull-up and pull-down networks.

The dimensions selected during layout are also reflected in the extracted
circuit, allowing their effect to be observed during post-layout simulation.

---

# 28. Layout-to-Simulation Correlation

One of the main goals of this project is to establish a connection between the
physical implementation and the electrical behaviour of the circuit.

The complete process can be represented as:

**Circuit Design → Layout → Extraction → Netlist → SPICE Model → Simulation → Verification**

The layout represents the physical implementation of the CMOS inverter,
while extraction converts the physical geometry into electrical information.

The extracted netlist and SPICE model allow the physically implemented circuit
to be simulated using NGSPICE.

The simulation results can then be compared with the expected CMOS inverter
behaviour.

This correlation confirms that the physical layout, extracted electrical
representation, and simulated circuit behaviour are consistent with the
intended design.

---

# 🔑 Key Learnings

- Understood the working principle of a CMOS inverter using complementary PMOS and NMOS transistors.

- Learned how to perform SPICE and NGSPICE simulations to study CMOS circuit behaviour.

- Analysed input/output waveforms, voltage levels, rise time, fall time, and propagation delay.

- Studied how transistor sizing influences drive strength, switching speed, delay, and power consumption.

- Learned how to transform a circuit schematic into a physical CMOS standard-cell layout.

- Understood the importance of cell boundaries, layer arrangement, and standard-cell organization.

- Implemented and verified VDD and GND connections in the physical layout.

- Learned how layout extraction converts physical geometry into an electrical netlist.

- Understood the effect of parasitic elements on post-layout circuit behaviour.

- Gained practical experience with the SKY130A PDK, Magic VLSI, SPICE, and NGSPICE flow.

- Learned how to relate physical layout results with simulated electrical behaviour.

- Studied the 16-mask CMOS fabrication process, covering well formation through metallization.

- Understood the overall semiconductor design flow:

**Circuit Design → Simulation → Characterization → Layout → Extraction → Post-Layout Simulation → Fabrication**

- 🚀 Developed a broader understanding of how a transistor-level circuit is converted into a verified physical silicon implementation.

---

# 🎯 Conclusion

This project provided an end-to-end understanding of the CMOS inverter, beginning with transistor-level operation and continuing through physical layout, post-layout simulation, and CMOS fabrication.

The inverter was initially analysed as an electrical circuit to understand its logic operation and electrical characteristics. SPICE and NGSPICE simulations were used to examine input-output relationships, switching behaviour, voltage levels, timing characteristics, and the influence of transistor sizing.

The circuit was then implemented as a SKY130A standard-cell layout, converting the abstract transistor circuit into a physical structure consisting of diffusion, polysilicon, contacts, metal interconnects, wells, and power rails.

The completed layout was extracted into an electrical representation, establishing the important relationship between the physical structure on silicon and the behaviour observed during simulation. Post-layout analysis also demonstrated how physical effects and parasitic elements can influence circuit performance.

Finally, the study of the 16-mask CMOS fabrication process completed the overall journey by showing how carefully designed semiconductor structures can be converted into physical devices on a silicon wafer.



The changing input signal allows the simulator to observe the switching
behaviour of the CMOS inverter.

The simulation also helps verify that the extracted circuit is correctly
connected and can be successfully simulated.

This stage connects the physical implementation back to measurable electrical
behaviour and confirms the operation of the extracted CMOS circuit.

<!-- INSERT YOUR IMAGE HERE -->
