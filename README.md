🔥 You got it, River. Here's a **banger-level `README.md`** for your submission, designed to impress: clear, technical, collaborative, and ready for GitHub or course upload.

---

## ✅ `README.md` – MathWorks\_Group14

> Engineering Pathways Program – MathWorks MATLAB Internship
> Group 14: Fast-Charging Battery Optimization
> 🔗 [Challenge Project Link](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Battery%20Fast%20Charging%20Optimization)

---

## ⚡ Project Overview

This project explores the design, simulation, and evaluation of **fast-charging strategies** for lithium-ion batteries using **Simscape Battery’s Single Particle Model (SPM)**.

We each implemented a variant of the battery model and charging logic, adjusted parameters, and studied effects on performance metrics such as SOC rise, voltage behavior, temperature, and waveform "wavelengths."

---

## 🧠 Project Goals

### 1. **Familiarize with the SPM Battery Model**

* Understand how the SPM simplifies electrochemical equations.
* Key parameters: solid-phase & electrolyte concentrations, thermal effects.

> *Note:* We approximated lithium plating risk using lithium-ion concentration instead of tracking electric potentials at the anode/separator.

---

### 2. **Set Up the Battery Simulation**

* Configure SPM with custom nominal capacity, initial SOC, cutoff voltage, and optional thermal properties.
* Model charging current input and output scopes: SOC, voltage, temperature.

---

### 3. **Simulate Baseline CC–CV Charging**

* Use the Battery CC–CV Controller block.
* Log:

  * Total charging time
  * Max temperature
  * Final SOC
  * Terminal voltage

---

### 4. **Design and Simulate Multi-Stage Charging Profiles**

* Create custom fast-charging sequences (e.g., 20 A → 10 A → 5 A → 0 A).
* Use `Step`, `Relay`, or `Signal Builder` blocks.
* Define stage transitions by time or SOC thresholds.

---

### 5. **Analyze and Compare Results**

* Record:

  * Charging duration
  * Max voltage & temperature
  * Final SOC
* Compare with CC–CV baseline
* Recommend optimal profiles for speed + safety.

---

## 📊 Experimental Results

| Trial | Duration (s) | Max Voltage (V) | Max Temp (K) | Final SOC (%) |
| ----- | ------------ | --------------- | ------------ | ------------- |
| 1     | 100          | 3.6             | 303          | 66            |
| 2     | 100          | 3.6             | 303          | 66            |
| 3     | 100          | 3.6             | 303          | 66            |

---

## 👤 Team Member Highlights

---

### 🔹 River

* Built a 3-stage switch logic based on SOC (20 → 10 → 5 A)
* Completed **Battery State Estimation Onboarding**
* Explored **Initial SOC tuning**, relay cutoff thresholds, waveform shaping
* Used scopes to visualize charging curve "wavelengths"
* Model: `CurrentModelSPM_Test.slx`

**Takeaways:**

* Switch logic was successfully designed but couldn't be fully integrated due to signal mismatch (Simulink vs Simscape).
* Thermal rise stayed safe (\~305 K), but **post-charge discharge** required tapering or relays.
* Estimation block gave better insight into runtime current behavior.

---

### 🔹 Andrew

* Built a modular **SPM Pack** using battery blocks and physical subsystems
* Observed nonlinear **voltage-SOC** relationship
* Verified model instability at >302 K, solved with **temperature-limited current**
* Tuned charge current to optimize smoothness vs speed

**Findings:**

* Higher current → faster charge but greater risk of overshoot or instability
* **Temperature**, not SOC, was the main constraint
* Recreated a model based on iPhone 15 specs to match real-world single-cell performance

---

### 🔹 Roberto

* Implemented **baseline CC–CV charging** inside the SPM circuit
* Used relay and delay logic to study tapering behavior
* Logged SOC ramp + discharge events in full charging cycles

**Model Metrics:**

| Metric    | Observation       |
| --------- | ----------------- |
| SOC Range | 0.3 → \~0.67      |
| Time      | \~72,000–86,400 s |
| Temp      | 298–305 K         |
| Voltage   | 3.2–3.65 V        |
| Current   | Pulsed + stepwise |

---

## 🧠 Reflections

* **Switch logic must be converted** using `Simulink-PS Converter` to integrate with Simscape Current Source.
* Charging control benefits from **relay cutoffs or breakpoint-driven tapering** to avoid post-peak discharge.
* SPM is lightweight and realistic for fast simulation but needs careful tuning at the limits.
* **Initial SOC**, thermal modeling, and controller logic all dramatically affect performance.

---

## 📚 Onboarding Completed

All team members:

* ✅ Simscape Battery Onboarding
* ✅ Simulink Onboarding
* ✅ Simscape Onboarding

River:

* ✅ Battery State Estimation Onboarding ✅

---

## 📁 Submission Structure

```
MathWorks_Group14_Submission/
├── README.md
├── river_model/
│   ├── CurrentModelSPM_Test.slx
│   ├── scope_SOC_temp_voltage_current.png
│   ├── switch_logic_diagram.png
│   └── river_findings.md
├── andrew_model/
│   ├── SPM_Pack_Model.slx
│   └── andrew_findings.md
├── roberto_model/
│   ├── SPM_CCCV_Integrated.slx
│   └── roberto_findings.md
```

---

## 🔄 Next Steps (Optional Reporting Phase)

* Add SOC overlays comparing profiles
* Generate a single-page executive summary
* Wrap up findings into a presentation
* Finalize switch logic integration with Simscape

---

> 🧠 Submitted by: River, Andrew, Roberto — Group 14, MathWorks Engineering Pathways

---

Let me know if you want this zipped, converted to PDF, or prepped for GitHub formatting. You nailed it, River 🔋🔥
