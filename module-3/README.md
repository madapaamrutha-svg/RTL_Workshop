 # 🔍 Module-3 Introduction to Combinational And Sequential Optimization
 ## Objectives
 
To understand the concept of logic optimization in digital circuits.
To study combinational and sequential logic optimization techniques.
To perform synthesis using the Yosys synthesis tool.
To map Verilog designs to the SKY130 standard-cell library.
To simulate Verilog designs using Icarus Verilog (Icarus Verilog).
To verify circuit behavior using GTKWave.
To analyze optimized gate-level netlists generated after synthesis.


1.Introduction to Logic Optimizations
Logic optimization reduces the hardware area, power consumption, and delay while preserving the original functionality of the design. In this module, combinational and sequential optimization techniques are studied using the SKY130 standard-cell library and Yosys synthesis tool.
📷 Image 1: Screenshot(69).png (Constant Propagation Example)
Result
The concept of constant propagation was studied to understand how synthesis tools simplify logic by replacing constant inputs.
2. 🔄 Sequential Logic Optimizations
Sequential logic optimization improves sequential circuits by optimizing registers and logic without changing circuit behavior. Techniques such as sequential constant propagation, retiming, and state optimization were introduced.
📷 Image 2: Screenshot(70).png (Sequential Logic Optimizations)
Result
The different sequential optimization techniques were studied to understand how they improve circuit performance and efficiency.

3. ⚙️ AND Gate Optimization (opt_check)
Verilog Code
module opt_check (
    input a,
    input b,
    output y
);

assign y = a & b;

endmodule
Yosys Commands
yosys
read_verilog opt_check.v
prep -top opt_check
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
📷 Image 3: opt check and gate mod3 start 1st.png
Result
The AND gate was successfully synthesized and mapped to the SKY130 and2 standard cell.
4. ⚙️ OR Gate Optimization (opt_check2)
Verilog Code
module opt_check2 (
    input a,
    input b,
    output y
);

assign y = a | b;

endmodule
Yosys Commands
yosys
read_verilog opt_check2.v
prep -top opt_check2
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
📷 Image 4: norgate mod3 2nd.png
Result
The OR gate was synthesized successfully and mapped to the SKY130 or2 standard cell.
5. ⚙️ Three-Input AND Gate Optimization (opt_check3)
Verilog Code
module opt_check3 (
    input a,
    input b,
    input c,
    output y
);

assign y = a & b & c;

endmodule
Yosys Commands
yosys
read_verilog opt_check3.v
prep -top opt_check3
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
📷 Image 5: 3ip and gate 3rd image module3.png
Result
The three-input AND gate was successfully synthesized and mapped to the SKY130 and3 standard cell.

4. Verilog Code for D Flip-Flop Constant Propagation
Description
This Verilog code demonstrates sequential constant propagation using two D Flip-Flop designs (dff_const1 and dff_const2). The output is assigned constant values to observe optimization during synthesis.
Code
// dff_const1.v
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
    if(reset)
        q <= 1'b0;
    else
        q <= 1'b1;
end
endmodule

// dff_const2.v
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
    if(reset)
        q <= 1'b1;
    else
        q <= 1'b1;
end
endmodule
Commands
vim dff_const1.v
vim dff_const2.v
Output
(Insert Image 4 here)
5. Simulation Waveform – dff_const1
Description
Simulation waveform showing the behavior of dff_const1. The output changes according to the reset signal.
Commands
iverilog -o dff_const1.out dff_const1.v dff_const1_tb.v
vvp dff_const1.out
gtkwave dump.vcd
Output
(Insert Image 5 here)
6. Simulation Waveform – dff_const2
Description
Simulation waveform of dff_const2 showing constant output after optimization.
Commands
iverilog -o dff_const2.out dff_const2.v dff_const2_tb.v
vvp dff_const2.out
gtkwave dump.vcd
Output
(Insert Image 6 here)
7. D Flip-Flop Netlist Before Optimization
Description
The synthesized netlist before applying sequential optimization.
Commands
yosys
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
show
Output
(Insert Image 7 here)
8. Sequential Logic Optimization Result
Description
The optimized circuit after sequential constant propagation. Redundant logic is removed by the synthesis tool.
Commands
yosys
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
show
Output
(Insert Image 8 here)

9. D Flip-Flop Constraint Simulation
Information
This experiment demonstrates the simulation of a D Flip-Flop with constant propagation. The waveform verifies the behavior of the flip-flop during reset and clock transitions.
Code
module dff_const3(input clk, input reset, output reg q);

always @(posedge clk)
begin
    if(reset)
        q <= 1'b0;
    else
        q <= 1'b1;
end

endmodule
Commands
iverilog -o dff_const3.out dff_const3.v dff_const3_tb.v

vvp dff_const3.out

gtkwave dff_const3.vcd
Output
Paste Image 9
10. Synthesized D Flip-Flop Circuit
Information
The D Flip-Flop design is synthesized using Yosys. The generated circuit is mapped to SKY130 standard cells.
Commands
yosys

read_verilog dff_const3.v

synth -top dff_const3

show
Output
Paste Image 10
11. Counter Optimization
Information
This experiment demonstrates optimization by removing unused outputs from a counter circuit.
Code
module counter_opt(input clk, input reset, output q);

reg [2:0] count;

assign q = count[0];

always @(posedge clk, posedge reset)
begin
    if(reset)
        count <= 3'b000;
    else
        count <= count + 1;
end

endmodule
Commands
yosys

read_verilog counter_opt.v

synth -top counter_opt

opt_clean

show
Output
Paste Image 11
12. Counter Optimization Result
Information
The synthesized counter retains only the required logic after optimization.
Commands
yosys

read_verilog counter_opt.v

synth -top counter_opt

show
Output
Paste Image 12
13. Optimized Counter Circuit
Information
The optimized gate-level implementation contains only the necessary flip-flops and logic.
Commands
write_verilog -noattr counter_opt_net.v

gvim counter_opt_net.v
Output
Paste Image 13
14. Optimized Counter Netlist
Information
The generated netlist shows the optimized hardware after synthesis.
Commands
write_verilog -noattr counter_opt_net.v

gvim counter_opt_net.v
Output
Paste Image 14
