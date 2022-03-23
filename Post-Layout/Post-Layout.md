# Post-Layout results
Post-Layout simulation results of high speed VCO in Skywater 130nm.
All results typical corner and VDD=1.8V unless otherwise stated.

First VCO layout and initial post-layout simulation results
====
"DP5" design was not good enough after post-layout extraction:
------
The design called "DP5" (design details [here](/Pre-Layout/Initial_design_investigation.md)) was looking promising in Pre-Layout simulations reaching around 4.1GHz @ 0.9V Vctrl.

However when we implemented the layout and run the first post-layout simulations we saw that the frequency dropped to around 1.5GHz. That was a huge drop.

This is the original design "DP5" and its corresponding layout:

![image](https://user-images.githubusercontent.com/95447782/155851428-3a0457ab-87d9-47ae-89a0-8701611c8fd1.png)


The reason for the massive drop was that the initial pre-layout simulations were run on the VCO schematic with no parasitic caps back-annotated yet into the Schematic, hence the frequency was looking too high in pre-layout sims.

After creating the first layout for the VCO, we extracted the parasitic capacitor values from the extracted netlist, back-annotated them into the Schematic and re-run the pre-layout simulations.

Then we saw the frequency dropped to to 1.8GHz in Pre-layout simulation with back-annotated parasitic caps (values extracted from layout).

This result was much more in line with the post-layout result.

Plot of the drop from 4GHz (DP5 pre-layout with no parasitic caps) to 1.5GHz (full layout extracted netlist), then back up to 1.8GHz (pre-layout with back annotated parasitic caps):

![image](https://user-images.githubusercontent.com/95447782/155850939-ce73f9ae-32ef-4c61-b42a-ab32810a30aa.png)



These are the critical nets that dominate the oscillating speed of the VCO:

![image](https://user-images.githubusercontent.com/95447782/155851084-13f3a256-5ef5-41ef-b05d-8682ed3f6ae6.png)

And these are the corresponding tracks in the initial layout:

![image](https://user-images.githubusercontent.com/95447782/155851110-65d0ff66-0a1b-4e4e-989a-4664155102ed.png)



After this we performed a significant amount of layout optimization to reduce parasitic capacitance on these critical nets in the ring oscillator.

With layout optimization techniques we managed to speed it up a bit, reaching just **over 2GHz at 0.9V Vctrl** with the same circuit topology, post-layout. However we wanted to increase this further.

Layout optimization techniques done to minimize capacitance on critical nets:
* Edited transistor Pcells to make Source and Drain contacts/LI straps slightly further apart without breaking DRC (further away tracks = less S to D capacitance)
* Rotated ring oscillator devices 90 degrees so that Sources and Drains have less distance in parallel, hence less capacitance from one node to another
* Shortened tracks on critical nets inside the ring oscillator
* Used LI (local interconnect layer) for short distance critical nets in ring oscillator
* Minimized metal layer changes and vias

However despite these local layout optimizations we eventually hit a wall and we couldn't make the VCO any faster with the initial circuit architecture.

**Fundamentally the initial design was limited by the circuit topology: 3 current starved cells topology was limiting the maximum VCO frequency.**



Circuit changes to recover speed
====
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

Layout of VCO with 1 current-starved cell (DP9 - including programmable current modes):

![VCO_layout_dp9_with_control_ports](https://user-images.githubusercontent.com/95447782/157237491-d3940136-1350-4486-a22b-8a3501f96bc9.png)





Post-Layout sim results (VCO with 1 current-starved cell, DP9, with programmable bias currents)
---------------
Extracted post-layout simulation results for the updated design are shown below. For a comparison between schematic (pre-layout estimates with back-annotated parasitic caps) and extracted (post-layout) results for this design point, see [pre-layout estimates vs post-layout results for DP9 VCO](/Post-Layout/Pre-layout_estimates_vs_post-layout_results_dp9.md).

Plan is to tapeout with current scaling options so we will have both high current - high speed options and lower current - lower speed options.

The final programmable bias current settings are as follows:
* x0.125 (mirror size 0.6um)
* x0.25 (mirror size 1.2um)
* x0.5 (mirror size 2.4um)
* x1 (mirror size 4.8um)
* x2 (mirror size 9.6um)

These are post-layout results Fvco and supply current versus programmable current modes:

![image](https://user-images.githubusercontent.com/95447782/159693245-e04fc65c-b5fe-4d00-9a81-7a24189e1221.png)



VCO output waveform for DP9 post-layout, 3.731GHz at 0.9V Vctrl.

![image](https://user-images.githubusercontent.com/95447782/157240235-1bb8ed1a-9c0a-45cd-b90a-125087433f65.png)



Fvco and Current for different bias currents:

![image](https://user-images.githubusercontent.com/95447782/157237708-59b3dd7f-74f1-4f7b-8a6d-24d01c316339.png)



Kvco Vs bias current (measured between 0.7V and 0.9V Vctrl):

![image](https://user-images.githubusercontent.com/95447782/157235253-d3ed1d04-e867-4759-9469-d4c04b7e8811.png)





Summary:
-------------
DP9 post-layout can achieve:

0.125x current mode --> **2.686GHz @ 0.9V Vctrl, 324uA rms, Kvco 9.328GHz/V (between 0.7V and 0.9V)**

0.25x current mode --> **3.208GHz @ 0.9V Vctrl, 386uA rms, Kvco 9.941GHz/V (between 0.7V and 0.9V)**

0.5x current mode --> **3.463GHz @ 0.9V Vctrl, 419uA rms, Kvco 8.8GHz/V (between 0.7V and 0.9V)**

1x current mode --> **3.731GHz @ 0.9V Vctrl, 447uA rms, Kvco 8.814GHz/V (between 0.7V and 0.9V)**

2x current mode --> **3.949GHz @ 0.9V Vctrl, 464uA rms, Kvco 6.843GHz/V (between 0.7V and 0.9V)**



Making devices larger:
------------
Also tried a design where all the devices that switch at high speed are at least 2x minimum width & 2x minimum length.

This would be with the intention to avoid reliability/lifetime concerns due to devices switching at high speeds.

However the achieved frequency of the VCO would be lower and power consumption much larger.

This would be the design with all devices made larger:

![image](https://user-images.githubusercontent.com/95447782/157237016-c6fd5c28-1b96-404c-a91f-6d5769128f80.png)


The speed would be lower and current consumption would be significantly higher:

![VCO_large_devices_LVT_pre-layout](https://user-images.githubusercontent.com/95447782/157236440-a8b8dea9-118f-400b-9160-c69509caa16a.png)







Integration into Caravel
====
Caravel pads maximum output frequency is **50MHz**.

Hence we have to divide down the VCO frequency.

Adding 7 or 8 divide-by-2 frequency dividers we can divide the nominal VCO frequency by 128 or 256.

This way we can divide down the ~3GHz down to ~30MHz range which is appropriate for driving out through Caravel pads.

![image](https://user-images.githubusercontent.com/95447782/158037373-de0ad5d7-6734-4ee0-97bd-bf22c06a9ad5.png)


Simulation showing the VCO driving a series of dividers converting the ~3GHz VCO output to ~30MHz.

![image](https://user-images.githubusercontent.com/95447782/158037401-9a68b447-8886-4814-8a9b-a34246a6c81f.png)


Layout of VCO with frequency dividers for integration into Caravel for MPW5 tapeout:

![image](https://user-images.githubusercontent.com/95447782/158037434-de58479f-fb53-46b5-ac71-cbd7a9dfdfd0.png)




Next steps:
====
* Finalize Caravel integration of VCO + dividers.
* Run sim and pre-checks, complete requirements for MPW5 tapeout.
* Actions completed - See [Tapeout](/Post-Layout/Tapeout.md) details.




