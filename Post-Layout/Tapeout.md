# High Speed VCO tapeout in Google-Skywater 130nm using Caravel harness chip
High Speed VCO tapeout in Skywater 130nm using Caravel harness chip



Final IP layout
====
In order to drive the Caravel pads, some extra driver circuitry was added.

Added extra buffers to ensure it can drive the Caravel output pads. Finally the IP will be driving out the VCO frequency divided down by 128 and 256 (so around 30MHz - 15MHz approx) out on io_out[] pads with io_oeb[] hardwired low in Caravel.

The output signals (out_div128_buf and out_div256_buf) are driving out io_out[] pads with corresponding io_oeb[] signals tied to VSS.

The option of driving out on gpio_analog[] was discarded in order to avoid driving through the 150 Ohm ESD resistors.

Simulation was run driving 5pF capacitance and output signals were ok (VCO output divided by 128 and 256, not the high speed 3GHz VCO output).

A custom frequency divider circuit was designed in order to divide down the >3GHz output from the VCO. This custom divider can take in the >3GHz straight from VCO, said divider can run above 3.5GHz in  post layout sims. Then after that we keep dividing down with more standard dividers and we keep lowering the frequency until we get down to divide-by-128  and 256.

This is the final IP layout including output buffers:

![final_ip_layout_including_output_buffers](https://user-images.githubusercontent.com/95447782/159128884-684d7186-d686-4544-af30-dd4a34b7c9c0.png)


This is the IP integrated in Caravel_user_project_analog:

![vco_integrated_in_caravel_user_project_analog](https://user-images.githubusercontent.com/95447782/159128930-f709074c-b0a0-4136-8134-12f70f5a419a.png)


High Speed VCO IP taped out in Caravel Skywater 130nm harness chip
====
After passing all prechecks both locally and in Efabless platform, the chip is taped out.

This is the final Caravel GDS with the High Speed VCO IP:

![Caravel_GDS_with_VCO_taped_out](https://user-images.githubusercontent.com/95447782/159129021-774e9976-ce00-4699-9d40-47be3756df81.png)


Acknowledgements
------
* Mr Kunal Ghosh, co-founder of VLSI System Design. https://www.vlsisystemdesign.com/
* Dr Javed S Gaggatur, https://scholar.google.com/citations?user=M38WZaQAAAAJ

Contact
-----
* Darío San Martín Molina (Author), Analog/Mixed-Signal IC Design Engineer. https://www.linkedin.com/in/dar%C3%ADo-s-a220a914/ 


