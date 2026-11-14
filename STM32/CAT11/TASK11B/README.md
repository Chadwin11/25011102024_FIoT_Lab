# CAT11 — Task 11B: Node-RED HTTP Client and JSON Telemetry

## EXP
CAT11 — 14/10/2026

## NAME OF EXP
Use Node-RED to request JSON telemetry from an STM32/ESP8266 HTTP endpoint.

## HARDWARE SETUP / PLATFORM
STM32F103C8T6 Blue Pill, Wemos D1 Mini ESP8266, Wi-Fi network, Node-RED, PC terminal, STM32 HAL and Keil MDK-ARM. The firmware returns JSON containing a node identifier and uptime in milliseconds.

## TASK NO
Task 11B — expose uptime telemetry over HTTP and retrieve it from Node-RED.

## CIRCUIT DIAGRAM
![Circuit Diagram](circuit.png)

## STEP-BY-STEP PROCEDURE
1. Complete the STM32-to-ESP8266 UART wiring and common ground from Task 11A.
2. Ensure the ESP8266 is connected to the same Wi-Fi network as the computer running Node-RED.
3. Build and flash the task firmware.
4. Reset the board. Firmware enables multiple TCP connections and starts a server on port 80.
5. Determine the ESP8266 IP address and verify that a browser on the same network can reach the endpoint.
6. Open Node-RED in a browser and import node_red_flow.json from this task folder if the flow file is present.
7. Open the HTTP Request node and set its URL to the endpoint on the ESP8266 IP address. Preserve the path used by the firmware (root path if no other route is implemented).
8. Connect the HTTP Request node to a Debug node, deploy the flow, and trigger the Inject node.
9. Inspect the response. Firmware formats a JSON body with node name STM32_BluePill and uptime_ms derived from HAL_GetTick().
10. Repeat the Inject action and confirm uptime increases between requests.

## HOW THE CODE WORKS
When the modem reports a client request using +IPD, the firmware extracts the link ID, creates a JSON object with the current tick count, adds HTTP status and Content-Type headers plus the correct Content-Length, sends the response using AT+CIPSEND, and closes the connection.

## EXPECTED OBSERVATION
Node-RED Debug should show a JSON response containing the node label and uptime_ms. This is the expected behavior from the source; verify it on the live network.

## TROUBLESHOOTING
Check Node-RED URL and ESP IP address, Wi-Fi network membership, TCP server startup, HTTP Request method, and exact endpoint path. If the Debug panel is empty, test with a browser first and inspect the serial modem output.

## INFERENCE
The task demonstrates how a low-cost embedded node can expose telemetry through HTTP and how Node-RED can consume it for automation or dashboarding.
