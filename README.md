Absolutely, River! I've analyzed your latest scope (SOC, voltage, current, temperature), and here's a final, updated `README.md` with **your actual simulation data points** included.

---

## ✅ Final `README.md` — MathWorks\_Group14

markdown
# 🔋 Battery Fast Charging with Simscape Battery – MathWorks Group 14

> **Engineering Pathways Program – MATLAB Internship**  
> Project Hub: [Battery Fast Charging Optimization](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Battery%20Fast%20Charging%20Optimization)

---

## 🎯 Project Overview

This project simulates and evaluates fast-charging strategies for lithium-ion batteries using the **Single Particle Model (SPM)** in Simscape Battery.

We explored how charging logic, current profiles, temperature limits, and SOC thresholds affect:
- Charging time
- Voltage behavior
- Thermal rise
- Final SOC performance

---

## 📘 Project Goals

1. **SPM Familiarization** – Understand model simplifications & lithium plating risk approximation  
2. **Battery Simulation Setup** – Tune parameters (initial SOC, cutoff voltage, thermal)  
3. **Baseline CC–CV Charging** – Implement reference profile & compare against custom methods  
4. **Multi-Stage Fast Charging** – Use switching logic, relay cutoffs, taper control  
5. **Analysis** – Log SOC, temp, current, voltage over time; recommend optimized profile  

---

## 📁 Team Members & Contributions

| Name     | Role |
|----------|------|
| **River** (me) | Parameter tuning, waveform optimization, battery state estimation, switch logic design, SOC sweep experiments |
| **Andrew**     | Built multi-cell SPM Pack model, focused on current stability, temperature-controlled charge cycles |
| **Roberto**    | Implemented CC–CV profile, relay delay tuning, scope validation and SOC ramp documentation |

---

## 🎓 Onboarding Completed

- ✅ Simulink Onboarding  
- ✅ Simscape Onboarding  
- ✅ Simscape Battery Onboarding  
- ✅ Battery State Estimation *(River only)*  

---

## 📈 River’s Results (from Scope)

### 🔬 Scope: `CurrentModelSPM_Test.slx`
- **Simulation Duration**: `T = 86,400 s`  
- **SOC Range**: `0.30 → ~0.57` (27% gain)  
- **Peak Battery Voltage**: `~3.56 V`  
- **Current Pattern**: Peaks at 20 A → drops to 0 in ~7 cycles  
- **Temperature**: Ranged from `~298 K → 304 K`  
- **Waveform Shape**: Clear sawtooth “wavelengths” in SOC and temp

### 📌 Observations:
- The current **pulse shape** shows high-to-zero transitions tied to SOC thresholds.
- **Temperature remained stable**, never exceeding 304 K.
- SOC climbs steadily in each pulse → shows successful repeatable cycles.
- **Voltage drops during rest periods**, indicating recovery effects post-charge.

---

## 📊 River’s Data Table

| Metric        | Value              |
|---------------|--------------------|
| Initial SOC   | 0.30               |
| Final SOC     | ~0.57              |
| Charging Time | ~86,400 s          |
| Max Voltage   | ~3.56 V            |
| Max Temp      | ~304 K             |
| Current Peaks | 20 A (step-wise)   |

---

## 🧠 Reflections

- **Switch logic worked as planned**, using 3 thresholds to simulate tapering — but it remained **digitally isolated** due to Simulink/Simscape mismatch.
- SPM modeling is responsive — but **requires taper control or relays** to prevent discharge after 70% SOC.
- **Battery State Estimation** helped monitor SOC accurately across cycles.
- Future improvement: use a `Simulink-PS Converter` to integrate logic into physical source input.

---

## 🧩 Team Comparison Summary

| Member   | Focus                     | Result Highlight |
|----------|---------------------------|------------------|
| River    | Switch logic + SOC tuning | SOC: 0.30→0.57; 304 K max temp |
| Andrew   | Pack-based SPM model      | Temp control stabilized full charges |
| Roberto  | CC–CV tuning w/ relays    | Full profile traced with baseline current |

---

## 📁 Folder Structure

```

MathWorks\_Group14\_Submission/
├── river\_model/
│   ├── CurrentModelSPM\_Test.slx
│   ├── scope\_SOC\_voltage\_temp\_current.png
│   ├── river\_findings.md
├── andrew\_model/
│   ├── SPM\_Pack\_Model.slx
├── roberto\_model/
│   ├── CC\_CV\_Integrated.slx
└── README.md

```

---

## ✅ Next Steps (If Time Allows)

- Integrate switch logic into full physical path
- Compare charge tapering methods (SOC vs Time control)
- Generate shared report or presentation slides for final documentation

> **Submitted by:**  
> River, Andrew, Roberto — Group 14, MathWorks Engineering Pathways


---

Let me know if you'd like this as a ZIP folder with filenames or converted to GitHub Markdown and/or PDF.

You’re submission-ready, River — excellent work!
