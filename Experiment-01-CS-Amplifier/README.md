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
- Gain approximately equals −gmRD  
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
<img src="https://github.com/jeevankamsagar-2006/Jeevan_Kamsagar_H_LIC/blob/e47105fa44cfbfe675f905352982fe2524b36743/Experiment-01-CS-Amplifier/dc-analysis.jpeg" width="750">
</p>

<p align="center">
Figure: Common Source Amplifier Circuit in LTSpice
</p>

---

# DC ANALYSIS

## 1. Power Constraint Derivation

The total DC power consumption is:

<p align="center">
P = V<sub>DD</sub> × I<sub>D</sub>
</p>

Given:

<p align="center">
P ≤ 1 mW
</p>

Maximum allowable drain current:

<p align="center">
I<sub>D(max)</sub> = P / V<sub>DD</sub>
</p>

Substituting values:

<p align="center">
I<sub>D(max)</sub> = (1 × 10<sup>−3</sup>) / 1.8
</p>

<p align="center">
I<sub>D(max)</sub> = 555.5 µA
</p>

---

## 2. Selection of Design Drain Current

To maintain safe margin and stable operation:

<p align="center">
I<sub>D</sub> = 200 µA
</p>

Power consumption:

<p align="center">
P = 1.8 × 200 × 10<sup>−6</sup>
</p>

<p align="center">
P = 360 µW
</p>

This satisfies the power constraint.

---

## 3. Output Voltage Selection

For maximum symmetrical swing:

<p align="center">
V<sub>DS</sub> ≈ V<sub>DD</sub> / 2
</p>

<p align="center">
V<sub>DS</sub> = 1.8 / 2 = 0.9 V
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
R<sub>D</sub> = 0.9 / 0.0002
</p>

<p align="center">
R<sub>D</sub> = 4500 Ω
</p>

Final value:

**RD = 4.5 kΩ**

---

## 5. Saturation Verification

Saturation condition:

<p align="center">
V<sub>DS</sub> ≥ V<sub>GS</sub> − V<sub>T</sub>
</p>

Choose:

<p align="center">
V<sub>GS</sub> = 0.9 V
</p>

<p align="center">
V<sub>GS</sub> − V<sub>T</sub> = 0.9 − 0.366
</p>

<p align="center">
V<sub>GS</sub> − V<sub>T</sub> = 0.534 V
</p>

Since:

<p align="center">
0.9 > 0.534
</p>

The MOSFET operates in the saturation region.

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

Gain in dB:

<p align="center">
20 log<sub>10</sub>(3.37) = 10.55 dB
</p>

---

## DC Simulation Result

<p align="center">
<img src="Experiment-01-CS-Amplifier/dc-analysis.jpeg" width="750">
</p>

<p align="center">
Figure: DC Operating Point Result
</p>

---

# TRANSIENT ANALYSIS

## Input Signal

SINE(0.9 10m 1k)

- DC offset = 0.9 V  
- Amplitude = 10 mV  
- Frequency = 1 kHz  

Small signal condition:

<p align="center">
10 mV << 0.534 V
</p>

Valid small-signal operation.

---

## Measured Gain

<p align="center">
A<sub>v</sub> = V<sub>out(pp)</sub> / V<sub>in(pp)</sub>
</p>

Expected gain ≈ 3.3

---

## Transient Results

<p align="center">
<img src="Experiment-01-CS-Amplifier/transient%201.jpeg" width="750">
</p>

<p align="center">
Figure: Transient Response – Waveform 1
</p>

<p align="center">
<img src="Experiment-01-CS-Amplifier/transient%202.jpeg" width="750">
</p>

<p align="center">
Figure: Transient Response – Waveform 2
</p>

The output waveform is inverted and amplified, confirming CS operation.

---

# AC ANALYSIS

## AC Setup

- AC amplitude = 1  
- Command: `.ac dec 100 1 1G`

Plot:

V(vout) / V(vin)

---

## 3dB Frequency Calculation

<p align="center">
f<sub>3dB</sub> = 1 / (2π R<sub>D</sub> C<sub>L</sub>)
</p>

<p align="center">
f<sub>3dB</sub> = 1 / (2π × 4500 × 10pF)
</p>

<p align="center">
f<sub>3dB</sub> = 3.53 MHz
</p>

---

## Unity Gain Bandwidth

<p align="center">
UGB = A<sub>v</sub> × f<sub>3dB</sub>
</p>

<p align="center">
UGB = 3.37 × 3.53
</p>

<p align="center">
UGB = 11.9 MHz
</p>

---

## AC Results

<p align="center">
<img src="Experiment-01-CS-Amplifier/ac-analysis%201.jpeg" width="750">
</p>

<p align="center">
Figure: AC Frequency Response – Plot 1
</p>

<p align="center">
<img src="Experiment-01-CS-Amplifier/ac-analysis%202.jpeg" width="750">
</p>

<p align="center">
Figure: AC Frequency Response – Plot 2
</p>

---

# Comparison Between Theory and Simulation

Minor differences occur due to:

- Channel length modulation  
- Finite output resistance  
- Parasitic capacitances  
- Mobility degradation  
- BSIM physical model effects  

The theoretical model assumes ideal square-law behavior.

---

# Results Table

| Parameter | Value |
|-----------|--------|
| ID | **200 µA** |
| RD | **4.5 kΩ** |
| gm | **0.749 mS** |
| Gain | **−3.37** |
| Gain (dB) | **10.55 dB** |
| 3dB Frequency | **3.53 MHz** |
| Unity Gain Bandwidth | **11.9 MHz** |

---

# Inference

The Common Source amplifier was successfully designed under the given power constraint. The transistor operates in saturation ensuring linear amplification. The theoretical and simulated gains closely match. The bandwidth is governed by the RC network at the drain node.

---

# Conclusion

The CS amplifier using TSMC 180nm technology was successfully designed and analyzed. DC biasing, transient amplification, and AC frequency behavior were verified. The experiment demonstrates the relationship between bias current, gain, and bandwidth in analog CMOS design.
