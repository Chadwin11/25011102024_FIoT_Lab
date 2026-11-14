# CAT12 — Task 12B: Button State Remembrance

## EXP
CAT12 — 23/10/2026

## NAME OF EXP
Read the Nucleo-F401RE user button and toggle the onboard LED once per valid press.

## HARDWARE SETUP / PLATFORM
STM32 Nucleo-F401RE, onboard user button B1 on PC13 (active-low), onboard green LED LD2 on PA5, STM32 HAL and Keil MDK-ARM.

## TASK NO
Task 12B — detect a button press edge, debounce it, and retain the resulting LED state after release.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Connect the Nucleo-F401RE to the PC through ST-LINK.
2. Use the onboard B1 button and LD2 LED; no external switch or LED is required for the configured board.
3. Open the CubeMX project and check PC13 input with pull-up and PA5 push-pull output.
4. Open the Keil project, build, and download the firmware.
5. Reset the board and note the initial LED state.
6. Press B1 briefly and release it. The code detects a falling edge on PC13 (SET to RESET).
7. The firmware checks that more than 50 ms has elapsed since the previous accepted press, flips led_state, and writes the new state to PA5.
8. Press B1 again. The LED should change to the opposite state.
9. Keep the button released. The LED should remain in its last state because the program stores the state in led_state rather than following the instantaneous button level.
10. Repeat several times and note any missed or repeated presses.

## HOW THE CODE WORKS
prev_btn stores the previous PC13 sample. A transition from SET to RESET indicates a press because B1 is active-low. HAL_GetTick() provides the debounce interval. led_state ^= 1 toggles the stored state, and HAL_GPIO_WritePin() applies it to PA5.

## EXPECTED OBSERVATION
Each valid press toggles LD2 once. Releasing the button does not change the LED state.

## TROUBLESHOOTING
If press detection is inverted, verify the active-low behavior of B1. If presses are repeated, inspect edge detection and debounce timing. If the LED is inverted, verify the board's LED polarity.

## INFERENCE
The experiment demonstrates edge detection, simple debounce timing, and state retention.
