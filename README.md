# 3GHz High Speed VCO
High Speed VCO in Google-Skywater 130nm process.

The scope of the work is to design a high speed VCO that can run in the GHz range (1.6 – 3.2GHz) with relatively low power consumption and low area.

A Phase Locked Loop (PLL) using this VCO in combination with appropriate frequency divider ratios can  generate a range of output frequencies up to 3.2GHz.

The design is to be implemented in 130nm CMOS technology.

![image](https://user-images.githubusercontent.com/95447782/159545975-644caf80-5cb7-410d-9a74-c7f3799e71a4.png)

![image](https://user-images.githubusercontent.com/95447782/159536411-3104660e-a312-41c9-ad33-6c2830ce608c.png)

![image](https://user-images.githubusercontent.com/95447782/159129021-774e9976-ce00-4699-9d40-47be3756df81.png)



Key features
===
* \> 3GHz VCO output frequency
* 1.8V supply
* Programmable bias current modes
* Custom VCO layout to minimize parasitics and achieve high frequency ([link](/Post-Layout/Post-Layout.md))
* Custom high speed frequency divider for >3.5GHz operation
* Area 0.00034mm^2 (VCO) + 0.00050mm^2 (10 Frequency dividers) 
* Taped out in Google-Skywater 130nm process




|		|	min	|	typ	|	max	|	Units	|	Conditions	|
|	------------	|	------------	|	------------	|	------------	|	------------	|	------------	|
|	Supply voltage	|	1.62	|	1.8	|	1.98	|	V	|		|
|		|		|		|		|		|		|
|	Fvco	|		|	2.68	|		|	GHz	|	@ 0.9V Vctrl, x0.125 bias mode	|
|		|		|	3.21	|		|	GHz	|	@ 0.9V Vctrl, x0.25 bias mode	|
|		|		|	3.46	|		|	GHz	|	@ 0.9V Vctrl, x0.5 bias mode	|
|		|		|	3.72	|		|	GHz	|	@ 0.9V Vctrl, x1 bias mode	|
|		|		|	3.94	|		|	GHz	|	@ 0.9V Vctrl, x2 bias mode	|
|		|		|		|		|		|		|
|	Supply current (VCO)	|		|	329.8	|		|	uA rms	|	@ 0.9V Vctrl, x0.125 bias mode	|
|		|		|	393.6	|		|	uA rms	|	@ 0.9V Vctrl, x0.25 bias mode	|
|		|		|	425.9	|		|	uA rms	|	@ 0.9V Vctrl, x0.5 bias mode	|
|		|		|	449.4	|		|	uA rms	|	@ 0.9V Vctrl, x1 bias mode	|
|		|		|	464.0	|		|	uA rms	|	@ 0.9V Vctrl, x2 bias mode	|
|		|		|		|		|		|		|
|	Kvco	|		|	9.31	|		|	GHz/V	|	@ 0.9V Vctrl, x0.125 bias mode	|
|		|		|	9.94	|		|	GHz/V	|	@ 0.9V Vctrl, x0.25 bias mode	|
|		|		|	8.78	|		|	GHz/V	|	@ 0.9V Vctrl, x0.5 bias mode	|
|		|		|	8.78	|		|	GHz/V	|	@ 0.9V Vctrl, x1 bias mode	|
|		|		|	6.79	|		|	GHz/V	|	@ 0.9V Vctrl, x2 bias mode	|
|		|		|		|		|		|		|
|	Area	|		|	0.00034	|		|	mm^2	|	VCO only	|
|		|		|	0.00050	|		|	mm^2	|	Frequency dividers (10 instances)	|
|		|		|		|		|		|		|
|	Noise	|		|		|		|		|		|
|		|		|		|		|		|		|



Design files
====
* [Schematics](https://github.com/powergainer/caravel_user_project_analog_vco/tree/main/xschem)
* [Layout](https://github.com/powergainer/caravel_user_project_analog_vco/tree/main/mag)
* [GDS](https://github.com/powergainer/caravel_user_project_analog_vco/tree/main/gds)

Simulation results
====
* [Pre-layout](/Pre-Layout/Initial_design_investigation.md)
* [Post-layout](/Post-Layout/Post-Layout.md)

Tape-out in Skywater 130nm Caravel harness chip
====
* [Tape-out of High Speed VCO in Skywater 130nm Caravel harness chip](/Post-Layout/Tapeout.md)


Methodology: Skywater 130nm technology PDK and EDA tools
====
The design methodology used in this projects is based on the Skywater 130nm PDK and open-source EDA toolflow.

More information on details about Google-Skywater 130nm technology and PDK and the open-source EDA toolflow can be found here:

[VSDIAT Skywater 130nm Physical Verification Workshop](https://github.com/powergainer/VSDIAT_Physical_Verification_Sky130)




References
====
[1] Hsieh, Ming-Ta & Sobelman, Gerald. (2006). “Comparison of LC and Ring VCOs for PLLs in a 90 nm Digital CMOS Process”.

[2] S. Suman, K. G. Sharma and P. K. Ghosh, "Analysis and design of current starved ring VCO," 2016 International Conference on Electrical, Electronics, and Optimization Techniques (ICEEOT), 2016, pp. 3222-3227.

[3] B. Goyal, S. Suman and P. K. Ghosh, "Design and analysis of improved performance ring VCO based on differential pair configuration," 2016 International Conference on Electrical, Electronics, and Optimization Techniques (ICEEOT), 2016.

[4] J. S. Gaggatur, "On-chip Temperature Compensated 2.5GHz to 10GHz Multi-band LC-VCO Phase Locked Loop for Wireline Applications," 2019 IEEE MTT-S International Microwave and RF Conference (IMARC), 2019, pp. 1-5.

[5] J. S. Gaggatur, "A 1.8 – 6.3 GHz Quadrature Ring VCO-based Fast-settling PLL for Wireline I/O in 55nm CMOS," 2021 34th International Conference on VLSI Design and 2021 20th International Conference on Embedded Systems (VLSID), 2021, pp. 294-298.




Acknowledgements
===
* Mr Kunal Ghosh, co-founder of VLSI System Design. https://www.vlsisystemdesign.com/
* Dr Javed S Gaggatur, https://scholar.google.com/citations?user=M38WZaQAAAAJ

Contact
===
* Darío San Martín Molina (Author), Analog/Mixed-Signal IC Design Engineer. https://www.linkedin.com/in/dar%C3%ADo-s-a220a914/ 


