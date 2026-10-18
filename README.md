![](../../workflows/gds/badge.svg) ![](../../workflows/docs/badge.svg)

# autocomp — load-adaptive sub-µW op-amp (Tiny Tapeout TTSKY26d, SKY130A, 2x2 analog tile)

A two-stage Miller op-amp, wired as a unity-gain follower from `ua[0]` to `ua[1]`, that picks its own second-stage current for the load it drives. A 4-bit code scales the second-stage current and the nulling resistor together. an on-chip sequencer steps the input by about 9.5 mV, an auto-zeroed overshoot detector watches the output, and a successive-approximation search keeps the lowest code whose step stays inside the detector's threshold. 


