**Roberto’s Report**

## Overview
The primary challenges I encountered were simulation errors caused by incomplete or conflicting control logic. These were mostly resolved through debugging, utilizing Simulink scope data and thoroughly analysing the behavior of graphs.

## Battery Design and Approach
I introduced the idea of using a reference battery model for our simulations to have clear initial parameters along with target variables. As a team, we decided to build our battery using the characteristics of a regular iPhone 15, using public tear down data. The reference battery consisted of an approximate nominal voltage of 3.869V, with a maximum cut-off around 4.48V and energy of 12.98 Wh. Other initial parameters include the area of the battery 0.0034 m^2 and the heat transfer coefficient of 10 W/m^2*k while keeping in mind the operating internal temperature of the device, between 273.15K  to 305.15K (kelvin). 

In my model, I chose to directly use the default Battery (Single Particle) block from the Simscape library, setting its parameters within the model workspace. In contrast, my teammates, Andrew and River, utilized the Battery Builder app. They used the app to first define the cell's geometry and properties based on our reference data and then exported that customized block into their Simulink model. We decided to try both workflows to see if the method of block creation affected the simulation issues we were facing. We later concluded that the issues were related to our control logic and not the battery block's implementation method.

## State of Charge (SOC) Behavior 
My initial thoughts were that simulation failure was due to violating SOC or voltage limits. After my investigation, it was noted that this was not the case, it was instead related to temperature runaway due to a long discharge time. As long as my temperature did not pass my threshold of 303.15K, it ran smoothly with little to no issues. I started simulating with an initial state of charge of .3 (30%) and was able to successfully charge the battery to .679 (67.9%) SOC and discharge the battery to .3 before running into instability which led to a crash in the model. 

## Reflection

Working on this project was a challenging yet worthwhile experience. I gained knowledge in the fundamentals of a lithium-ion battery and how they come in different models like the Single Particle Model (SPM). I learned more about the benefits and capabilities of using this model through my work. A key takeaway from this model is that it utilizes low to mid current profiles to charge and discharge while preserving battery health long term. During my simulation I explored and implemented control systems designing, basic signal processing and electrochemical modeling.

Moving forward, I will still continue to work on this project as it has sparked my curiosity and fired up my desire to complete it.  
