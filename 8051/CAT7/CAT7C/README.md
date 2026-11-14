# CAT7C — Keypad-Controlled LCD Character Movement

## EXP / DATE
CAT7 — 24/08/2026

## NAME OF EXP
Use a 4×4 matrix keypad to move a character across a 16×2 LCD.

## HARDWARE SETUP / PLATFORM
AT89S52, 16×2 LCD using lcd.c/lcd.h, 4×4 keypad rows P1.0–P1.3 and columns P1.4–P1.7 as defined in main.c, Keil C51.

## TASK NO
CAT7C — move the displayed asterisk using directional keypad keys.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Open TASK7C.uvproj.
2. Inspect lcd.h/lcd.c for LCD pins and main.c for keypad pin assignments.
3. Connect keypad rows to P1.0–P1.3 and columns to P1.4–P1.7.
4. Connect the LCD according to lcd.h. Check that the LCD wiring does not conflict with keypad port usage.
5. Build the project with main.c and lcd.c.
6. Program the HEX file and reset the board.
7. Confirm an asterisk appears at the first LCD position.
8. Press 2 to move up, 8 down, 4 left and 6 right.
9. Observe the asterisk move one position at a time. The program restricts the cursor to two rows and 16 columns.
10. Release each key before the next press.

## HOW THE CODE WORKS
keypad_scan() drives one row low at a time and reads the column nibble. A debounce delay confirms a key and the function waits for release. The program erases the old asterisk, updates row/column coordinates and draws it at the new position.

## KEY MAP
| Key | Movement |
|---|---|
| 2 | Up |
| 8 | Down |
| 4 | Left |
| 6 | Right |

## TROUBLESHOOTING
If directions are wrong, verify row/column orientation. If keys repeat, inspect debounce and release handling. If LCD coordinates are wrong, check lcd_goto() and display dimensions.

## INFERENCE
The task combines keypad scanning, debouncing, coordinate state and LCD cursor control.
