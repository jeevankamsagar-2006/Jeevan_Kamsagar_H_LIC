# Experiment 2

## DC, AC and Transient Analysis of Common Source Amplifier with Source Degeneration

### AIM

To design a Common Source (CS) amplifier with an NMOS transistor and source degeneration using TSMC 180nm technology in LTspice. The design must adhere to a supply voltage of 1.8V and a power constraint of $\leq 1mW$, and involve evaluating the DC operating point, transient response, voltage gain, and bandwidth.

---

### 1. Introduction

**What is an NMOS Common Source Amplifier with Source Degeneration?**

The Common Source (CS) amplifier is a fundamental building block in analog IC design. In this configuration:

* **Source Degeneration:** A resistor ($R_s$) is placed at the source to provide negative feedback, which improves linearity and stabilizes the gain.
* **Active Load:** A PMOS transistor is used as a load to achieve high gain within the $1.8V$ supply limit.

---

### 2. Working Principle

For proper amplification, transistors must be in the **Saturation Region**.

* **Saturation Condition:** $V_{DS} \geq V_{GS} - V_{th}$ (for NMOS) and $V_{SD} \geq V_{SG} - |V_{thp}|$ (for PMOS).

The voltage gain is stabilized by $R_s$ and is approximately:

$$
A_v \approx - \frac{g_m(r_{o1} || r_{o2})}{1 + g_m R_s}
$$

---

### 3. Design Calculations

The design is carried out step-by-step based on the given constraints.

#### Step 1: Power Budget and Drain Current ($I_D$)

Given $P \leq 1mW$ and $V_{DD} = 1.8V$:

$$
I_D = \frac{P}{V_{DD}} = \frac{1 \times 10^{-3}}{1.8}
= 555.5 \mu A
$$

**We select $I_D = 500 \mu A$** to stay safely within the power limit.

#### Step 2: Determining Node Voltages and $R_s$

To ensure symmetrical swing and stability:

* **Source Resistor ($R_s$):**

$$
V_{Rs} = 0.2V
$$

$$
R_s = \frac{V_{Rs}}{I_D}
= \frac{0.2V}{500 \mu A}
= \mathbf{400 \Omega}
$$

* **Output Voltage ($V_{out}$):**

$$
V_{out} = \frac{V_{DD}}{2} + 0.2V
= 0.9V + 0.2V
= \mathbf{1.1V}
$$

#### Step 3: NMOS Gate Bias and Overdrive Voltage

Using:

$$
V_{ov} = 0.25V
$$

$$
V_{thn} = 0.36V
$$

Then:

$$
V_{GS} = V_{thn} + V_{ov}
= 0.36V + 0.25V
= 0.61V
$$

* **Gate Voltage ($V_{B1}$):**

$$
V_{B1} = V_{GS} + V_{Rs}
= 0.61V + 0.2V
= \mathbf{0.81V}
$$

#### Step 4: Transistor Sizing ($W/L$)

Using the saturation current equation:

$$
I_D = \frac{1}{2} k_n' \frac{W}{L} V_{ov}^{2}
$$

where:

$$
k_n' \approx 277 \mu A/V^2
$$

* **For NMOS:**

$$500 \mu A = \frac{1}{2}(277 \mu A/V^2)\frac{W_n}{180nm}(0.25)^2$$

Solving gives:

**$W_n \approx 11.6\mu m$**

* **For PMOS:**

To support the same drain current:

**$W_p \approx 29.5\mu m$**

---

### 4. Circuit Schematic

The schematic below was constructed in LTspice using the `tsmc018.lib` library.

![Circuit Schematic](circuit2.jpeg)

---

### 5. Simulation Results

#### A. DC Operating Point Analysis

The simulation was performed to verify the quiescent points ($I_D$ and $V_{out}$).

![DC Operating Point](dc_analysis2.jpeg)

* **Simulated $I_D$:** $506 \mu A$
* **Simulated $V_{out}$:** $1.104V$
* **Simulated $V_s$:** $0.202V$

These values closely match the design targets.

---

#### B. Transient Analysis

A $1kHz$ sine wave with $10mV$ amplitude ($20mV$ p-p) was applied.

![Transient Response Waveform](transient2_1.jpeg)

* **$V_{in(p-p)}$:** $19.99mV$
* **$V_{out(p-p)}$:** $0.25V$

Voltage Gain:

$$
A_v
===

# \frac{0.25}{0.0199}

\mathbf{13.15}
$$

The output signal is amplified and phase inverted, as expected from a common-source amplifier.

---

#### C. AC Analysis (Frequency Response)

The frequency response was analyzed with a $10pF$ load capacitor.

![Frequency Response Bode Plot](ac_analysis2.jpeg)

* **Mid-band Gain:** $21.95dB$
* **3dB Bandwidth:** $2.276MHz$
* **Unity Gain Bandwidth (UGB):** $27.905MHz$

---

### 6. Result Comparison

| Parameter                  | Theoretical / Target | Simulated  |
| -------------------------- | -------------------- | ---------- |
| Drain Current ($I_D$)      | $500\mu A$           | $506\mu A$ |
| Output Voltage ($V_{out}$) | $1.1V$               | $1.104V$   |
| Source Voltage ($V_s$)     | $0.2V$               | $0.202V$   |
| Voltage Gain ($A_v$)       | $23.74dB$            | $21.95dB$  |
| 3dB Bandwidth              | -                    | $2.276MHz$ |

---

### 7. Inference

1. The amplifier satisfies the power constraint since the total power consumption is:

$$
P = V_{DD} \times I_D
$$

$$
P = 1.8V \times 506\mu A
= 0.91mW
$$

which is below the specified limit of 1mW.

2. The simulated gain is slightly lower than the theoretical gain because of non-ideal effects such as body effect and channel length modulation.

3. The presence of the $10pF$ load capacitor shifts the dominant pole toward lower frequencies, thereby reducing bandwidth.

4. Both NMOS and PMOS transistors remain in the saturation region, ensuring proper amplifier operation.

---

### 8. Conclusion

A Common Source amplifier with source degeneration was successfully designed and analyzed using TSMC 180nm CMOS technology in LTspice.

The circuit achieved:

* Drain Current ≈ $506\mu A$
* Output Voltage ≈ $1.104V$
* Mid-band Gain ≈ $21.95dB$
* Bandwidth ≈ $2.276MHz$
* Power Consumption ≈ $0.91mW$

The design successfully met all specified constraints while demonstrating stable gain, proper biasing, and satisfactory frequency response characteristics.
