# Andrew's Findings

## Battery Voltage Behavior

The terminal voltage at full state of charge (SOC = 1) is approximately 3.515 V, and at empty (SOC = 0), it is about 3.0 V. This observation indicates that the battery voltage does not rise linearly with SOC, reflecting the inherent nonlinear relationship between voltage and SOC.

## Effects of Charging Current

Lower charging currents resulted in more stable battery behavior, enabling successful complete charge and discharge cycles. Initially, the hypothesis was that high currents caused model instability. Indeed, it was confirmed that high charging currents led to rapid increases in voltage and, subsequently, significant temperature rises within the battery.

## Effects of Temperature

Temperature was ultimately identified as the critical factor causing model failures. When the battery temperature exceeded approximately 302 K, the Simulink model experienced numerical instability and crashes. Initially, it was suspected that the underlying physics parameters of the model were the cause; however, implementing a temperature-controlled current source resolved these issues, allowing stable charging and discharging cycles. The impact of temperature on the battery's charging capability became clearly observable, highlighting temperature as the primary limiting factor.

## Misconceptions

Early assumptions about voltage limits based solely on initial SOC values were incorrect. Instead, the battery's temperature proved to be the more significant determinant of achievable voltage levels. Cooler battery temperatures allowed reaching higher voltages, confirming temperature dependency as a crucial factor in voltage limits.

## Battery Building

Constructing the battery model was more simple than initially anticipated. The process involved defining battery dimensions, selecting the battery type, and specifying the desired capacity. Efforts were made to closely replicate the specifications of an iPhone 15 battery based on publicly available data. To align with modern smartphone batteries, a single-cell configuration was utilized, making the simulation relevant to contemporary phone battery technology.

## Personal Reflections
Working on this project provided an intellectually fulfilling experience. I gained deep insight into how batteries function from a fundamental physics perspective, particularly regarding their behavior during charging and discharging cycles. Additionally, I learned the significant benefits and capabilities of using the Single Particle Model (SPM) for battery modeling, and now very much appreciate the practicality of this modeling approach.

Upon reflection with the team, we reached a consensus that focusing exclusively on the Simscape Battery Onramp from the beginning would have been more beneficial, rather than allocating time to multiple introductory onramps. Such an approach would have allowed us to dive deeper into the theoretical foundations of SPM, maximizing our understanding to be able to troubleshoot more efficiently.

The most rewarding realization for me was discovering how profoundly temperature affects the battery model. By the project's conclusion, it became clear that temperature critically regulates the battery's current, voltage, and state of charge (SOC), making it a primary factor in our model breaking.

Because of how engaging and rewarding I found this project, I have decided to continue working on it throughout the summer and perhaps beyond, aiming to further expand and complete it fully.

## Work Done:

### Onramps:
- Simulink Onramp
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
<img width="418" height="636" alt="image" src="https://github.com/user-attachments/assets/223f02be-41f1-4c0b-91d6-0a4d2d8c5a21" /><img width="425" height="494" alt="image - Battery Charging Current Limit Params" src="https://github.com/user-attachments/assets/82f54b2d-ee30-4b7e-a99b-b55d6063767b" /><img width="455" height="481" alt="image - Relay Params" src="https://github.com/user-attachments/assets/1bc08e10-cf07-426e-af2f-989ea4d11ca4" /><img width="420" height="290" alt="image - Unit delay Params" src="https://github.com/user-attachments/assets/31781559-f6eb-4acc-828e-926a153cb0e9" />
<img width="1413" height="937" alt="Scope Image" src="https://github.com/user-attachments/assets/f6776ade-dee4-40b3-8ca8-3b8e13db7ace" />


