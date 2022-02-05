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

Blue = 3-stage CS-VCO, mirrors 1.29u/.18u, inverters 0.5u/.18u (1.462GHz @ 0.9V Vctrl)
Purple = 3-stage CS-VCO, mirrors 1.6u/.18u, inverters 0.5u/.18u (1.695GHz @ 0.9V Vctrl)
Pink = 3-stage CS-VCO, mirrors 2.4u/.18u, inverters 0.5u/.18u (2.068GHz @ 0.9V Vctrl)

![image](https://user-images.githubusercontent.com/95447782/152638679-bf99ab79-a2ef-4ce9-96f7-176f2dee13d7.png)


|Current mirror multiplication factor	|Fvco @ 0.9V Vctrl (Hz)|	Kvco (Hz/V)|
|------------|------------|------------|
|1.277	|1.462E+09	|5.27E+09 Hz/V|
|1.584	|1.695E+09	|5.62E+09 Hz/V|
|2.376	|2.068E+09	|5.65E+09 Hz/V|

![image](https://user-images.githubusercontent.com/95447782/152638733-b8a1b642-7250-406c-ba6e-2241208b3f1d.png)

![image](https://user-images.githubusercontent.com/95447782/152638736-9f5acc31-cad4-4307-8fc7-ea8dd6436e4b.png)



Hence increasing current mirror ratio can help increase frequency and Kvco.




Increasing inverter drive strength:
-----
Making inverters minimum length.

Leakage not much of a concern since top and bottom mirror devices are 0.18um length.

For a fixed mirror ratio, show effect of changing inverter drive strength (0.18um L vs 0.15um L).

Freq goes up significantly.

But duty cycle starts to distort.
And peak to peak swing goes down significantly (if mirror ratio also increased).


Kvco:
--------
Show table of Kvco for each Design point.


Summary
--------
Show curves of F vs V for all design points so far.
* Looks like design with mirrors at 1.6u/0.18u and min length inverters may be an ok tradeoff for relatively high speed, and oscillator internal phases not too distorted.
* Possibly reduce mirror ratio to help reduce duty cycle distortion a bit without losing too much speed.

Further work:
* Rising edge is slower, look into making PMOS stronger than NMOS in delay cells.

* Maybe that way we can square the waveform better, and from there maybe we can try to go even faster with larger W on delay cells? But drain capacitance may increase and thus reduce speed? So perhaps the way to go from there may be increase mirror ratio.

* Also look at reducing inverter W, since that may reduce drain cap, if that dominates speed then speed may go up

* But can it drive the output buffer then? Maybe reduce output buffer 1st stage... Investigate effect of output buffer. More strength better? But more capacitance? So whats the best trade off. Etc.
