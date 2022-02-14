# vco
High Speed VCO in Skywater 130nm

CS-VCO
====
5-stage vs 3-stage
------
Higher frequency can be achieved with 3 stages rather than 5 stages.

Fvco vs Vctrl for 3 vs 5 stages:
![image](https://user-images.githubusercontent.com/95447782/152638575-39170f98-0a9e-4087-888b-266762a9a17b.png)

Supply current (rms) vs Vctrl for 3 vs 5 stages:
![image](https://user-images.githubusercontent.com/95447782/152638600-cf312c5a-065f-4a95-95e7-a39406e051e8.png)


3 stages yields higher frequency at not much current increase.
From now on we focus on 3 stages.


Increasing current mirror ratio:
------
Mirror ratio increased from 1.29 to 1.6 to 2.4

Starting point: 1.29u/1.01u = x1.277 ratio

DP1: 1.6u/1.01u = x1.584 ratio

DP2: 2.4u/1.01u = x2.376 ratio

We can gain some speed at not much current increase.
But duty cycle starts to distort.
Not much current increase.

* Blue = 3-stage CS-VCO, mirrors 1.29u/.18u, inverters 0.5u/.18u (1.462GHz @ 0.9V Vctrl)
* Purple = 3-stage CS-VCO, mirrors 1.6u/.18u, inverters 0.5u/.18u (1.695GHz @ 0.9V Vctrl)
* Pink = 3-stage CS-VCO, mirrors 2.4u/.18u, inverters 0.5u/.18u (2.068GHz @ 0.9V Vctrl)

![image](https://user-images.githubusercontent.com/95447782/152638679-bf99ab79-a2ef-4ce9-96f7-176f2dee13d7.png)


|Current mirror multiplication factor	|Fvco @ 0.9V Vctrl (Hz)|	Kvco (Hz/V)|
|------------|------------|------------|
|1.277	|1.462E+09	|5.27E+09 Hz/V|
|1.584	|1.695E+09	|5.62E+09 Hz/V|
|2.376	|2.068E+09	|5.65E+09 Hz/V|

![image](https://user-images.githubusercontent.com/95447782/152638733-b8a1b642-7250-406c-ba6e-2241208b3f1d.png)

![image](https://user-images.githubusercontent.com/95447782/152638736-9f5acc31-cad4-4307-8fc7-ea8dd6436e4b.png)


Takeaway:
Hence increasing current mirror ratio can help increase frequency and Kvco.




Increasing delay cell inverter drive strength:
-----
For a fixed mirror ratio, we show the effect of changing delay cell inverter drive strength (0.18um L vs 0.15um L).

Increasing delay cell inverters drive strength (reducing L from 0.18u to 0.15u)

* Blue = 3-stage CS-VCO, mirrors 1.6u/.18u, inverters 0.5u/.15u (2.16GHz)
* Green = 3-stage CS-VCO, mirrors 2.4u/.18u, inverters 0.5u/.15u (2.64GHz)

![image](https://user-images.githubusercontent.com/95447782/152638828-c01e81c4-7ec4-4877-a6c4-71a90fd05a42.png)


Takeaway:
Making inverters minimum length can benefit high frequency operation.
Frequency goes up significantly.
But duty cycle starts to distort.
And peak to peak swing goes down significantly (specially if mirror ratio also increased).

Leakage not much of a concern since top and bottom mirror devices are 0.18um length.




Kvco:
--------
Table of Kvco for each Design point.

|Design Point|			Kvco|
|------------|------------|
|mirrors 1.29u/.18u|			5.27E+09 Hz/V|
|mirrors 1.6u/.18u|			5.62E+09 Hz/V|
|mirrors 2.4u/.18u|			5.65E+09 Hz/V|
|mirrors 1.6u/.18u, invs 0.5u/.15u|			6.73E+09 Hz/V|
|mirrors 2.4u/.18u, invs 0.5u/.15u|			6.63E+09 Hz/V|

![image](https://user-images.githubusercontent.com/95447782/152638918-b112174d-7f43-41e1-9e05-8159bac787ab.png)




Summary
--------
F vs Vctrl for various design points so far:
![image](https://user-images.githubusercontent.com/95447782/152638931-341f046e-7443-44dc-8cd2-3050ec599e56.png)

Current consumption vs Vctrl:
![image](https://user-images.githubusercontent.com/95447782/152638934-b6bda38d-de88-48fe-9ace-bc7f6dfe32f5.png)


* Looks like design with mirrors at 1.6u/0.18u and min length inverters may be an ok tradeoff for relatively high speed, and oscillator internal phases not too distorted.
* Possibly reduce mirror ratio to help reduce duty cycle distortion a bit without losing too much speed.


Further optimization:
===
We tried to increase oscillation speed by trying to optimize the following aspects of the circuit:

Fixing the output swing:
----
Rising edge is slower than falling edge, look into making PMOS stronger than NMOS in delay cells and/or output buffer. --> This was fixed by making the PMOS on the last stage of the output buffer stronger than the NMOS.

![image](https://user-images.githubusercontent.com/95447782/153831511-d61e6ae6-783c-46fe-a107-447aa74bc398.png)


Optimization of delay cell dimensions:
---
We can try to gain speed with larger W on delay cells (more drive strength, able to charge capacitance faster)? But drain capacitance may increase and thus reduce speed? So perhaps the way to go may be reducing inverter W, since that may reduce drain cap, if that dominates speed then speed may go up.

**Sweep of delay cell pmos & nmos dimensions:**



From there maybe we can try to increase current mirror ratio.

Output buffer optimization:
---
The load capacitance presented by the output buffer to the ring oscillator reduces operating speed. Can the ring oscillator drive the output buffer fast enough? Maybe reduce output buffer 1st stage. Investigate effect of output buffer on speed. More strength better? But more capacitance? So what's the best trade off?






