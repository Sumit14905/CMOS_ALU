# CMOS_ALU
CMOS implementation of a 4-bit ALU in LTspice using 180 nm technology, featuring custom-designed logic gates, a 28T full adder, arithmetic and logic operations, and transistor-level simulation with waveform analysis.
# 1-Bit CMOS Arithmetic Logic Unit (ALU)
The Arithmetic Logic Unit (ALU) is one of the most important components of a digital processor, responsible for performing arithmetic and logical operations on binary data. In this project, a 1-bit CMOS ALU has been designed and simulated at the transistor level using 180 nm CMOS technology in LTspice.

Instead of implementing the complete ALU as a single transistor network, a hierarchical and modular design methodology has been adopted. Individual CMOS logic cells such as the AND gate, OR gate, XOR gate, Full Adder, and 4:1 Multiplexer were first designed and verified independently. These verified modules were then integrated to realize the complete ALU.

This modular approach improves readability, simplifies debugging, encourages design reuse, and allows the architecture to be easily extended to higher-bit ALUs.

# CMOS Design Considerations

The entire ALU is implemented using static CMOS logic, which consists of complementary Pull-Up Networks (PUN) formed by PMOS transistors and Pull-Down Networks (PDN) formed by NMOS transistors.

Static CMOS offers several advantages:

* Full rail-to-rail output voltage
* Negligible static power dissipation
* High noise immunity
* Reliable operation over a wide range of operating conditions
* Ease of cascading logic gates

  # Building Blocks

---

## 1. CMOS AND Gate

The CMOS AND gate is implemented using **static CMOS logic** in 180 nm technology. It produces a logic HIGH only when both input signals are HIGH. The design is realized using complementary pull-up (PMOS) and pull-down (NMOS) transistor networks, providing full voltage swing, low static power dissipation, and high noise immunity.

### Boolean Expression

\[
Y = A.B
\]

### Truth Table

| A | B | Y |
|:-:|:-:|:-:|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

---

### Circuit Schematic

<p align="center">
  <img src="Images/and_gate_schematic.png" width="700">
</p>

<p align="center">
<b>Figure 1.</b> Transistor-level CMOS implementation of the AND gate.
</p>

---

### Simulation Waveform

<p align="center">
  <img src="Images/and_gate_waveform.png" width="800">
</p>

<p align="center">
<b>Figure 2.</b> Transient response of the CMOS AND gate.
</p>

---


## 2. CMOS OR Gate

The CMOS OR gate is designed using complementary PMOS and NMOS transistor networks. It generates a logic HIGH whenever at least one input is HIGH.

### Boolean Expression

\[
Y = A + B
\]

### Truth Table

| A | B | Y |
|:-:|:-:|:-:|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

### Circuit Schematic

<p align="center">
<img src="Images/or_gate_schematic.png" width="700">
</p>

<p align="center">
<b>Figure 3.</b> CMOS OR Gate.
</p>

### Simulation Waveform

<p align="center">
<img src="Images/or_gate_waveform.png" width="800">
</p>

<p align="center">
<b>Figure 4.</b> Transient response of the CMOS OR gate.
</p>



---
## 4. 28-Transistor CMOS Full Adder

The Full Adder is the arithmetic core of the ALU. It performs one-bit binary addition using three inputs: **A**, **B**, and **Cin**. The implemented architecture uses 28 transistors and generates two outputs: **Sum** and **Carry Out (Cout)**.

### Equations

\[
Sum = A \oplus B \oplus Cin
\]

\[
Cout = AB + Cin(A \oplus B)
\]

### Circuit Schematic

<p align="center">
<img src="Images/fulladder_schematic.png" width="750">
</p>

<p align="center">
<b>Figure 7.</b> 28-Transistor CMOS Full Adder.
</p>

### Simulation Waveform

<p align="center">
<img src="Images/fulladder_waveform.png" width="900">
</p>

<p align="center">
<b>Figure 8.</b> Full Adder transient simulation.
</p>


---



## 5. CMOS 4:1 Multiplexer

The **4:1 Multiplexer (MUX)** serves as the output selection stage of the ALU. It selects one of the four functional outputs (SUM, AND, OR, and XOR) based on the two select inputs (**S1** and **S0**) and forwards the selected signal to the final ALU output.

Instead of implementing the 4:1 multiplexer directly at the transistor level, a **hierarchical design methodology** has been adopted. The circuit is constructed by interconnecting **three identical CMOS 2:1 Multiplexers**, allowing the verified 2:1 MUX design to be reused. This modular approach simplifies circuit design, verification, debugging, and future scalability.

---

### CMOS 2:1 Multiplexer

The CMOS 2:1 Multiplexer is the fundamental building block used to realize the 4:1 multiplexer. It selects one of two inputs according to the select signal (**S0**).

#### Boolean Expression

\[
Y=\overline{S_0}A+S_0B
\]

#### Truth Table

| S0 | Output |
|:--:|:------:|
| 0 | A |
| 1 | B |

#### Circuit Schematic

<p align="center">
<img src="Images/mux2_schematic.png" width="700">
</p>

<p align="center">
<b>Figure 9.</b> Transistor-level CMOS implementation of the 2:1 Multiplexer.
</p>

#### Simulation Waveform

<p align="center">
<img src="Images/mux2_waveform.png" width="850">
</p>

<p align="center">
<b>Figure 10.</b> Transient simulation of the CMOS 2:1 Multiplexer.
</p>


---

### Hierarchical Construction of the 4:1 Multiplexer

The complete 4:1 multiplexer is realized using **three CMOS 2:1 Multiplexer blocks** arranged in two stages.

- **MUX1** selects between **D0** and **D1** using **S0**.
- **MUX2** selects between **D2** and **D3** using **S0**.
- **MUX3** selects between the outputs of MUX1 and MUX2 using **S1** to generate the final output.

This hierarchical implementation demonstrates the modularity and reusability of CMOS logic design.

#### Block Diagram

<p align="center">
<img src="Images/mux4_block_diagram.png" width="700">
</p>

<p align="center">
<b>Figure 11.</b> Hierarchical implementation of the 4:1 Multiplexer using three CMOS 2:1 Multiplexers.
</p>

---

#### Transistor-Level Circuit

<p align="center">
<img src="Images/mux4_schematic.png" width="700">
</p>

<p align="center">
<b>Figure 12.</b> Transistor-level CMOS implementation of the 4:1 Multiplexer.
</p>

---

### Selection Table

| S1 | S0 | Selected Input |
|:--:|:--:|:--------------:|
| 0 | 0 | D0 |
| 0 | 1 | D1 |
| 1 | 0 | D2 |
| 1 | 1 | D3 |

---

#### Simulation Waveform

<p align="center">
<img src="Images/mux4_waveform.png" width="850">
</p>

<p align="center">
<b>Figure 13.</b> Transient simulation of the CMOS 4:1 Multiplexer.
</p>

