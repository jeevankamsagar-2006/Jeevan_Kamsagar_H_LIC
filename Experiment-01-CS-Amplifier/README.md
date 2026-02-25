# LIC LAB  
# EXPERIMENT 01  
# DESIGN AND ANALYSIS OF COMMON SOURCE (CS) AMPLIFIER  
Technology: TSMC 180 nm  
Supply Voltage: 1.8 V  

---

# AIM

To design and analyze a Common Source (CS) amplifier using TSMC 180 nm MOSFET technology in LTSpice under a 1.8 V supply, satisfying the given power constraint, and to determine:

- DC Operating Point  
- Drain Current (ID)  
- Drain Resistance (RD)  
- Transistor Width (W)  
- Voltage Gain (Theoretical and Simulated)  
- Gain in dB  
- 3 dB Frequency  
- Bandwidth  
- Unity Gain Bandwidth  

---

# INTRODUCTION TO COMMON SOURCE AMPLIFIER

The Common Source amplifier is one of the most fundamental voltage amplification configurations using a MOSFET. In this topology:

- Source is grounded  
- Input is applied at the gate  
- Output is taken from the drain  

When the MOSFET operates in the saturation region, it behaves like a voltage-controlled current source. A small change in gate voltage produces a proportional change in drain current. This varying drain current produces an amplified voltage across the drain resistor.

Key characteristics of CS amplifier:

- Provides voltage gain  
- Produces 180° phase inversion  
- Gain depends on transconductance (gm) and drain resistance (RD)  
- High frequency behavior dominated by output node capacitance  

Correct biasing is critical. The transistor must remain in saturation throughout signal swing.

---

# GIVEN PARAMETERS

Technology: TSMC 180 nm  
VDD = 1.8 V  
Power constraint ≤ 1 mW  
Channel length L = 560 nm  
Threshold voltage VT ≈ 0.366 V  
Load capacitor CL = 10 pF  

---

# CIRCUIT DIAGRAM

<center>

[PASTE YOUR LTSPICE CIRCUIT IMAGE HERE]

</center>

Figure 1: Designed CS Amplifier in LTSpice

---

# DC ANALYSIS – Q POINT DESIGN

## Step 1: Power Constraint

Power:

P = VDD × ID  

Given maximum power:

P ≤ 1 mW  

Therefore:

ID ≤ 1×10⁻³ / 1.8  

ID ≤ 555.5 µA  

To stay within limit and obtain good gain, choose:

ID = 400 µA  

---

## Step 2: Selecting Proper Operating Voltage

For maximum symmetrical output swing:

VDS ≈ VDD / 2  

VDS = 1.8 / 2  

VDS = 0.9 V  

---

## Step 3: Calculating Drain Resistance

RD = (VDD − VDS) / ID  

RD = (1.8 − 0.9) / (400 × 10⁻⁶)  

RD = 0.9 / 0.0004  

RD = 2250 Ω  

So,

RD = 2.25 kΩ  

---

## Step 4: Saturation Condition Check

Saturation condition:

VDS ≥ VGS − VT  

Choose:

VGS = 0.9 V  

Then:

VGS − VT = 0.9 − 0.366  

VGS − VT = 0.534 V  

Since:

0.9 > 0.534  

The MOSFET operates in saturation.

---

## Step 5: Transistor Width Calculation

Drain current equation in saturation:

ID = (1/2) μn Cox (W/L) (VGS − VT)²  

Rearranging:

W = (2 ID L) / [μn Cox (VGS − VT)²]  

Substituting values:

ID = 400 µA  
L = 560 nm  

Calculated width:

W ≈ 6.67 µm  

After simulation adjustment to match ID:

Final width used:

W = 9.08 µm  

This correction accounts for second-order effects in the SPICE model.

---

# DC OPERATING POINT RESULTS

<center>

[PASTE YOUR DC OPERATING POINT IMAGE HERE]

</center>

From simulation:

V(vin) ≈ 0.9 V  
V(vout) ≈ 0.90005 V  

The output node centered at 0.9 V confirms correct Q-point biasing.

---

# TRANSIENT ANALYSIS

## Input Signal

SINE(0.9 10m 1k)

DC Offset = 0.9 V  
Amplitude = 10 mV  
Frequency = 1 kHz  

Small signal condition:

Amplitude (10 mV) << Overdrive voltage (0.534 V)  

Therefore small signal model is valid.

---

## Measured Values

Vin(pp) = 19.237 mV  
Vout(pp) = 63.997 mV  

Voltage Gain:

Av = 63.997 / 19.237  

Av = 3.326  

Gain in dB:

Av(dB) = 20 log₁₀(3.326)  

Av(dB) ≈ 10.438 dB  

---

<center>

[PASTE YOUR TRANSIENT WAVEFORM IMAGE HERE]

</center>

The waveform confirms:

- Amplification  
- 180° phase inversion  

---

# THEORETICAL GAIN

For CS amplifier:

Av = −gm RD  

Where:

gm = 2ID / (VGS − VT)  

gm = (2 × 400×10⁻⁶) / 0.534  

gm = 1.498 × 10⁻³ S  

Thus:

Av = 1.498×10⁻³ × 2250  

Av ≈ 3.37  

In dB:

Av ≈ 10.55 dB  

---

## Difference Between Theory and Simulation

Simulated gain: 3.326  
Theoretical gain: 3.37  

Small deviation occurs due to:

- Channel length modulation  
- Parasitic capacitances  
- Mobility degradation  
- Non-ideal SPICE model  

The theoretical model assumes ideal square-law behavior.

---

# AC ANALYSIS – FREQUENCY RESPONSE

AC command used:

.ac dec 100 1 1G  

AC input magnitude:

AC 1  

Plot:

V(vout)/V(vin)

---

# AC RESPONSE WITHOUT LOAD CAPACITOR

<center>

[PASTE AC PLOT WITHOUT 10pF IMAGE HERE]

</center>

From simulation:

f3dB = 1.3051 GHz  

Since single dominant pole:

BW = 1.3051 GHz  

Because parasitic capacitance is small (~50 fF), pole frequency is very high.

---

# AC RESPONSE WITH LOAD CAPACITOR (CL = 10 pF)

<center>

[PASTE AC PLOT WITH 10pF IMAGE HERE]

</center>

From simulation:

f3dB = 7.328 MHz  

Therefore:

BW = 7.328 MHz  

Unity Gain Bandwidth:

UGB ≈ 23–24 MHz  

---

# UNITY GAIN VERIFICATION

UGB = Av × f3dB  

UGB = 3.326 × 7.328 MHz  

UGB ≈ 24.37 MHz  

Matches closely with simulated value.

---

# DOMINANT POLE EXPLANATION

Dominant pole formed by:

RD and Total Output Capacitance  

Pole frequency:

fp = 1 / (2π RD Ctotal)  

When CL increases:

- Capacitance increases  
- Pole frequency decreases  
- Bandwidth reduces  

Therefore output node behaves as a low-pass filter.

---

# RESULTS

RD = 2.25 kΩ  
W = 9.08 µm  
ID = 400 µA  
Gain (Transient) = 3.326  
Gain (Theoretical) = 3.37  
Gain (dB) ≈ 10.4 dB  
f3dB (Parasitic only) = 1.3051 GHz  
f3dB (With 10pF) = 7.328 MHz  
UGB ≈ 24 MHz  

---

# INFERENCE

The Common Source amplifier was successfully designed using 180 nm technology.

The DC biasing ensured saturation operation and symmetrical signal swing. Transient analysis verified voltage amplification with phase inversion. AC analysis demonstrated the strong dependence of bandwidth on output node capacitance.

The theoretical and simulated results show close agreement, confirming correct analytical design and practical validation.

The experiment successfully demonstrates the relationship between biasing, gain, and frequency response in a MOSFET Common Source amplifier.

---

END OF EXPERIMENT
