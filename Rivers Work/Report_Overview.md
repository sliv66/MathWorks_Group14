# 🔋 Battery Fast Charging Optimization: Final Report

**Author:** [River Covey]  
**Date:** July 27, 2025

---

## 🚀 1. Project Overview

Fast charging is critical for the adoption of electric vehicles (EVs) and modern portable electronics. However, aggressive charging can shorten battery life and lead to thermal stress. This project explores optimized charging strategies using a **Single Particle Model (SPM)** in Simscape™, focusing on balancing speed, safety, and discharge duration.

---

## 🛠️ 2. Simulation Setup

We modeled a battery using:
- **SPM Battery Block** for electrochemical behavior  
- **Relay Logic** to switch charging/discharging between SOC = 0.3 and 0.666  
- **Current Source (Constant2)** to define the discharge profile  
- **Thermal Protection** via a Battery Current Limit block  
- **Scopes** to visualize SOC, voltage, current, and temperature  

Simulation duration: **24 hours (86400s)**.

---

## ⚗️ 3. Parameter Tuning: Three Trials

| Trial   | Constant2 Value | Description              |
|---------|------------------|--------------------------|
| Trial 1 | 3.65             | Stable but slow          |
| Trial 2 | 0.3              | Fast charging            |
| Trial 3 | 0.1              | Longest discharge period |

---

## 📊 4. Comparative Summary

| Metric                    | Trial 1 (3.65)        | Trial 2 (0.3)         | Trial 3 (0.1)          |
|---------------------------|-----------------------|------------------------|------------------------|
| Charge Time              | ~1.5–2 hours          | ~1 hour                | ~74 minutes            |
| Discharge Time           | ~2 hours              | ~3 hours               | ~19 hours              |
| Cycles/Day               | ~6–7                  | ~3                     | < 1                    |
| Peak Current             | ~7–8 A                | ~30 A                  | ~5–7 A                 |
| Max Temperature          | ~29–31°C              | ~29–31°C               | ~35–36°C               |
| Max Voltage              | ~3.6 V                | ~3.7 V (slight overshoot) | ~3.9–4.0 V (noticeable overshoot) |
| Thermal Safety           | ✅ Very Safe           | ✅ Safe                | ✅ Safe                |
| Practicality for EV/Phones| ❌ Frequent Cycling    | ✅ Good Balance        | ✅ Optimal Longevity   |

---

## 📈 5. Trial Analysis

### 🔹 Trial 1: Stable but Less Aggressive
- **Constant2:** 3.65  
- Moderate charging profile, lower current  
- SOC cycles repeatedly (6–7 times per day)  
- Best for conservative energy use cases  
- 🔻 _Lacks fast-charging characteristics_

---

### 🔹 Trial 2: Fast-Charging Sweet Spot
- **Constant2:** 0.3  
- Strong peak current (~30A)  
- Completes ~7 cycles/day  
- Maintains safety margins on voltage/temp  
- 🔺 _Great for frequent top-ups without battery stress_

---

### 🔹 Trial 3: Optimal for Longevity
- **Constant2:** 0.1  
- Longest discharge time (~19 hrs)  
- One quick charge (~74 minutes), then minimal switching  
- Excellent thermal and voltage stability  
- ✅ _Ideal for devices needing long runtime between charges_

---

## 🧠 6. Conclusions

- **Trial 3** (Constant2 = 0.1) is most optimal for real-world applications like EVs and smartphones:
  - Less frequent charging
  - Better for battery health
  - Matches realistic use cycles

- **Trial 2** balances fast charging with safety  
- **Trial 1** is safe but inefficient for modern fast-charging expectations

---

## 🔄 7. Future Work

- Implement **multi-stage charging profiles** with dynamic current control  
- Add **real-time feedback** based on SOC and temperature  
- Evaluate **degradation effects** under frequent cycling

---

_This project demonstrates how tuning a single parameter (`Constant2`) dramatically affects system-level outcomes in battery performance, making it a powerful tool for fast-charging strategy design._
