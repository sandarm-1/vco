# Post-Layout results
Post-Layout simulation results of high speed VCO in Skywater 130nm.

First VCO layout and initial post-layout simulation results
====
"DP5" design was not good enough after post-layout:
------
The design called "DP5" (design details [here](https://github.com/powergainer/vco/blob/main/Initial_design_investigation.md)) was looking promising in Pre-Layout simulations reaching around 4.1GHz @ 0.9V Vctrl.

However when we implemented the layout and run the first post-layout simulations we saw that the frequency dropped to around 1.5GHz. That was a huge drop.

This is the original design "DP5" and its corresponding layout:

![image](https://user-images.githubusercontent.com/95447782/155851428-3a0457ab-87d9-47ae-89a0-8701611c8fd1.png)


The reason for the massive drop was that the initial pre-layout simulations were run on the VCO schematic with no parasitic caps back-annotated yet into the Schematic, hence the frequency was looking too high in pre-layout sims.

After creating the first layout for the VCO, we extracted the parasitic capacitor values from the extracted netlist, back-annotated them into the Schematic and re-run the pre-layout simulations.

Then we saw the frequency dropped to to 1.8GHz in Pre-layout simulation with back-annotated parasitic caps (values extracted from layout).

This result was much more in line with the post-layout result.

Plot of the drop from 4GHz (pre-layout with no parasitic caps) to 1.5GHz (full layout extracted netlist), then back up to 1.8GHz (pre-layout with back annotated parasitic caps):

![image](https://user-images.githubusercontent.com/95447782/155850939-ce73f9ae-32ef-4c61-b42a-ab32810a30aa.png)



These are the critical nets that dominate the oscillating speed of the VCO:

![image](https://user-images.githubusercontent.com/95447782/155851084-13f3a256-5ef5-41ef-b05d-8682ed3f6ae6.png)

And these are the corresponding tracks in the initial layout:

![image](https://user-images.githubusercontent.com/95447782/155851110-65d0ff66-0a1b-4e4e-989a-4664155102ed.png)



After this we performed a significant amount of layout optimization to reduce parasitic capacitance on these critical nets in the ring oscillator.

With layout optimization techniques we managed to speed it up a bit, reaching just **over 2GHz at 0.9V Vctrl** with the same circuit topology. However we wanted to increase this further.

Layout optimization techniques done to minimize capacitance on critical nets:
* Edited transistor Pcells to make Source and Drain contacts/LI straps slightly further apart without breaking DRC (further away tracks = less S to D capacitance)
* Rotated ring oscillator devices 90 degrees so that Sources and Drains have less distance in parallel, hence less capacitance from one node to another
* Shortened tracks on critical nets inside the ring oscillator
* Used LI (local interconnect layer) for short distance critical nets in ring oscillator
* Minimized metal layer changes and vias

However despite these local layout optimizations we eventually hit a wall and we couldn't make the VCO any faster with the initial circuit architecture.

Fundamentally the initial design was limited by the circuit topology: 3 current starved cells topology was limiting the maximum VCO frequency.



Circuit changes to increase speed
------
The original circuit architecture was fundamentally limited by the use of 3 current-starved delay cells in the ring oscillator.

The proposed improved architecture to speed up the VCO uses only one current-starved delay cell and two non-starved cells (i.e. standard inverters).

![image](https://user-images.githubusercontent.com/95447782/155852188-53bcd6bf-f415-45a9-b41e-0f4d696cd764.png)

The circuit proposed is equivalent to a buffer with positive feedback with one voltage-controlled delay cell in the feedback line. The standard inverters not only switch faster than equivalent current-starved cells but also they provide full rail to rail swing at their output hence creating a higher overdrive voltage at the gate of the starved cell, increasing operating speed and extending control voltage range.

![image](https://user-images.githubusercontent.com/95447782/155852210-26125757-1e2d-4189-bf13-cf728838c905.png)


For this to work it requires balancing the ring osc stages properly.
The starved cell one must be relatively small as this is the critical path for maximum speed operation.
The intermediate stage must be small also, as it’s the load for the starved cell.
The 3rd stage must be larger so it can drive the starved cell fast enough.


With this circuit topology, we went through an iterative optimization loop to optimize the key components of the VCO for relatively high speed:
* Optimizing current multiplication factor in current mirrors
* Optimizing strength of 3rd stage in the ring oscillator
* Optimizing ring oscillator overall balance of 3 stages

Device dimensions for VCO with 1 current-starved cell (DP9):

![image](https://user-images.githubusercontent.com/95447782/155852569-27e3ee61-9785-4331-8dbd-0c0872f6ec14.png)

Layout of VCO with 1 current-starved cell (DP9):

![image](https://user-images.githubusercontent.com/95447782/155852731-50e7df0f-eb6e-4cec-b07b-8c8d05e78c76.png)





