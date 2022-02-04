# vco
High Speed VCO in Skywater 130nm

CS-VCO
====
5-stage vs 3-stage
------
Higher frequency can be achieved with 3 stages rather than 5 stages.

*Curve of F vs V for 3 vs 5 stages*



From now on we focus on 3 stages.


Increasing current mirror ratio:
------
Mirror ratio increased from 1.29 to 1.6 to 2.4
Show effect of F and current.

Not much current increase.


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
