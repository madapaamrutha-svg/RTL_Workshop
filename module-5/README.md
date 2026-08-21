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

📌 Experiment 5 – Incomplete CASE Statement
📖 Experiment Overview
This experiment demonstrates the behavior of an incomplete CASE statement in Verilog HDL. A CASE statement is commonly used to implement combinational logic with multiple input conditions. If all possible case values are not specified and no default case is provided, the output remains unchanged for the uncovered conditions. During synthesis, the tool infers a latch to preserve the previous output value. This experiment highlights the importance of covering all possible input combinations to avoid unintended latch inference and ensure reliable hardware implementation.
📝 Verilog RTL Code
module incom_case(
input i0,
input i1,
input i2,
input [1:0] sel,
output reg y
);

always @(*)
begin
    case(sel)
        2'b00 : y = i0;
        2'b01 : y = i1;
        2'b10 : y = i2;
    endcase
end

endmodule
⚙️ Simulation Commands
vim incom_case.v

vim incom_case_tb.v

iverilog -o incom_case incom_case.v incom_case_tb.v

vvp incom_case

gtkwave incom_case.vcd
🖼️ Experimental Output
Image 5 – RTL Simulation of Incomplete CASE Statement
(Paste Image 5 here.)
📊 Observation
The waveform shows the behavior of the CASE statement for different select inputs.
Since the CASE statement does not include all possible input combinations and no default case is provided, the output retains its previous value for uncovered conditions.
This behavior results in latch inference during synthesis.
The experiment demonstrates the importance of writing complete CASE statements in combinational logic.
✅ Result
The simulation successfully demonstrated the behavior of an incomplete CASE statement. The waveform confirms that missing case conditions cause the output to retain its previous value, leading to latch inference during synthesis. This emphasizes the importance of including all possible case values or a default case in Verilog designs.





