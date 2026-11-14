# CAT5C — Stepper Motor Speed and Direction Control

## EXP / DATE
CAT5 — 10/08/2026

## NAME OF EXP
Control stepper motor stepping sequence, direction and speed using 8051 timer interrupts.

## HARDWARE SETUP / PLATFORM
AT89S52, stepper motor with a suitable driver, speed button P3.2, direction button P3.3, Port 1 upper-nibble driver outputs, 11.0592 MHz crystal, Keil C51. Never drive motor windings directly from MCU GPIO.

## TASK NO
CAT5C — cycle through slow, medium and fast stepping and reverse the sequence direction.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Identify the stepper motor and compatible driver. Confirm the driver's input order matches step_seq[].
2. Connect the four driver inputs to the Port 1 upper-nibble outputs used by the code.
3. Connect motor power to the driver as specified by its datasheet and share ground with the MCU where required.
4. Connect active-low speed and direction buttons to P3.2 and P3.3.
5. Open TASK5C.uvproj, build and program the HEX file.
6. Reset the MCU. The timer begins advancing through the four-step sequence.
7. Press and release the speed button to cycle Slow (100 ms), Medium (50 ms) and Fast (10 ms).
8. Press and release the direction button to reverse the sequence.
9. Observe motor direction and speed. If the motor vibrates without rotating, switch off power and check coil pairing and driver sequence.
10. Do not alter motor wiring while energized.

## HOW THE CODE WORKS
step_seq[] defines the four output patterns. Timer 0 provides a nominal 1 ms tick. ms_count determines when the next motor step occurs. speed_idx selects the interval; dir_cw selects forward or reverse index movement. The foreground loop debounces the two buttons.

## TROUBLESHOOTING
Check driver supply, common ground, coil order, motor current rating, sequence and output mapping. Disconnect power if the motor overheats.

## INFERENCE
The task demonstrates timer-scheduled motor stepping with independent speed and direction controls.
