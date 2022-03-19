# High Speed VCO tapeout in Skywater 130nm using Caravel harness chip
High Speed VCO tapeout in Skywater 130nm using Caravel harness chip

To be updated with further details.

Final IP layout
====
In order to drive the Caravel pads, some extra driver circuitry was added.

Added extra buffers to ensure it can drive the Caravel output pads. Finally the IP will be driving out the VCO frequency divided down by 128 and 256 (so around 30MHz - 15MHz approx) out on io_out[] pads with io_oeb[] hardwired low in Caravel.

The output signals (out_div128_buf and out_div256_buf) are driving out io_out[] pads with corresponding io_oeb[] signals tied to VSS.

The option of driving out on gpio_analog[] was discarded in order to avoid driving through the 150 Ohm ESD resistors.

Simulation was run driving 5pF capacitance and output signals were ok.

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
* Kunal Ghosh, co-founder of VLSI System Design.
* Dr Javed S Gaggatur

Contact
-----
* Darío San Martín Molina (Author), Analog/Mixed-Signal IC Design Engineer. https://www.linkedin.com/in/dar%C3%ADo-s-a220a914/ 



However when we implemented the layout and run the first post-layout simulations we saw that the frequency dropped to around 1.5GHz. That was a huge drop.
