# Andrew's Findings

## Battery Voltage Behavior

The terminal voltage at full state of charge (SOC = 1) is approximately 3.515 V, and at empty (SOC = 0) it is about 3.0 V. This observation indicated that the battery voltage does not rise linearly with SOC, reflecting the inherent nonlinear relationship between voltage and SOC.

## Effects of Charging Current

Lower charging currents resulted in more stable battery behavior, enabling successful complete charge and discharge cycles. Initially, the hypothesis was that high currents caused model instability. Indeed, it was confirmed that high charging currents led to rapid increases in voltage and, subsequently, significant temperature rises within the battery.

## Effects of Temperature

Temperature was ultimately identified as the critical factor causing model failures. When the battery temperature exceeded approximately 302 K, the Simulink model experienced numerical instability and crashes. Initially, it was suspected that the underlying physics parameters of the model were the cause. However, implementing a temperature-controlled current source resolved these issues, allowing stable charging and discharging cycles. The impact of temperature on the battery's charging capability became clearly observable, highlighting temperature as the primary limiting factor.

## Misconceptions

Early assumptions about voltage limits based solely on initial SOC values were incorrect. Instead, the battery's temperature proved to be the more significant determinant of achievable voltage levels. Cooler battery temperatures allowed reaching higher voltages, confirming temperature dependency as a crucial factor in voltage limits.

## Battery Building

Constructing the battery model was simpler than initially anticipated. The process involved defining battery dimensions, selecting the battery type, and specifying the desired capacity. Efforts were made to closely replicate the specifications of an iPhone 15 battery based on publicly available data. To align with modern smartphone batteries, a single-cell configuration was utilized, making the simulation relevant to contemporary phone battery technology.

## Work Done:

### Onramps:
- Simulink Onboard
- Simscape Onramp
- Simscape Battery Onramp

### Research:
- Santhanagopalan & White (2006) – First EKF on a reduced Doyle‑Fuller‑Newman model
- COMSOL Multiphysics 6.3 - Single-Particle Modeling of Lithium-Ion Batteries
- Dong Zhang, Satadru Dey, Scott J. Moura - Lithium-Ion Battery State Estimation for a Single Particle Model

### Videos:
- https://www.mathworks.com/videos/from-electrode-to-pack-simulate-and-tune-fast-charge-profiles-1717557216452.html
- https://www.youtube.com/watch?v=QbRaLMtNjt8&t=255s

### General Testing with Github around 50 hours

## Images
<img width="1426" height="914" alt="Battery Builder Image" src="https://github.com/user-attachments/assets/40694454-a0d1-40a9-b0ca-3eac92621c4d" />
<img width="1504" height="647" alt="Model Image" src="https://github.com/user-attachments/assets/fdf3dc16-026c-49b3-b352-2b8fefdc7270" />
<img width="1413" height="937" alt="Scope Image" src="https://github.com/user-attachments/assets/f6776ade-dee4-40b3-8ca8-3b8e13db7ace" />
<img width="425" height="494" alt="image - Battery Charging Current Limit Params" src="https://github.com/user-attachments/assets/82f54b2d-ee30-4b7e-a99b-b55d6063767b" /><img width="455" height="481" alt="image - Relay Params" src="https://github.com/user-attachments/assets/1bc08e10-cf07-426e-af2f-989ea4d11ca4" />



