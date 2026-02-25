# LIC LAB  
# EXPERIMENT 01  
# DESIGN AND ANALYSIS OF COMMON SOURCE (CS) AMPLIFIER  
# TSMC 180nm TECHNOLOGY  

---

# Introduction

The Common Source (CS) amplifier is one of the most fundamental building blocks in analog CMOS circuit design. In this configuration, the source terminal is common to both the input and output. The input signal is applied at the gate terminal, and the output is taken from the drain terminal.

When the MOSFET operates in the saturation region, it behaves as a voltage-controlled current source. A small variation in gate-to-source voltage produces a proportional variation in drain current. This varying drain current flowing through the drain resistor generates an amplified voltage at the output node.

Key characteristics of a CS amplifier:

- Provides voltage amplification  
- Produces 180° phase inversion  
- Gain approximately equals −gₘRᴰ  
- High input impedance  
- Bandwidth controlled by output RC network  

Proper DC biasing ensures the transistor remains in saturation during the entire input signal swing.

---

# Aim

To design and analyze a Common Source amplifier using TSMC 180nm CMOS technology in LTSpice with:

- Supply voltage VDD = 1.8V  
- Power constraint ≤ 1mW  
- Channel length L = 560nm  
- Load capacitance CL = 10pF  

And to evaluate:

- DC Operating Point  
- Transient Response  
- AC Frequency Response  
- Voltage Gain  
- Bandwidth  
- Unity Gain Bandwidth  

---

# Given Parameters

- VDD = 1.8 V  
- Power constraint P ≤ 1 mW  
- Channel length L = 560 nm  
- Threshold voltage VT = 0.366 V  
- Load capacitance CL = 10 pF  

---

# Circuit Diagram

<p align="center">
<img src="https://github.com/jeevankamsagar-2006/Jeevan_Kamsagar_H_LIC/blob/58adf187a181793e98582104eff58aaa8e2d0759/Experiment-01-CS-Amplifier/dc-analysis.jpeg" width="750">
</p>

<p align="center">
Figure: Common Source Amplifier Circuit in LTSpice
</p>

---

# DC ANALYSIS

## 1. Power Constraint Derivation

<p align="center">
P = V<sub>DD</sub> × I<sub>D</sub>
</p>

Given:

<p align="center">
P ≤ 1 mW
</p>

<p align="center">
I<sub>D(max)</sub> = P / V<sub>DD</sub>
</p>

<p align="center">
I<sub>D(max)</sub> = (1 × 10<sup>−3</sup>) / 1.8
</p>

<p align="center">
I<sub>D(max)</sub> = 555.5 µA
</p>

---

## 2. Selection of Design Drain Current

Chosen:

<p align="center">
I<sub>D</sub> = 200 µA
</p>

<p align="center">
P = 1.8 × 200 × 10<sup>−6</sup>
</p>

<p align="center">
P = 360 µW
</p>

Power constraint satisfied.

---

## 3. Output Voltage Selection

<p align="center">
V<sub>DS</sub> ≈ V<sub>DD</sub> / 2
</p>

<p align="center">
V<sub>DS</sub> = 0.9 V
</p>

---

## 4. Drain Resistance Calculation

<p align="center">
R<sub>D</sub> = (V<sub>DD</sub> − V<sub>DS</sub>) / I<sub>D</sub>
</p>

<p align="center">
R<sub>D</sub> = (1.8 − 0.9) / (200 × 10<sup>−6</sup>)
</p>

<p align="center">
R<sub>D</sub> = 4500 Ω
</p>

**RD = 4.5 kΩ**

---

## 5. Saturation Verification

<p align="center">
V<sub>DS</sub> ≥ V<sub>GS</sub> − V<sub>T</sub>
</p>

<p align="center">
V<sub>GS</sub> − V<sub>T</sub> = 0.9 − 0.366 = 0.534 V
</p>

<p align="center">
0.9 > 0.534
</p>

Device operates in saturation.

---

## 6. Transconductance Calculation

<p align="center">
g<sub>m</sub> = 2I<sub>D</sub> / (V<sub>GS</sub> − V<sub>T</sub>)
</p>

<p align="center">
g<sub>m</sub> = (2 × 200 × 10<sup>−6</sup>) / 0.534
</p>

<p align="center">
g<sub>m</sub> = 0.749 mS
</p>

---

## 7. Theoretical Voltage Gain

<p align="center">
A<sub>v</sub> = −g<sub>m</sub> R<sub>D</sub>
</p>

<p align="center">
A<sub>v</sub> = − (0.749 × 10<sup>−3</sup>) × 4500
</p>

<p align="center">
A<sub>v</sub> = −3.37
</p>

<p align="center">
Gain (dB) = 20 log<sub>10</sub>(3.37) = 10.55 dB
</p>

---

## DC Simulation Result

<p align="center">
I<sub>D(sim)</sub> = 201.649 µA  
</p>

<p align="center">
V<sub>out(sim)</sub> = 0.9074 V  
</p>

Drain current error:

<p align="center">
0.824 %
</p>

Output voltage error:

<p align="center">
0.82 %
</p>

Agreement within 1%.

---

# TRANSIENT ANALYSIS

## Input Signal

SINE(0.9 10m 1k)

<p align="center">
10 mV << 0.534 V
</p>

Valid small-signal condition.

---

## Gain Comparison

Theoretical:

<p align="center">
A<sub>v</sub> = −3.37
</p>

Simulated:

<p align="center">
A<sub>v(sim)</sub> ≈ −3.3
</p>

Gain error:

<p align="center">
≈ 2.07 %
</p>

Reason:

<p align="center">
A<sub>v</sub> = −g<sub>m</sub> (R<sub>D</sub> || r<sub>o</sub>)
</p>

Finite output resistance reduces gain slightly.

---

## Transient Waveforms

<p align="center">
<img src="https://github.com/jeevankamsagar-2006/Jeevan_Kamsagar_H_LIC/blob/58adf187a181793e98582104eff58aaa8e2d0759/Experiment-01-CS-Amplifier/transient%201.jpeg" width="750">
</p>

<p align="center">
<img src="https://github.com/jeevankamsagar-2006/Jeevan_Kamsagar_H_LIC/blob/58adf187a181793e98582104eff58aaa8e2d0759/Experiment-01-CS-Amplifier/transient%202.jpeg" width="750">
</p>

Output is inverted and amplified.

---

# AC ANALYSIS

## 3dB Frequency (Theory)

<p align="center">
f<sub>3dB</sub> = 1 / (2π R<sub>D</sub> C<sub>L</sub>)
</p>

<p align="center">
f<sub>3dB</sub> = 3.53 MHz
</p>

---

## Simulated 3dB Frequency

<p align="center">
f<sub>3dB(sim)</sub> ≈ 3.2 – 3.6 MHz
</p>

---

## Unity Gain Bandwidth

<p align="center">
UGB = A<sub>v</sub> × f<sub>3dB</sub>
</p>

<p align="center">
UGB = 3.37 × 3.53 = 11.9 MHz
</p>

Simulated:

<p align="center">
≈ 11 – 12 MHz
</p>

---

## AC Plots

<p align="center">
<img src="https://github.com/jeevankamsagar-2006/Jeevan_Kamsagar_H_LIC/blob/58adf187a181793e98582104eff58aaa8e2d0759/Experiment-01-CS-Amplifier/ac-analysis%201.jpeg" width="750">
</p>

<p align="center">
<img src="https://github.com/jeevankamsagar-2006/Jeevan_Kamsagar_H_LIC/blob/58adf187a181793e98582104eff58aaa8e2d0759/Experiment-01-CS-Amplifier/ac-analysis%202.jpeg" width="750">
</p>

---

# Reasons for Practical Variations

Differences arise due to:

- Channel length modulation  
- Finite output resistance  
- Gate-drain capacitance (Miller effect)  
- Drain-bulk capacitance  
- Mobility degradation  
- Velocity saturation  
- Advanced BSIM model effects  

Total output capacitance:

<p align="center">
C<sub>total</sub> = C<sub>L</sub> + C<sub>gd</sub> + C<sub>db</sub>
</p>

Effective capacitance slightly increases, shifting pole frequency.

---

# Final Results Table

| Parameter | Theory | Simulation | Error |
|-----------|----------|------------|--------|
| ID | 200 µA | 201.649 µA | 0.82% |
| RD | 4.5 kΩ | 4.5 kΩ | 0% |
| gm | 0.749 mS | ≈0.74 mS | ~1% |
| Gain | −3.37 | −3.3 | 2.07% |
| 3dB Freq | 3.53 MHz | ≈3.3 MHz | <5% |
| UGB | 11.9 MHz | ≈11–12 MHz | <5% |

---

# Inference

The Common Source amplifier satisfies the power constraint and operates in the saturation region. Theoretical and simulated values closely match. Minor deviations are due to physical non-idealities included in the BSIM device model. The bandwidth is controlled by the RC network at the drain node.

---

# Conclusion

The Common Source amplifier using TSMC 180nm technology was successfully designed and validated. DC biasing, transient gain, and AC frequency response confirm correct amplifier operation. The experiment demonstrates the direct relationship between bias current, gain, and bandwidth in CMOS analog circuit design.
