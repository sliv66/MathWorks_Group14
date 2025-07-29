# MathWorks_Group14
Engineering Pathways Program - MathWorks MATLAB Internship - Group 14 - Fast-Charging Battery Optimization
Project Link - https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Battery%20Fast%20Charging%20Optimization
---
Project Goals:
1. Familiarize with the SPM Battery Model -

Study the theory behind the Battery Single Particle Model (SPM) block in Simscape Battery and how it simplifies complex electrochemical equations. Identify key parameters: solid-phase concentration, electrolyte concentration, and thermal effects.

Note: A more rigorous method to evaluate lithium plating risk is to compare the electric potentials at the solid and liquid phases at the anode/separator interface. When the potential difference approaches zero, metallic lithium plating becomes more favorable. However, to reduce modeling complexity with the SPM, we use lithium-ion concentrations as a practical substitute for estimating plating risk.

2. Set Up the Battery Simulation -

Use the SPM block and configure key parameters such as nominal capacity, initial state of charge (SOC), cutoff voltage, and thermal properties (if modeling heat).
Explore model inputs (charging current) and outputs (SOC, voltage, temperature).

3. Simulate Baseline CC–CV Charging -

Use the Battery CC–CV controller block to implement the standard charging method as reference.
Simulate the CC–CV process and record metrics such as:Total charging time, Maximum temperature (if thermal modeling is enabled), Final SOC and terminal voltage behavior.

4. Design and Simulate Multi-Stage Charging Profiles -

Create custom fast-charging strategies using step functions, lookup tables, or Signal Builder blocks.
Profiles may include 2–4 constant current stages (e.g., high current → medium → low → taper).
Define transitions based on time or SOC thresholds.
Run simulations for each profile and document performance.

5. Analyze and Compare Results -

For each charging profile, collect:Charging duration, Maximum voltage and temperature, and Final SOC.
Compare performance visually and numerically against the CC–CV baseline.
Recommend profiles that offer faster charging while staying within safety limits.

--------------------
Results 
------------------------------------------------
|Trial 1.|Charging duration:       100 seconds |
|        |Maximum voltage:               3.6 V |
|        |temperature:                   303 k |
|        |Final SOC:         .666 * 100% = 66% |
------------------------------------------------

------------------------------------------------
|Trial 2.|Charging duration:       100 seconds |
|        |Maximum voltage:               3.6 V |
|        |temperature:                   303 k |
|        |Final SOC:         .666 * 100% = 66% |
------------------------------------------------

------------------------------------------------
|Trial 3.|Charging duration:       100 seconds |
|        |Maximum voltage:               3.6 V |
|        |temperature:                   303 k |
|        |Final SOC:         .666 * 100% = 66% |
------------------------------------------------


## Andrew's Findings

### Battery Voltage Behavior

The terminal voltage at full state of charge (SOC = 1) is approximately 3.515 V, and at empty (SOC = 0) it is about 3.0 V. This observation indicated that the battery voltage does not rise linearly with SOC, reflecting the inherent nonlinear relationship between voltage and SOC.

### Effects of Charging Current

Lower charging currents resulted in more stable battery behavior, enabling successful complete charge and discharge cycles. Initially, the hypothesis was that high currents caused model instability. Indeed, it was confirmed that high charging currents led to rapid increases in voltage and, subsequently, significant temperature rises within the battery.

### Effects of Temperature

Temperature was ultimately identified as the critical factor causing model failures. When the battery temperature exceeded approximately 302 K, the Simulink model experienced numerical instability and crashes. Initially, it was suspected that the underlying physics parameters of the model were the cause. However, implementing a temperature-controlled current source resolved these issues, allowing stable charging and discharging cycles. The impact of temperature on the battery's charging capability became clearly observable, highlighting temperature as the primary limiting factor.

### Misconceptions

Early assumptions about voltage limits based solely on initial SOC values were incorrect. Instead, the battery's temperature proved to be the more significant determinant of achievable voltage levels. Cooler battery temperatures allowed reaching higher voltages, confirming temperature dependency as a crucial factor in voltage limits.

### Battery Building

Constructing the battery model was simpler than initially anticipated. The process involved defining battery dimensions, selecting the battery type, and specifying the desired capacity. Efforts were made to closely replicate the specifications of an iPhone 15 battery based on publicly available data. To align with modern smartphone batteries, a single-cell configuration was utilized, making the simulation relevant to contemporary phone battery technology.

## 🔹 Roberto
- Submit CC–CV charging baseline model with full scopes
- Include findings about SOC ramp rate and discharge behavior
- Reflect any unit delay or relay experiments

---

## 📘 Simulations Overview

| Metric        | Observation                          |
|---------------|--------------------------------------|
| SOC Range     | 0.3 → ~0.67                          |
| Charging Time | ~72,000–86,400 seconds              |
| Temp Range    | 298–305 K                            |
| Voltage       | 3.2–3.65 V                           |
| Current       | Variable pulses or stair-steps       |

All scope plots available in `scope_SOC_voltage_temp_current.png`

---

## 🔬 Notes & Reflections

- The **Switch Logic** was built successfully (three-stage based on SOC thresholds), but signal type mismatch prevented full integration with the Simscape current controller — future work could use a `Simulink-PS Converter` + controlled source.
- The **battery model is responsive**, but post-peak discharge can be aggressive without cutoff logic — a clear case for adding taper or relay-based SOC limits.
- Completing **Battery State Estimation** gave insight into how initial SOC and runtime current affect output SOC scaling.

---

## ✅ Next Steps (Future Reporting)

- Add overlay comparisons of SOC under different parameter conditions
- Create a final report doc or slide deck using our current scope plots
- Expand switch integration with physical control signal to close the loop


