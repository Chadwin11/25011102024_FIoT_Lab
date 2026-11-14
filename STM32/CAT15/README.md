# CAT15 — BME280 Environmental Monitoring with MQTT and Node-RED

## EXP
CAT15

## NAME OF EXP
BME280 sensor interfacing with STM32, ESP8266 Wi-Fi connectivity, MQTT messaging, and Node-RED dashboard analytics.

## HARDWARE SETUP / PLATFORM
- MCU target: STM32F401RET6, as configured in IOT_project.ioc.
- Sensor: BME280.
- Wireless module: ESP8266.
- Development tools: STM32CubeMX and Keil MDK-ARM.
- I2C1: PB6 (SCL), PB7 (SDA).
- USART1: PA9 (TX), PA10 (RX).
- USART2: PA2 (TX), PA3 (RX).
- MQTT broker in the Node-RED flow: broker.emqx.io:1883.
- MQTT topic used by firmware: college/weather/bme280.

## TASK NO
CAT15 — acquire BME280 environmental readings and publish them through MQTT for Node-RED dashboard analytics.

## CIRCUIT DIAGRAM
A file named circuit.png was not present in the inspected CAT15 task directory, so no circuit image is embedded here. Use IOT_project.ioc for the configured MCU pin assignments and verify the physical wiring against the actual hardware.

## BEFORE YOU START
1. Confirm the BME280 module supports 3.3 V logic and power.
2. Connect BME280 SDA to PB7 and SCL to PB6; connect sensor GND to board GND and power it from the supported 3.3 V rail.
3. Connect ESP8266 UART to the configured USART1 pins (PA9/PA10) and share ground.
4. Ensure the ESP8266 has a stable supply capable of handling its current peaks.
5. The source includes Wi-Fi credentials in the code. Replace them with local credentials privately before use; do not publish real passwords in a public repository.

## STEP-BY-STEP PROCEDURE
1. Open IOT_project.ioc in STM32CubeMX and confirm the target is STM32F401RET6.
2. Confirm I2C1, USART1 and USART2 are enabled and their pins match the table above.
3. Open the Keil project under MDK-ARM and check that Core source, Bosch BME280 API files, and ESPLib files are included.
4. Build the project. Resolve missing include paths or source-file references before downloading.
5. Flash the firmware to the Nucleo board and reset it.
6. Firmware probes the BME280 at address 0x76 and then 0x77. If neither responds, it reports an error and enters Error_Handler().
7. The BME280 driver is initialized with I2C read/write callbacks. Temperature, pressure and humidity oversampling are configured to 1x, filter is disabled, and the sensor is placed in normal mode.
8. The ESP8266 is initialized in station mode, then the firmware attempts to join the configured Wi-Fi network.
9. The firmware opens a TCP connection to broker.emqx.io on port 1883 and sends an MQTT CONNECT packet.
10. In the main loop, the firmware reads BME280 data, formats temperature, pressure and humidity into a JSON string, and publishes the JSON to college/weather/bme280 using QoS 0.
11. Open Node-RED and import node_red_flow.json from this folder.
12. Verify the MQTT broker node uses broker.emqx.io port 1883 and the MQTT-in node subscribes to college/weather/bme280.
13. Deploy the flow. Inspect the debug output and dashboard widgets for live values, charts and derived environmental indicators.
14. If you are testing without the physical sensor, use the provided Inject nodes in Node-RED to send sample payloads through the dashboard function flow; these test injects do not prove the physical sensor link.

## HOW THE CODE WORKS
main.c initializes HAL, clocks, GPIO, I2C and UART peripherals. It detects the BME280 address, configures the Bosch API callbacks, applies sensor settings, initializes the ESP8266 and MQTT connection, then reads and publishes a JSON telemetry message periodically. node_red_flow.json subscribes to the MQTT topic, parses the payload, calculates altitude and climate classifications, and routes values to dashboard text, charts and gauges.

## EXPECTED OBSERVATION
When the sensor, Wi-Fi, broker and Node-RED flow are all connected, Node-RED should receive JSON containing temperature, pressure and humidity and update the dashboard. The source includes sample Inject nodes for testing the dashboard logic separately.

## TROUBLESHOOTING
- BME280 not detected: check SDA/SCL, PB6/PB7, 3.3 V, GND and I2C address.
- ESP8266 cannot join Wi-Fi: verify local credentials, 2.4 GHz network availability and power supply.
- MQTT connection fails: check internet connectivity, broker host/port, and ESP8266 TCP response.
- No dashboard updates: confirm exact MQTT topic match and that the flow is deployed.
- Dashboard test data appears but sensor data does not: this indicates the Node-RED inject path works, not necessarily the hardware telemetry path.

## INFERENCE
CAT15 combines embedded sensor acquisition, a custom Wi-Fi/MQTT interface, JSON telemetry, and Node-RED analytics into an end-to-end IoT monitoring pipeline.
