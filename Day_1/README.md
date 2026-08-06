# Day 1: Introduction to Verilog RTL Design & Synthesis

## Overview
Welcome to Day 1 of the RTL Design Workshop. In this session, I learned the basics of Verilog RTL Design, simulation using Icarus Verilog (iverilog), waveform analysis using GTKWave, and logic synthesis using Yosys.

---

## Table of Contents
1. What is a Simulator, Design, and Testbench?
2. Getting Started with Iverilog
3. Lab: Simulating a 2-to-1 Multiplexer
4. Verilog Code Analysis
5. Introduction to Yosys & Gate Libraries
6. Synthesis using Yosys
7. Summary

---

# 1. What is a Simulator, Design, and Testbench?

## Simulator
A simulator is a software tool used to verify the functionality of a digital circuit before hardware implementation.

## Design
The design is the Verilog code that describes the required hardware functionality.
<img width="880" height="556" alt="6d5a017b-25ac-44ad-a186-e54d5fedb3fc" src="https://github.com/user-attachments/assets/022fdf42-a030-4252-826c-c7e68716bc98" />




## Testbench
A testbench provides different input combinations to verify whether the design produces the expected outputs.
<img width="976" height="556" alt="5a3dc0d0-1386-440f-bc1d-d6aabb3a5c63" src="https://github.com/user-attachments/assets/34b40dc2-47be-496a-8a5f-a8b135d372df" />



# 2. Getting Started with Iverilog

Iverilog is an open-source Verilog simulator.

Simulation Flow:

Design + Testbench → Iverilog → VCD File → GTKWave

<img width="1080" height="640" alt="8063fea1-a7b5-44a6-bacd-73d3d8463bd5" src="https://github.com/user-attachments/assets/b6870a1b-47f9-4177-8bd5-7be55b810925" />


# 3. Lab: Simulating a 2-to-1 Multiplexer

## Step 1: Install Required Tools

```bash
sudo apt install iverilog
sudo apt install gtkwave
```

## Step 2: Compile

```bash
iverilog good_mux.v tb_good_mux.v
```

## Step 3: Run Simulation

```bash
./a.out
```

## Step 4: View Waveform

```bash
gtkwave tb_good_mux.vcd
```

**Image: GTKWave Output**
<img width="1920" height="940" alt="mux wave" src="https://github.com/user-attachments/assets/0bd68e56-52d8-40ad-b0bb-f821ed3408aa" />

---

# 4. Verilog Code Analysis

## Multiplexer Code

<img width="1080" height="616" alt="b027b3d7-04f8-4027-bc3b-aa204b61ed2d" src="https://github.com/user-attachments/assets/6f7f7336-5aeb-4c19-a707-8df1903213c2" />

   

### Explanation
- Inputs: i0, i1
- Select Line: sel
- Output: y
- If sel = 1, output = i1
- If sel = 0, output = i0



# 7. Summary

- Learned Verilog RTL basics.
- Understood Simulator, Design, and Testbench.
- Simulated a 2:1 Multiplexer using Iverilog.
- Viewed waveform using GTKWave.
