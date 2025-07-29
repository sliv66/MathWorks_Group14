# MathWorks_Group14
Engineering Pathways Program - MathWorks MATLAB Internship - Group 14 - Fast-Charging Battery Optimization
Project Link - https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Battery%20Fast%20Charging%20Optimization

---

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


