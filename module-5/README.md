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
