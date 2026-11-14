# CAT12 — Task 12C: Short-Press and Long-Press Classification

## EXP
CAT12 — 23/10/2026

## NAME OF EXP
Use the Nucleo-F401RE user button to distinguish short and long presses and control LD2.

## HARDWARE SETUP / PLATFORM
STM32 Nucleo-F401RE, B1 user button on PC13 (active-low), LD2 onboard LED on PA5, STM32 HAL, Keil MDK-ARM.

## TASK NO
Task 12C — short press toggles the LED; long press enables continuous blinking; short press while blinking stops the mode.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Connect the Nucleo board to the PC using ST-LINK.
2. Open the project and confirm PC13 is configured as input with pull-up and PA5 as output.
3. Build and flash the program.
4. Reset the board and wait for the initial state.
5. Press B1 for less than one second and release. The code classifies a press lasting at least 50 ms but less than 1000 ms as short and toggles LD2.
6. Press and hold B1 for at least one second, then release. The code sets blink_en and enters continuous blinking.
7. While blinking, press and release B1 briefly. The code clears blink_en and writes PA5 RESET.
8. Repeat a short press to toggle the LED again, and a long press to re-enter blinking.
9. Record the observed behavior and compare it with the source logic.

## HOW THE CODE WORKS
The firmware detects active-low press and release transitions on PC13. t_down stores the tick when the press begins. On release, duration is calculated using HAL_GetTick(). Durations below 50 ms are ignored; 50–999 ms are treated as short; 1000 ms or more enables blinking. In blink mode, the LED is toggled at 200 ms intervals without a blocking delay.

## IMPORTANT SOURCE NOTE
The current file contains more than one main() definition in the visible source content. A C project cannot link two application entry points. Before building, inspect Core/Src/main.c and retain the intended implementation for this task, removing or excluding any duplicate implementation. Do not assume a successful build until this is resolved.

## EXPECTED OBSERVATION
A valid short press toggles LD2; a long press enables blinking; a subsequent short press exits blinking and turns LD2 off.

## TROUBLESHOOTING
Check active-low button logic, debounce minimum, 1000 ms threshold, and 200 ms blink schedule. If compilation reports duplicate main, resolve the duplicate entry point first.

## INFERENCE
This task demonstrates elapsed-time classification and a small state machine using the HAL tick counter.
