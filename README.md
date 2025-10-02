# Advanced Analog Design

## Lab Report

### Introduction to Analog Integrated Circuit Design


#### 19/09

---

## Table of Contents

- 1 NMOS Transistor
  - 1.1 Simulation on Cadence - Schematic Creation
  - 1.2 Bias Point VGS = 1 V, VDS = 2 V
  - 1.3 iD–vDS Characteristic (sweep of vDS for several VGS)
  - 1.4 iD–vGS Characteristic (sweep of vGS for several VDS)
  - 1.5 Graphical Verification of the Bias Point
  - 1.6 Theoretical vs Practical Comparison
- 2 Common-Source Amplifier
  - 2.1 Schematic Creation
  - 2.2 Time-Domain and Frequency Simulations
  - 2.3 Theoretical Calculations and Comparison
  - 2.4 Sizing Adjustment for |Av| = 10 and Vout ≈ VDD/2
  - 2.5 Results of the Adjustment

---

In this first lab, the objective was to become familiar with **Cadence Virtuoso** through three complementary aspects.  
We started with the study of an **NMOS transistor**, measuring parameters at a fixed bias point (VGS = 1 V and VDS = 2 V). We then plotted the **iD–vDS** and **iD–vGS** characteristics for different voltage values, verifying consistency with the chosen operating point.  

The NMOS was dimensioned with **L = 0.35 μm** and **W = 2 μm**. Parameters were extracted at VSG = 1 V and VSD = 2 V, then the static characteristics were plotted to confirm the bias point.  

Finally, we designed a **common-source amplifier**, presenting both time-domain and frequency simulation results. The gain was compared with theoretical calculations, and the design was tuned to reach a gain of **20 dB** with the output centered at **VDD/2**.  

---

# Chapter 1  
## NMOS Transistor

### 1.1 Simulation on Cadence - Schematic Creation
The NMOS test circuit was created using **Cadence Virtuoso**.  
We opened a new schematic cell with the `tech_c35b4` technology. Components were chosen as follows:
- NMOS transistor from `PRIMLIB/Mosfets/nmos4`  
- DC voltage sources from `analogLib/Sources/Independent/vdc`  
- Ground from `analogLib/Sources/Globals/gnd`

- Figure 1.1 – Schematic for NMOS transistor study

<img width="361" height="377" alt="image" src="https://github.com/user-attachments/assets/d166efcc-2e27-4131-a216-17e12790a0b6" />

---

### 1.2 Bias Point VGS = 1 V, VDS = 2 V
The operating point was obtained with a **DC Operating Point analysis**.  
At VGS = 1 V and VDS = 2 V, the following values were measured:
ID = 66.96 μA
gm = 243.7 μS
gDS = 4.601 μS
Vth = 548.2 mV
r0 = 1 / gDS = 217.344 kΩ


These reference values were used for graphical verification.
<img width="364" height="329" alt="image" src="https://github.com/user-attachments/assets/c302af0a-7b52-45c2-840f-e25d7bbe436f" />

Figure 1.2 – Annotated DC operating point (VGS=1 V, VDS=2 V)

---

### 1.3 iD–vDS Characteristic (sweep of vDS for several VGS)
Using a **DC sweep** on vDS, with VGS constant, we plotted iD vs vDS.  
A parametric analysis repeated the sweep for VGS ranging from 0 V to 3.3 V (step 0.3 V).  
The curve corresponding to VGS ≈ 1 V shows ID ≈ 66.96 μA, consistent with the .op analysis.

<img width="471" height="302" alt="image" src="https://github.com/user-attachments/assets/7bee2be2-5310-42aa-85c8-a20e966855d8" />

---

### 1.4 iD–vGS Characteristic (sweep of vGS for several VDS)
By sweeping vGS while keeping VDS constant, we obtained the iD–vGS characteristic.  
The sweep was repeated for VDS ranging from 0.3 V to 3.0 V (step 0.3 V).  
The threshold voltage Vth is visible, with quadratic increase beyond.  

At (VGS, VDS) = (1 V, 2 V), ID ≈ 66.96 μA, consistent with the .op analysis.
<img width="367" height="195" alt="image" src="https://github.com/user-attachments/assets/1131b655-c24b-49ab-b350-8ee0f9fc2e9e" />

---

### 1.5 Graphical Verification of the Bias Point
The bias point (VGS=1 V, VDS=2 V) was verified independently on both iD–vDS and iD–vGS curves.  
In both cases, ID ≈ 66.96 μA, confirming consistency between simulation and graphical reading.  
<img width="424" height="274" alt="image" src="https://github.com/user-attachments/assets/5ecab9d2-a6d0-479f-b808-c4cca81bf0ba" />

---

### 1.6 Theoretical vs Practical Comparison
Theoretical model in saturation:  

ID = 1/2 · k’n (W/L) (VGS − Vth)^2


With:
- k’n = 175 μA/V²  
- W = 2 μm  
- L = 0.35 μm  
- Vth ≈ 0.46 V  

→ Theoretical ID ≈ 145.8 μA  
→ Simulation gave ID ≈ 66.96 μA  

**Difference explanation**: real transistor models include effects ignored in the quadratic equation (carrier mobility reduction, velocity saturation, channel length modulation).  

Thus, simulation reflects physical reality better, though theory provides intuition.
<img width="475" height="315" alt="image" src="https://github.com/user-attachments/assets/d2cdc0df-5ba5-4797-9e1f-16f279e430c3" />

---

# Chapter 2  
## Common-Source Amplifier

### 2.1 Schematic Creation
The amplifier was designed with:
- NMOS biased at VGS ≈ 0.76 V  
- Load resistance RL = 16 kΩ  
- W = 22 μm, L = 2 μm  
- Output taken at the drain  

This ensures the output is centered near VDD/2.
<img width="362" height="376" alt="image" src="https://github.com/user-attachments/assets/d0b84565-4120-457f-98af-14f54577abfd" />

Figure 2.1 – Common-source amplifier schematic


---

### 2.2 Time-Domain and Frequency Simulations
- **Transient simulation**: with input sine (10 mVpp), output showed ≈57 mVpp with 180° phase inversion.  
Gain ≈ -5.7.  

- **AC analysis**: with Vin = 1 V AC, Bode plot confirmed ≈ 15 dB gain at low frequency.  
<img width="605" height="280" alt="image" src="https://github.com/user-attachments/assets/f7493e8a-1f4f-4d3a-88d8-a20cd0eb03b8" />

---

### 2.3 Theoretical Calculations and Comparison
Small-signal model:  

Av = - gm (RL || r0) = - gm·RL / (1 + gds·RL)


From .op annotations: gm, gds → compute r0.  
→ Theoretical gain ≈ -5.7 (≈15 dB).  
→ Simulation confirmed ≈ 15 dB.  

Small differences come from non-idealities (channel length modulation, finite input amplitude, sweep step).
<img width="605" height="390" alt="image" src="https://github.com/user-attachments/assets/398fb5d5-d840-4f2d-a8e3-9713004eab48" />

---

### 2.4 Sizing Adjustment for |Av| = 10 and Vout ≈ VDD/2
Target: gain |Av| = 10 (20 dB) with output centered at VDD/2.  

Steps:  
1. Choose RL = 10 kΩ → ID ≈ VDD / (2·RL) ≈ 165 μA.  
2. With λ ≈ 0.069 V⁻¹ → r0 ≈ 88 kΩ → RL || r0 ≈ 9.2 kΩ.  
3. Target gm ≈ 1.1 mS.  
4. Vov ≈ 0.30 V → VGS ≈ 0.85 V.  
5. From kn′ = 175 μA/V² → W/L ≈ 20.5 → choose L=2 μm, W≈41 μm.  

Simulation confirmed output centering at VDD/2 and |Av|≈10.


---

### 2.5 Results of the Adjustment
Final parameters:  

VGS,DC = 0.83 V
RL = 11 kΩ
W = 44 μm (L = 2 μm)


At this point:  
- Output ≈ VDD/2  
- Frequency response plateau at Av ≈ 20 dB  
- Consistent with theoretical estimation  
<img width="341" height="482" alt="image" src="https://github.com/user-attachments/assets/936b6f77-b0f0-4fc1-b5e4-abf959b33e4a" />
Figure 2.4 – Operating point (.op) annotations

<img width="533" height="344" alt="image" src="https://github.com/user-attachments/assets/05694d68-c6c6-45c7-aa8a-7e0484280cfe" />

Figure 2.5 – Frequency gain (≈ 20 dB plateau at low frequency)


---

## Conclusion
This lab was a valuable exercise combining **microelectronics** and **analog design**.  
It demonstrated:  
- NMOS transistor modeling and biasing  
- Graphical and theoretical verification of transistor characteristics  
- Common-source amplifier design and analysis  
- Iterative sizing to meet gain and output constraints  

The work highlighted differences between simplified models and real simulations, emphasizing the importance of accurate device modeling in integrated circuit design.  



