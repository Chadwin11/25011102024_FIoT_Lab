# CAT4 — Matrix Keypad, Seven-Segment Display and LED Modes

## EXP / DATE
CAT4 — 03/08/2026

## NAME OF EXP
Matrix keypad scanning with seven-segment digit display and LED pattern control.

## HARDWARE SETUP / PLATFORM
AT89S52, keypad scanned through Port 2, seven-segment display driven by P0, LEDs driven by P1, Keil C51.

## TASK NO
CAT4 — detect a keypad key, display numeric keys and invoke the LED operation assigned to the key.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Open week4.uvproj and inspect week4_logic.c.
2. Wire the keypad rows/columns to match the P2 values written in keypad_scan(). The routine drives P2 patterns 0x7F, 0xBF, 0xDF and 0xEF and reads P2.3, P2.2 and P2.1.
3. Connect the seven-segment segment inputs to P0 according to the physical circuit and display type.
4. Connect the LED bank to the P1 outputs used by the program (P1.1–P1.4).
5. Check whether the 8051 board provides the required Port 0 pull-ups. Add external pull-ups only as required by the board/display circuit.
6. Build the project and program the HEX file.
7. Reset the MCU and press keys 0–9 one at a time.
8. Check that numeric keys are represented by seg_table on the seven-segment display.
9. Test keys 1–4 for individual LED outputs; key 5 running pattern; key 6 alternating pattern; key 7 binary count; key 8 all-LED blink; key 9 all off; key 0 reset.
10. Release each key before pressing another. Observe whether a new key interrupts an active pattern.

## HOW THE CODE WORKS
keypad_scan() drives one row low at a time and detects a low column. last_key prevents a held key from being processed repeatedly. display_digit() writes the segment lookup value to P0. led_control() dispatches the requested pattern function.

## KEY ACTIONS
| Key | Operation |
|---|---|
| 1–4 | Individual LED outputs |
| 5 | Running LED |
| 6 | Alternating LEDs |
| 7 | Binary count |
| 8 | All LEDs blink |
| 9 | All LEDs off |
| 0 | Reset outputs and display 0 |

## TROUBLESHOOTING
Check keypad row/column orientation, seven-segment common-anode/common-cathode type, Port 0 pull-ups, LED polarity and P1 mapping.

## INFERENCE
The experiment combines matrix scanning, lookup-table display encoding and reusable LED-control routines.
