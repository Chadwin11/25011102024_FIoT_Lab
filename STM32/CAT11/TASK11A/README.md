# CAT11 — Task 11A: ESP8266 TCP Server with HTTP Response

## EXP
CAT11

## DATE
14/10/2026

## NAME OF EXP
HTTP server using STM32 and Wemos D1 Mini ESP8266 with AT commands.

## HARDWARE SETUP / PLATFORM
- STM32F103C8T6 Blue Pill
- Wemos D1 Mini (ESP8266)
- STM32CubeMX and Keil MDK-ARM
- Browser as HTTP client

## TASK NO
Task 11A — configure the ESP8266 TCP server and return an HTTP response.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## CORE LOGIC / PSEUDOCODE / CODE BASE
1. Configure the ESP8266 for multiple TCP connections.
2. Start the TCP server on port 80.
3. Receive incoming client data through ESP8266 serial notifications.
4. Identify the connection ID and HTTP request.
5. Construct an HTTP response with content type and content length.
6. Send the response using the ESP8266 send-data command and close the client connection.

The task folder contains the STM32CubeMX configuration, Core source, Drivers, and MDK-ARM project directory.

## INFERENCE
The project code is structured to use the STM32 and ESP8266 as an embedded HTTP server for browser requests. This describes the implementation approach and does not claim a live network test result.
