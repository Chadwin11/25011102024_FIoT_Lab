# CAT5B.2 — Button-Selectable Square-Wave Frequency

## EXP / DATE
CAT5 — 10/08/2026

## NAME OF EXP
Generate square waves at selectable frequencies using Timer 0.

## HARDWARE SETUP / PLATFORM
AT89S52, 11.0592 MHz crystal, waveform output P1.1, active-low mode button P3.2, Keil C51, Timer 0 Mode 1. Use an oscilloscope or logic analyzer.

## TASK NO
CAT5B.2 — cycle through five timer reload settings using a push-button.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Open TASK5B_2.uvproj and inspect main.c.
2. Connect P1.1 to an oscilloscope input and connect instrument ground to MCU GND.
3. Connect the mode button to P3.2 in the active-low arrangement expected by the source.
4. Build and program the HEX file.
5. Reset the MCU. freq_mode starts at zero.
6. Observe the initial square wave on the oscilloscope.
7. Press and release the button. The source debounces the press, advances freq_mode, waits for release and debounces again.
8. Repeat to cycle through the five reload table entries.
9. Measure and record each output frequency with the oscilloscope.

## HOW THE CODE WORKS
th_table and tl_table contain timer preload values. The ISR reloads Timer 0 and toggles WAVE_OUT. Each interrupt is one half-cycle, so the measured output frequency depends on twice the interrupt interval.

## EXPECTED OBSERVATION
The output frequency changes when the button is pressed. The source comments identify nominal settings of 100 Hz, 500 Hz, 1 kHz, 2 kHz and 5 kHz; verify actual values on the instrument.

## TROUBLESHOOTING
Check P1.1, common ground, timer interrupt setup, button pull-up and crystal frequency. If measured frequencies differ, review the timer machine-cycle and half-period calculation.

## INFERENCE
The experiment demonstrates timer-based waveform generation and button-controlled frequency selection.
