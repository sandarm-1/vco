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
Looks like design with mirrors at 1.6u/0.18u and min length inverters may be an ok tradeoff for relatively high speed, and oscillator internal phases not too distorted.
