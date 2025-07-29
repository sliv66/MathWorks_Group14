# Battery Fast-Charging Optimization: Project Report

**Author:** [River Covey/Group 14]
**Date:** July 29, 2025
>| **https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Battery%20Fast%20Charging%20Optimization**

---

## 1. Project Overview

>Fast charging is essential for modern devices like electric vehicles and smartphones.
>However, it's a challenge to charge batteries quickly without harming them (e.g., overheating, reducing lifespan).
>This project aimed to find the best way to fast charge a battery, modeled using a **Single Particle Model (SPM)** in Simulink,
>focusing on making charging faster and extending discharge time, all while keeping the battery safe.

Our simulations ran for **24 hours (a full day)** to see how the battery performed over many cycles.

---

## 2. How We Tested Charging

<img width="1331" height="671" alt="Screenshot 2025-07-29 at 2 34 10 PM" src="https://github.com/user-attachments/assets/c86f3d77-f863-4bd9-8f61-cac0161f0696" />


We used a digital model of a battery in Simulink. The core of our setup included:

* **Battery Model (SPM):** This component simulates the battery's chemical and electrical behavior.
* **Sensors:** We had virtual sensors to measure crucial battery metrics like voltage, current, and temperature.
* **Charging Controller:** This system, influenced by our adjustable `Constant2` parameter, sent commands to control the current flowing into the battery.
It also featured a **Safety Limit** block to prevent damage from excessive current.
* **SOC Estimator:** This component continuously calculated the battery's State of Charge (how full it was) over time.
* **Scope:** A visualization tool that displayed all these measurements (SOC, voltage, current, temperature) over the entire simulation duration.

By adjusting a key control setting called `Constant2` within this model, we explored different charging and discharging behaviors. We focused on three main trials to understand the various trade-offs:

* **Trial 1 (Less Ideal):** A setting for `Constant2` that produced a specific, less aggressive behavior.
* **Trial 2 (Mid-Ideal):** A setting for `Constant2` that gave a good balance.
* **Trial 3 (Most Ideal):** A setting for `Constant2` that produced our most desired overall outcome, particularly regarding discharge duration.

For each trial, we carefully measured:
* **Charging Time:** How long it took to charge the battery from its lowest to its highest capacity.
* **Discharge Time:** How long the battery lasted before needing a recharge.
* **Battery Stress Indicators:** How hot the battery got (Temperature) and how high its voltage spiked (Voltage).

---

## 3. Understanding the Results: What the Graphs Tell Us

Our results are presented in a series of graphs, often called "scopes," that visually track the battery's behavior over time. Let's look at an example from **Trial 3** to understand what each line on these graphs means:

![Example Scope (Trial 3)](https://github.com/user-attachments/assets/4b0e26d1-f4ea-4e65-b9b7-1185a504edfb)

* **1. SOC (State of Charge) - *The Battery's Fuel Gauge***:
    * This **purple line** shows the battery's fill level, like a fuel gauge from empty (0%) to full (100%).
    * When the line goes **down** (negative slope), the battery is **discharging** (being used). You can see this in the long downward slope in the example graph.
    * When the line goes **up** (positive slope), the battery is **charging** (being refilled). You can see the sharp upward spike around 20 hours in the example.
    * *See specific discharge time measurement:* ![SOC Discharge Time](https://github.com/user-attachments/assets/ac453338-0df8-4873-b99e-c06d49124e01)
    * *See specific charge time measurement:* ![SOC Charge Time](https://github.com/user-attachments/assets/215ae194-1649-45b6-ba4c-45c941f05dee)

* **2. batteryVoltage - *The Battery's Electrical Pressure***:
    * This **yellow line** shows the electrical "pressure" or voltage of the battery.
    * As the battery discharges (SOC goes down), its voltage naturally drops.
    * When it charges (SOC goes up), the voltage rises. You'll often see a quick spike (an "overshoot") at the start of charging, especially with fast charging, before it settles.

* **3. current - *The Flow of Energy***:
    * This **yellow line** shows how much electrical energy is flowing in or out of the battery.
    * A **positive spike** indicates **charging current** (energy flowing *into* the battery).
    * A **negative line** (below zero) indicates **discharging current** (energy flowing *out of* the battery).

* **4. temp (Temperature) - *The Battery's Heat***:
    * This **yellow line** tracks the battery's internal temperature.
    * When the battery is actively working (charging or discharging at higher rates), it generates heat, and the temperature line goes up.
    * During idle periods or slower operation, the temperature tends to cool down. Maintaining a safe temperature is vital for battery health.

---

## 4. Key Findings from Our Trials

Our experiments clearly demonstrated how adjusting the `Constant2` control setting significantly influences the battery's charging speed and discharge duration, alongside its thermal and electrical behavior. Finding the optimal balance between these factors is crucial for battery performance and longevity.

Here's a summary of what each trial revealed:

| Metric                          | Trial 1 (Less Ideal)             | Trial 2 (Mid-Ideal)              | Trial 3 (Most Ideal)              |
| :------------------------------ | :------------------------------- | :------------------------------- | :-------------------------------- |
| **Control Setting (`Constant2`)** | 3.65                             | 0.3                              | 0.1                               |
| **Peak Charging Power (Visual Est.)** | ~7-8 Amps (Moderate)             | ~30 Amps (Strong)                | ~5-7 Amps (Moderate)              |
| **Typical Charging Time** | ~1.5 - 2 hours                   | ~1 hour                          | ~74 minutes (~1.2 hours)          |
| **Typical Discharge Time** | ~1.5 - 2 hours                   | ~2.5 - 3 hours                   | ~19 hours                         |
| **Max Temperature** | ~29-31°C (Very safe)             | ~29-31°C (Very safe)             | ~35-36°C (Safe)                   |
| **Max Voltage** | ~3.6 V (Very stable)             | ~3.7 V (Stable, slight overshoot)| ~3.9-4.0 V (Noticeable overshoot) |
| **Cycles in 24 hours** | ~6-7 cycles                      | ~7 cycles                        | Less than 1 cycle                 |

---

**Detailed Analysis of Each Trial:**

* **Trial 1 (Less Ideal):**
    * **Settings:** `Constant2` at 3.65.
    * **Performance:** This trial shows a stable, low-stress operation. The charging current is moderate (~7-8 Amps), leading to a charging time of 1.5-2 hours. The battery remains cool (~29-31°C), and voltage is stable. It cycles well, completing 6-7 charge/discharge cycles in a day.
    * **Why "Less Ideal":** While very safe and reliable, its charging speed isn't optimized for "fast" charging demands.
    * **Visuals:** ![Trial 1 Scope (Less Ideal)](https://github.com/user-attachments/assets/0156d052-fea5-4266-8481-0eb4b7a8429c)

* **Trial 2 (Mid-Ideal):**
    * **Settings:** `Constant2` at 0.3.
    * **Performance:** This trial uses a stronger 30 Amp peak charging current, significantly reducing charging time to about 1 hour. The battery's temperature and voltage remain well within safe limits (~29-31°C), showing a good balance between speed and battery health. It completes approximately 7 cycles in a day.
    * **Why "Mid-Ideal":** It achieves a practical fast charge speed while maintaining good battery health, making it a strong contender for daily use.
    * **Visuals:** ![Trial 2 Scope (Mid-Ideal)](https://github.com/user-attachments/assets/772b9677-c839-4a60-b2d5-e2dc189915ea)

* **Trial 3 (Most Ideal):**
    * **Settings:** `Constant2` at 0.1.
    * **Performance:** This trial uses a lower ~5-7 Amp peak current. Its standout feature is an incredibly long discharge time of ~19 hours, meaning the battery can be used much longer between recharges. The charging itself takes about 74 minutes, with manageable heat (~35-36°C) and voltage (~3.9-4.0V).
    * **Why "Most Ideal":** While not the absolute fastest charging in terms of minutes, it's "most ideal" because it maximizes the *time the battery can be used* between charges. This is crucial for applications needing extended operation and fewer charge cycles.
    * **Visuals:** ![Trial 3 Scope (Most Ideal)](https://github.com/user-attachments/assets/6186e06c-b7a0-43dd-84af-f863a47568dd)

---

## 5. Conclusion and Next Steps

Our project successfully explored different ways to charge and discharge a battery model, demonstrating that optimizing performance is about balancing various factors.

* **No Single "Best":** There isn't one single "ideal" setting for all situations. It truly depends on your specific operational goals. Do you prioritize **fast charging (like Trial 2)** for frequent, quick top-ups, or **long usage time between charges (like Trial 3)** for extended operation?
* **Complex Control:** We observed that adjusting `Constant2` (our control setting) had a complex, non-linear effect on the actual charging current the battery received. This highlights that understanding the battery's control logic is key to achieving desired performance. Our project confirmed that `Constant2` values at or above `0.1` consistently produced realistic and useful results.
* **Safety First:** Keeping the battery cool and preventing dangerous voltage spikes is always critical. Our model's built-in safety features (the `Battery Charging Current Limit` block) were vital for ensuring the battery operated safely throughout all trials.

**Future Work:**
To achieve even better optimization, the next step would be to implement **multi-stage charging**. This involves dynamically changing the current during a single charge cycle (e.g., starting with high current, then gradually reducing it) based on the battery's real-time temperature and charge level. This adaptive control allows for the fastest possible charging while continuously safeguarding the battery and maximizing its lifespan.

---
