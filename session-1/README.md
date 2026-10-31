# Session 1 – RISC-V Simulation and Verification

## Overview

This session was carried out in GitHub Codespaces using a RISC-V based design. I compiled a C program, ran it on the Spike RISC-V simulator, studied the instructions that were generated, and then viewed the simulation waveform in GTKWave.

The goal was to understand the complete flow from source code to simulation, waveform analysis and synthesis.

---

## 1. Disassembling the Compiled Program

The compiled object file `sum1ton.o` was inspected with the `objdump` command.

Disassembly turns the machine code stored in an object file back into readable assembly, so we can see exactly which instructions the processor will run.

The screenshot shows several sections of the program, including `.plt` and `.text`. The `.text` section holds the executable instructions. Instructions such as `mov`, `push`, `pop`, `call`, `cmp`, `je`, `jmp` and `ret` can be seen; they perform operations and control the program flow.

### Key Takeaways

- Inspecting a compiled object file with `objdump`.
- Machine code can be viewed as assembly instructions.
- The `.text` section stores the executable code.
- Disassembly is useful for debugging and understanding compiler output.
- High-level C code is translated into low-level instructions.

### Screenshot

<img width="796" height="859" alt="image" src="https://github.com/user-attachments/assets/c90e4f93-2c32-4e93-b5a6-f5bde7198419?raw=true" />

---

## 2. Compiling and Running the Program

The first step was to compile the source program and produce the executable.

Using the terminal in GitHub Codespaces, I ran the compile commands and then executed the generated output.

### What is Compilation?

Compilation translates source code written in a programming language into machine-level instructions that the target processor can execute. For a RISC-V application, the compiler generates RISC-V instructions from the source code.

### Key Takeaways

- Working with the Codespaces terminal.
- Compiling a RISC-V program.
- Running the generated executable.
- Checking the program output from the terminal.

### Screenshot

<img width="951" height="526" alt="image" src="https://github.com/user-attachments/assets/d90b2681-51c2-4ec7-9a06-c90bdb05817a?raw=true" />

---

## 3. Running the Program on Spike

Spike is the RISC-V ISA simulator. It models a RISC-V processor in software, so programs can be executed and their behaviour observed without real hardware.

### What is Spike?

Spike is a functional simulator for RISC-V processors. It is widely used to verify instruction execution before hardware is available.

### Key Takeaways

- Running a RISC-V program on Spike.
- How an ISA simulator supports processor verification.
- Observing execution without physical hardware.

### Screenshot

<img width="304" height="543" alt="image" src="https://github.com/user-attachments/assets/5e7c9727-6854-4a86-a339-dcd9cd703ec5?raw=true" />

---

## 4. Program Execution and Output

Here the program was executed and the RISC-V instructions were observed in the terminal. The program adds a series of numbers and prints the final result:

**Sum = 45**

This matches the expected value, confirming that the program ran correctly. The terminal also lists RISC-V instructions such as `li`, `add`, `addi`, `sub`, `and`, `sll`, `srl` and `bne`.

### Key Takeaways

- How a program is turned into RISC-V instructions.
- How those instructions are executed.
- Verifying a program by checking its output.
- The program produced the expected **sum of 45**.

### Screenshot

<img width="962" height="538" alt="image" src="https://github.com/user-attachments/assets/469d94d3-1484-43c9-b202-203c927fd5f3?raw=true" />

---

## 5. Opening the Simulation Waveform

After simulation, the waveform file was opened in GTKWave, a viewer that displays digital signals against time.

It lets us watch how signals such as clock, reset, inputs and outputs change during the simulation.

### What is a Waveform?

A waveform is a graph of signal values over time. It is used to check whether a digital circuit behaves as intended.

### Key Takeaways

- Opening a simulation waveform.
- Identifying individual signals.
- Seeing how signal values change over time.
- Using waveforms to debug digital designs.

### Screenshot

<img width="960" height="544" alt="image" src="https://github.com/user-attachments/assets/1867dd35-47c4-4f6c-95d4-d5789b0fddba?raw=true" />

---

## 6. Waveform Analysis in GTKWave

The signals were then studied in more detail. The horizontal axis shows time, and each trace shows the logic value of a signal.

Common logic values:

- `0` – Logic LOW
- `1` – Logic HIGH
- `X` – Unknown
- `Z` – High impedance

By following the transitions, we can confirm whether the design gives the correct outputs for the applied inputs.

### Key Takeaways

Waveform analysis is a core part of RTL verification. It helps reveal wrong logic, timing issues and unexpected signal behaviour.

### Screenshot

<img width="548" height="603" alt="image" src="https://github.com/user-attachments/assets/8970d869-a703-4b9d-86ca-d22de8e5a38a?raw=true" />

---

## 7. Synthesized Design / Layout View

The last screenshot shows the design in a graphical view, representing the hardware structure produced after processing the RTL.

Synthesis converts RTL (Register Transfer Level) code into a gate-level netlist built from standard logic cells. Viewing the result shows how the RTL description becomes real hardware structures.

### What is Synthesis?

Synthesis is the process of mapping RTL code onto logic gates and standard cells. The synthesized netlist is then used in later physical design steps such as placement and routing.

### Key Takeaways

- How RTL code is converted into hardware.
- How synthesis produces a gate-level representation.
- Visually inspecting the generated design.
- The link between RTL, simulation, synthesis and physical implementation.

### Screenshot

<img width="339" height="557" alt="image" src="https://github.com/user-attachments/assets/50564238-e3f0-42e8-8994-90439ca19431?raw=true" />

---

# Conclusion

In Session 1, I learned the basic RISC-V design and verification flow in GitHub Codespaces. I compiled and ran a RISC-V program, simulated it with Spike, studied the assembly instructions, and analysed the resulting waveforms in GTKWave.

This session showed me how software instructions get executed, and how digital hardware designs are simulated, verified and synthesized.

