#  **MathWorks Group 14**
# 🔋 Battery Fast Charging with Simscape Battery
------------------------------------------------------
> **Engineering Pathways Program – MATLAB Internship**  
> Project Hub: [Battery Fast Charging Optimization](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Battery%20Fast%20Charging%20Optimization)

------------------------------------------------------

## 🎯 Project Overview

This project simulates and evaluates fast-charging strategies for lithium-ion batteries using the **Single Particle Model (SPM)** in Simscape Battery.
Each team member has their models, scope, and feedback from their contributions for the project. Files and data mentioned throughout the READme.md can be found in team member's Media folder.

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

------------------------------------------------------------

## 📁 Team Members & Contributions
---
| **River**      | Parameter tuning, waveform optimization, battery state estimation, switch logic design, SOC sweep experiments |

| **Andrew**     | Built multi-cell SPM Pack model, focused on current stability, temperature-controlled charge cycles           |

| **Roberto**    | Implemented CC–CV profile, relay delay tuning, scope validation and SOC ramp documentation                    |

---------------------------
## 🎓 Onboardings Completed
---
- ✅ Simulink Onboarding
- https://matlabacademy.mathworks.com/details/simulink-onramp/simulink
- ✅ Simscape Onboarding
- https://matlabacademy.mathworks.com/details/simscape-onramp/simscape
- ✅ Simscape Battery Onboarding
- https://matlabacademy.mathworks.com/details/simscape-battery-onramp/orsb
- ✅ Battery State Estimation Onboarding *(River only)*
- MATLAB > SIMULINK > LEARN > ELECTRIFICATION > BATTERY STATE ESTIMATION
------------------------------

## 🧰 Model Architecture Summary (`CurrentModelSPM_Test.slx`)
---
> This section explains the main building blocks and logic inside the battery charging model.

* 🔧 Core **blocks used**
* 🧮 Key **constants and parameters**
* 🔁 Subsystems and control structures
* 📊 Logging and outputs

---

### 🔷 Core Simscape Battery Blocks

| Block                         | Purpose                                                                  |
| ----------------------------- | ------------------------------------------------------------------------ |
| **Battery (SPM)**             | Single Particle Model cell behavior (thermal + electrochemical dynamics) |
| **Controlled Current Source** | Drives current based on control logic (from CC–CV block or custom logic) |
| **Temperature Sensor**        | Reads cell temperature and outputs to scope/logging                      |
| **Current Sensor**            | Measures actual charging current applied                                 |
| **Voltage Sensor**            | Tracks battery terminal voltage                                          |
| **Thermal Reference**         | Grounds thermal domain                                                   |

---

### 🔧 Simulink Control + Logic

| Block                   | Functionality                                                                  |
| ----------------------- | ------------------------------------------------------------------------------ |
| **Relay**               | Enables or disables current based on SOC                                       |
| **Coulomb Counting**    | Estimates SOC via integration of current                                       |
| **Switch**              | Enables condition-based current selection (used in custom fast-charging logic) |
| **Compare to Constant** | Used in SOC logic for current stage transitions                                |
| **Gain**                | Converts raw values to scale for thresholds                                    |
| **Logical Operator**    | AND/OR conditions used to control current cutoff                               |
| **Scope**               | Visualizes: SOC, batteryVoltage, current, temp                                 |

---

### 🧮 Key Constants & Parameters

| Constant Block / Setting    | Value   | Purpose                                     |
| --------------------------- | ------- | ------------------------------------------- |
| **Initial SOC**             | 0.3     | Starting state of charge                    |
| **Cutoff Voltage**          | 3.65 V  | Used in CC–CV logic to transition stages    |
| **Relay Threshold (SOC)**   | 0.7     | Disables current if SOC > threshold         |
| **ChargingCurrentLimit**    | 20 A    | Max current applied                         |
| **Temp limit for safe op.** | \~305 K | Observed max safe thermal limit in practice |
| **Time Step (Tfinal)**      | 86400 s | Total simulation duration                   |

---

### 📈 Logged Outputs (to Scope)

| Output Name        | Description                                              |
| ------------------ | -------------------------------------------------------- |
| **SOC**            | State-of-charge over time (tracked via Coulomb Counting) |
| **batteryVoltage** | Terminal voltage of the cell                             |
| **current**        | Charging current (from controller or taper logic)        |
| **temp**           | Cell temperature in Kelvin                               |

----------------------------------------------

### 🧩 Control Flow Summary

1. **Input Current Logic**

   * Can be driven by CC–CV block or custom switch/relay logic
   * Current routed through Controlled Current Source block

2. **SOC Estimation**

   * Coulomb counting + initial SOC = real-time state-of-charge

3. **Relay Logic**

   * If SOC > 0.7 → cutoff current
   * Prevents overcharging or post-peak discharge

4. **Thermal Monitoring**

   * Temp sensor outputs logged, scoped, and used for analysis

----------------------------------------------------


## 📈 Example Result From Scope

### 🔬 Scope: `CurrentModelSPM_Test.slx`
- Results vary based on Block Parameter tuning
- **Simulation Duration**: `T = 86,400 seconds`, `T = 24 hours`
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

## 📊 Data Table 

| Metric        | Value              |
|---------------|--------------------|
| Initial SOC   | 0.30               |
| Final SOC     | ~0.57              |
| Charging Time | ~86,400s/12hr*60s  |
| Max Voltage   | ~3.56 V            |
| Max Temp      | ~304 K             |
| Current Peaks | 20 A (step-wise)   |
Folders > River's Media

## 🧠 Reflections

- **Switch logic worked as planned**, using 3 thresholds to simulate tapering — but it remained **digitally isolated** due to Simulink/Simscape mismatch.
- SPM modeling is responsive — but **requires taper control or relays** to prevent model failure after 66% SOC.
- **Battery State Estimation** helped monitor SOC accurately across cycles.

--------------------------------------------------

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

------------------------------------------------

## ✅ Next Steps

- Integrate switch logic into full physical path
- Compare charge tapering methods (SOC vs Time control)
- Generate shared report or presentation slides for final documentation

> **Submitted by:**  
> River Covey, Andrew Prince, Roberto Duenas — Group 14, MathWorks Engineering Pathways

------------------------------------------------------------------------------------------
**Documentation:**
> - https://www.mathworks.com/products/simscape-battery.html
> - https://www.mathworks.com/help/simscape-battery/ref/batterysingleparticle.html
> - https://www.mathworks.com/company/technical-articles/generating-safe-fast-charge-profiles-for-ev-batteries.html
> - https://www.mathworks.com/help/simscape-battery/ug/battery-constant-current-constant-voltage.html
> - https://www.mathworks.com/videos/simscape-battery-essentials-part-6-battery-charging-and-discharging-1663756212085.html
> - https://www.mathworks.com/help/simscape-battery/ug/battery-state-of-charge-estimation.html
> - https://www.mathworks.com/help/sldo/ug/perform-grouped-estimation-of-model-parameters-for-single-particle-battery-model.html
