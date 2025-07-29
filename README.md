# MathWorks_Group14
Engineering Pathways Program - MathWorks MATLAB Internship - Group 14 - Fast-Charging Battery Optimization
Project Link - https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Battery%20Fast%20Charging%20Optimization

---

## 📋 What Andrew & Roberto Should Add

### 🔹 Andrew
- Upload `.slx` model with scope data
- Add parameter sweeps or tuning (e.g., cutoff voltage, max temp)
- Contribute at least one scope screenshot
- Add `andrew_findings.md` summarizing results

### 🔹 Roberto
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
