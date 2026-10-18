<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

autocomp is a two-stage Miller op-amp (PMOS input pair, NMOS second stage, 0.99 pF Miller capacitor) wired as a unity-gain follower from ua[0] (VIN) to an internal output OUT, which reaches ua[1] (VOUT) through an on-chip unity-gain buffer while OUT_EN = 1. A 4-bit code K sets the second-stage current to (1 + K) x 8 unit PMOS legs and switches the nulling resistor to about 2.98 MOhm / (1 + K), so the second-stage transconductance scales with K while Rz x gm2 stays constant. Higher codes give more phase margin with a capacitive load and draw more current.

## How to test

Manual mode (start here):

1. Power the tile at 1.8 V. Set MAN = 1 (ui[1]), put a code on KE0 to KE3 (uio[0:3]) and read it back on KO0 to KO3 (uo[0:3]).
2. Choose an on-chip load with S0 to S3 (ui[3:6]), or 0 for none.
3. Set OUT_EN = 1 (ui[2]) to connect the output to ua[1] through the pad buffer. The demo board pulls each analog pin down with 10 MOhm, which takes 80 nA at 0.8 V; the buffer supplies it, so no fixture is needed and a 10x scope probe (10 MOhm, about 15 pF) can go straight on ua[1]. A 1x probe (1 MOhm, about 100 pF) also works but pulls VOUT about 14 mV low and takes up to about 1 point off the overshoot. Bias VIN (ua[0]) near 0.8 V and keep it below about 1.0 V, apply a small step (for example 0.80 V to 0.81 V, or to 0.90 V) and watch VOUT for overshoot and settling. VOUT shows OUT within the buffer's offset (a few mV) and about 1.1 % less step, so the overshoot at ua[1] matches the table above within about 0.05 point.
4. Repeat for several codes and loads: higher codes settle faster and draw more current.

## External hardware

The 1.8 V supply of the demo board, a signal generator or DAC for VIN, an oscilloscope with a 10x probe on VOUT (ua[1]), a 100 kHz clock on clk (from the demo board) for calibration with CLK_SEL = 1, and a picoammeter or a voltmeter of 1 GOhm or more on ua[2] for the bias monitor.