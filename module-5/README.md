## 📌  Incomplete IF Statement
📖 Experiment Overview
This experiment demonstrates the behavior of an incomplete IF statement in Verilog HDL. An incomplete IF statement assigns the output only when a specific condition is satisfied, leaving the remaining conditions without any assignment. During RTL simulation, the output retains its previous value whenever the condition is false. During synthesis, this behavior results in latch inference, as the synthesis tool inserts a latch to preserve the previous output value. This experiment highlights the importance of assigning outputs under all possible conditions in combinational logic to avoid unintended hardware.
📝 Verilog RTL Code
module incom_if(
    input i0,
    input i1,
    input sel,
    output reg y
);

always @(*)
begin
    if(sel)
        y = i1;
end

endmodule
⚙️ Simulation Commands
vim incom_if.v

vim incom_if_tb.v

iverilog -o incom_if incom_if.v incom_if_tb.v

vvp incom_if

gtkwave incom_if.vcd
🖼️ Experimental Output
Image 1: RTL Simulation of Incomplete IF Statement
(Insert Image 1 here.)
📊 Observation
The output changes only when the select signal (sel) is high.
When sel is low, the output retains its previous value because no assignment is made.
This behavior indicates memory retention, which results in latch inference during synthesis.
The experiment demonstrates why complete conditional assignments are essential for combinational logic design.
✅ Result
The RTL simulation successfully demonstrated the behavior of an incomplete IF statement. The waveform confirmed that the output retains its previous value for unspecified conditions, illustrating latch inference caused by incomplete conditional assignments.

📌 Experiment 2 – RTL Schematic of Incomplete IF Statement
📖 Experiment Overview
This experiment focuses on the synthesis of the incomplete IF statement using the Yosys synthesis tool. During synthesis, the RTL description is analyzed to determine the required hardware implementation. Since the output is not assigned for every possible condition, the synthesis tool infers a latch to preserve the previous output value. The generated RTL schematic visually demonstrates how incomplete combinational logic results in unintended storage elements.
📝 Verilog RTL Code
module incom_if(
    input i0,
    input i1,
    input sel,
    output reg y
);

always @(*)
begin
    if(sel)
        y = i1;
end

endmodule
⚙️ Synthesis Commands
yosys

read_verilog incom_if.v

prep -top incom_if

show
🖼️ Experimental Output
Image 2: RTL Schematic of the Incomplete IF Statement
(Insert Image 2 here.)
📊 Observation
The RTL schematic contains a latch inferred by the synthesis tool.
The latch stores the previous output whenever the IF condition is not satisfied.
The synthesized circuit confirms that incomplete assignments introduce unintended memory elements.
This experiment emphasizes the importance of assigning outputs for all input conditions in combinational logic.
✅ Result
The synthesized RTL schematic successfully demonstrates latch inference caused by an incomplete IF statement. The generated hardware includes a latch, confirming that incomplete conditional assignments lead to unintended storage elements during synthesis.
📌 Experiment 3 – RTL Simulation of Incomplete IF Statement
📖 Experiment Overview
This experiment analyzes the RTL simulation waveform of an incomplete IF statement. The objective is to observe how the output behaves when all input conditions are not explicitly assigned. During simulation, whenever the specified condition is false, the output retains its previous value instead of changing immediately. This behavior indicates memory retention and is one of the primary reasons for latch inference during synthesis. The waveform generated using GTKWave helps verify the functional behavior of the RTL design.
📝 Verilog RTL Code
module incom_if(
input i0,
input i1,
input sel,
output reg y
);

always @(*)
begin
    if(sel)
        y = i1;
end

endmodule
⚙️ Simulation Commands
iverilog -o incom_if incom_if.v incom_if_tb.v

vvp incom_if

gtkwave incom_if.vcd
🖼️ Experimental Output
Image 3 – RTL Simulation Waveform of Incomplete IF Statement
(Paste Image 3 here.)
📊 Observation
The waveform shows that the output changes only when the select signal is active.
When the condition is false, the output retains its previous value.
This behavior confirms that the output is not assigned under all possible conditions.
The waveform clearly demonstrates the need for complete conditional assignments in combinational logic.
✅ Result
The RTL simulation successfully demonstrated the behavior of an incomplete IF statement. The waveform confirms that the output retains its previous value whenever no assignment is made, illustrating latch-like behavior that leads to latch inference during synthesis.

📌 Experiment 4 – RTL Schematic of Incomplete IF-ELSE Statement
📖 Experiment Overview
This experiment demonstrates the synthesis of an incomplete IF-ELSE statement using the Yosys synthesis tool. The RTL description is synthesized to observe how incomplete conditional assignments affect the generated hardware. Since the output is not assigned for every possible condition, the synthesis tool automatically infers a latch to preserve the previous output value. The generated RTL schematic clearly illustrates the impact of incomplete coding on hardware implementation.
📝 Verilog RTL Code
module incom_if2(
input i0,
input i1,
input sel,
output reg y
);

always @(*)
begin
    if(sel)
        y = i1;
    else if(!sel)
        y = i0;
end

endmodule
⚙️ Synthesis Commands
yosys

read_verilog incom_if2.v

prep -top incom_if2

show
🖼️ Experimental Output
Image 4 – RTL Schematic of Incomplete IF-ELSE Statement
(Paste Image 4 here.)
📊 Observation
The RTL schematic represents the synthesized hardware for the IF-ELSE design.
The synthesis process analyzes the conditional assignments and generates the corresponding logic.
The circuit implementation can be verified by comparing the RTL schematic with the Verilog description.
Proper conditional assignments help ensure predictable and optimized hardware generation.
✅ Result
The RTL schematic was successfully generated for the IF-ELSE design using Yosys. The synthesized circuit accurately represents the Verilog description and demonstrates the importance of correct conditional coding in digital circuit design.

## Experiment 4 – Incomplete Case Statement

### Overview
This experiment demonstrates the synthesis result of an **incomplete case statement**. Since not all possible input combinations are covered, the synthesis tool infers additional hardware (such as latches) to preserve the previous output value.

### Image 1 – Synthesized Netlist (Incomplete Case)
The synthesized circuit generated by Yosys shows the hardware implementation of the incomplete case statement. The presence of a latch indicates that the output is not assigned for every possible case, causing memory elements to be inferred during synthesis.

> 📷 **Insert Image 6 here**
### Result

The synthesized netlist shows that a latch is inferred because the case statement does not define outputs for all possible input conditions. This indicates incomplete combinational logic and may lead to synthesis-simulation mismatches.
### Image 2 – Simulation Waveform
The GTKWave simulation verifies the behavior of the incomplete case implementation. The output changes according to the defined case conditions, while retaining its previous value for undefined input combinations.

> 📷 **Insert Image 7 here**
### Result

The RTL simulation waveform verifies the behavior of the incomplete case statement. The output retains its previous value for undefined conditions, confirming latch behavior during simulation.

## Experiment 5 – Complete Case Statement

### Overview
This experiment demonstrates the synthesis of a **complete case statement**, where all possible input conditions are defined. This allows the synthesis tool to generate purely combinational logic without inferring latches.

### Image 1 – Synthesized Netlist (Complete Case)
The Yosys synthesized schematic shows a combinational implementation of the complete case statement. Since every input condition is covered, the design does not require storage elements.

> 📷 **Insert Image 8 here**
### Result

The synthesized design contains only combinational logic without any inferred latches. Since all input combinations are covered, the circuit is optimized for reliable synthesis and predictable hardware implementation.

## Experiment 6 – Partial Case Assignment

### Overview
This experiment demonstrates the effect of **partial assignments** inside a case statement. When the output is not assigned in every branch, synthesis infers latch-based storage to maintain the previous output value.

### Image 1 – Synthesized Netlist (Partial Assignment)
The synthesized circuit generated by Yosys includes latch elements because the output assignment is incomplete. This illustrates how partial assignments can unintentionally introduce sequential behavior into the design.

> 📷 **Insert Image 9 here**
### Result

The synthesis report indicates latch inference due to partially specified output assignments. Missing assignments force the synthesizer to preserve previous output values, resulting in sequential storage elements.

### Image 2 – Simulation Waveform
The GTKWave simulation confirms the synthesized behavior. The waveform shows that the output retains its previous value whenever an assignment is missing, matching the inferred latch behavior.

> 📷 **Insert Image 10 here**
### Result

The RTL simulation confirms the behavior of the partial case statement. The waveform shows that the output holds its previous state whenever the case statement does not assign a new value, demonstrating latch inference.
