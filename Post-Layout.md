# Post-Layout results
Post-Layout simulation results of high speed VCO in Skywater 130nm.

First VCO layout and initial post-layout simulation results
====
"DP5" design was not good enough after post-layout:
------
The design called "DP5" (design details here LINK) was looking promising in Pre-Layout simulations reaching around 4.1GHz @ 0.9V Vctrl.

However when we implemented the layout and run the first post-layout simulations we saw that the frequency dropped to around 1.5GHz. That was a huge drop.

The reason was that the initial pre-layout simulations were run on the VCO schematic with no parasitic caps back-annotated yet into the Schematic, hence the frequency was looking too high in pre-layout sims.

After creating the first layout for the VCO, we extracted the parasitic capacitor values from the extracted netlist, back-annotated them into the Schematic and re-run the pre-layout simulations.

Then we saw the frequency dropped to to 1.8GHz in Pre-layout simulation with back-annotated parasitic caps (values extracted from layout).

This result was much more in line with the post-layout result.



Plot of the drop from 4GHz to 1.5GHz, then back up to 1.8GHz with back annotated para caps.
*PLOT HERE*


These are the critical nets that dominate the oscillating speed of the VCO:

*PLOT OF net10, net9, net8 in SCH (ENSURE THIS SHOWS  the architecture with 3 starved cells)*

*AND SCREENSHOT OF THOSE TRACKS IN THE INITIAL LAYOUT*


After this we performed a significant amount of layout optimization to reduce parasitic capacitance on these critical nets in the ring oscillator.
With layout optimization techniques we managed to speed it up a bit, reaching
?over 2GHz I think?

Layout optimization techniques to minimize capacitance on critical nets
* Edit transistor Pcells to make Source and Drain contacts/LI straps slightly further apart without breaking DRC (further away tracks = less S to D capacitance)
* Rotate ring oscillator devices 90 degrees so that Sources and Drains have less distance in parallel, hence less capacitance from one node to another
* Shorten tracks on critical nets inside the ring oscillator
* Use LI (local interconnect layer) for short distance critical nets in ring oscillator
* Minimize metal layer changes and vias

However despite these local layout optimizations we eventually hit a wall and we couldn't make the VCO any faster with the initial circuit architecture.

Fundamentally the initial design was limited by the circuit topology: 3 current starved cells topology was limiting the maximum VCO frequency.



Circuit changes to increase speed
------
