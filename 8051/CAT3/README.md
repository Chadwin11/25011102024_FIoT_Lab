# CAT3 — Switch-Controlled LED Modes

## EXP / DATE
CAT3 — 27/07/2026

## NAME OF EXP
8051 GPIO input, push-button debouncing and LED pattern state machine.

## HARDWARE SETUP / PLATFORM
AT89S52, four LEDs driven by the lower nibble of P1 in cat_03.c, active-low push-button input P2.6, Keil C51. The folder also contains switch_logic.c, a separate simple P2.0-to-P1.0 example.

## TASK NO
CAT3 — switch between running LED, binary counter, alternating pattern and all-LED flash modes.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Open Switch_logic_28.7.uvproj in Keil and inspect which C source files are included in the build.
2. For the four-mode assessment, use cat_03.c. Do not confuse it with switch_logic.c, which is a separate single-LED example.
3. Connect four LEDs to P1.0–P1.3 using suitable current-limiting resistors.
4. Connect the push-button to P2.6 in the active-low arrangement expected by button_pressed().
5. Build the project and resolve compiler errors.
6. Program the generated HEX file and reset the board.
7. Press and release the button once to advance to the next mode.
8. Observe the running LED pattern, then the 0–15 binary count, then alternating 0101/1010, then all four LEDs flashing.
9. Press again to return to the first mode.
10. Record the actual board wiring and observations.

## HOW THE CODE WORKS
button_pressed() checks P2.6, waits 20 ms, checks again, then waits for release. state stores the selected mode. Each state function updates the lower four P1 bits. The main loop dispatches the selected function.

## EXPECTED OBSERVATION
Each accepted button press advances one LED mode.

## TROUBLESHOOTING / SOURCE NOTE
The current cat_03.c contains delay_ms(50 0) in state_all_flash(), which is invalid C syntax. Confirm the intended delay and correct this typo before building. Verify active-low button wiring. switch_logic.c only mirrors P2.0 to P1.0 and does not implement the four modes.

## INFERENCE
The task demonstrates GPIO polling, switch debouncing and finite-state control on an 8051.
