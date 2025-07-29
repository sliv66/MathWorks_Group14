Model Scope Data
These graphs show a complete and successful charge and discharge cycle. The control system charges the battery at a constant current until it reaches a State of Charge (SOC) threshold, and then immediately begins to discharge. This model correctly captures the corresponding changes in voltage and temperature.

Graph Analysis

1. Constant Current (CC) Charging Phase (t ≈ 0 – 3100s)
current: After a brief initial spike, the current holds steady at a positive value of approximately 2 Amps. This indicates a constant current charge.

SOC: As a direct result of the constant current, the State of Charge increases at a steady, linear rate, rising from 30% to 70%.

batteryVoltage: The voltage rises steadily as the battery stores energy.

temp: The battery's temperature slowly and consistently increases due to internal heat generation from the charging process.

2. Charge-to-Discharge Transition (t ≈ 3100s)
This is the moment the control logic switches modes.

The transition is triggered when the SOC plot reaches its peak of 0.7 (70%). This is your charge cutoff condition.

The current plot shows an instantaneous flip from +2A to approximately -5A.

This sudden change from charging to discharging causes a sharp drop in the batteryVoltage.

3. Constant Current (CC) Discharging Phase (t > 3100s)
current: The current is held constant at approximately -5 Amps.

SOC: The State of Charge decreases linearly as the battery is discharged.

batteryVoltage: The voltage steadily decreases as energy is drawn from the battery.

temp: The temperature rises at a faster rate than it did during charging. This is because heat generation is proportional to the square of the current (I²), and the discharge current (5A) is higher than the charge current (2A).