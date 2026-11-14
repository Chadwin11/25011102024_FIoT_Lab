# CAT12 — Task 12A: Nucleo-F401RE LED Bring-Up

## EXP
CAT12

## DATE
23/10/2026

## NAME OF EXP
STM32F401RE GPIO output bring-up using the on-board LED.

## HARDWARE SETUP / PLATFORM
- STM32 Nucleo-F401RE (STM32F401RET6)
- STM32CubeMX and Keil MDK-ARM
- On-board LED LD2 connected to PA5

## TASK NO
Task 12A — configure and toggle the on-board LED.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## CORE LOGIC / PSEUDOCODE / CODE BASE
1. Initialize the STM32 HAL and system clock.
2. Configure PA5 as a GPIO output.
3. Toggle PA5 in the main loop using the delay defined by the application.

## INFERENCE
The task demonstrates basic GPIO output control on the STM32F401RE. The code describes the LED toggle operation; no independent hardware test result is asserted here.
