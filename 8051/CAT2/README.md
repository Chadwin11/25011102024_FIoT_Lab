# CAT2 — 8051 Tool-Chain Setup and LED Blink

## EXP / DATE
CAT2 — 20/07/2026

## NAME OF EXP
8051 development environment bring-up and bare-metal LED blinking.

## HARDWARE SETUP / PLATFORM
AT89S52, 11.0592 MHz crystal, LED on P1.0 (as defined in week2_l.c), Keil µVision and a compatible programmer.

## TASK NO
CAT2 — build, program and verify a periodic LED output.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Power the AT89S52 board using its specified supply and identify the LED connected to P1.0.
2. Connect the programmer to the board in the correct orientation and connect it to the computer.
3. Open week2.uvproj in Keil µVision.
4. Open week2_l.c and verify the LED mapping: sbit LED = P1^0.
5. Build the project. Resolve missing C51 toolchain or target-device configuration if reported.
6. Program the generated HEX file to the AT89S52.
7. Reset the board and observe the LED connected to P1.0.
8. The code inverts the LED output and waits approximately 500 ms before repeating.
9. Record the visible blink interval and confirm that the correct HEX file was programmed.

## HOW THE CODE WORKS
reg51.h provides 8051 register definitions. delay_ms() uses nested software loops to approximate a millisecond delay for the stated crystal. main() repeatedly inverts P1.0 and waits 500 ms.

## EXPECTED OBSERVATION
The P1.0 LED alternates between ON and OFF. Visible polarity depends on the board LED circuit.

## TROUBLESHOOTING
Check power, programmer orientation, target selection, P1.0 wiring, LED polarity and oscillator frequency. Software-delay timing changes with oscillator and compiler settings.

## INFERENCE
This task introduces the 8051 build-program-observe workflow and direct port-bit control without an Arduino API, HAL or RTOS.
