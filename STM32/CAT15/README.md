# CAT15 — BME280 Environmental Monitoring with MQTT and Node-RED

## EXP
CAT15

## NAME OF EXP
BME280 sensor interfacing with STM32, ESP8266 Wi-Fi connectivity, MQTT messaging, and Node-RED dashboard analytics.

## HARDWARE SETUP / PLATFORM
- Microcontroller target: STM32F401RET6 (configured in IOT_project.ioc)
- Sensor: BME280 environmental sensor
- Wireless module: ESP8266
- Development configuration: STM32CubeMX and Keil MDK-ARM
- Sensor interface: I2C1, PB6 (SCL) and PB7 (SDA)
- ESP8266 interface: USART1, PA9 TX and PA10 RX
- Terminal/debug interface: USART2, PA2 TX and PA3 RX
- MQTT broker in Node-RED flow: broker.emqx.io:1883
- MQTT topic published by firmware: college/weather/bme280

## TASK NO
CAT15 — acquire BME280 environmental measurements on the STM32 and publish them over MQTT for visualization and analytics in Node-RED.

## CORE LOGIC / PSEUDOCODE / CODE BASE
1. Initialize HAL, system clock, GPIO, I2C1, USART1, and USART2.
2. Probe the BME280 at I2C address 0x76 and then 0x77; enter the error handler if neither responds.
3. Configure the Bosch BME280 Sensor API with I2C read/write callbacks and a delay callback.
4. Configure temperature, pressure, and humidity oversampling to 1x, filter off, and normal operating mode.
5. Initialize the ESP8266 in station mode through USART1 and request Wi-Fi connection.
6. Open a TCP connection to the configured MQTT broker and send the MQTT connection packet using the custom ESP library.
7. Read temperature, pressure, and humidity from the BME280.
8. Format the readings as JSON and publish to college/weather/bme280 using QoS 0.
9. Repeat the sensor-read and publish cycle after the firmware delay.

The accompanying Node-RED flow subscribes to college/weather/bme280 through the EMQX public broker. Its function node parses readings, derives altitude and environmental classifications, and sends values to dashboard text, chart, and gauge widgets. The flow also includes inject nodes for sample/test payloads.

## INFERENCE
The project combines I2C sensor acquisition, UART-based ESP8266 control, MQTT telemetry, and Node-RED dashboard processing. The firmware source documents the intended data path and publish loop; successful live broker delivery or hardware operation is not asserted here.

## PROJECT FILES
- IOT_project.ioc — STM32CubeMX configuration.
- Core/Src/main.c — BME280 initialization, sensor acquisition, ESP8266 setup, and MQTT publish loop.
- Core/Inc/main.h — application header.
- node_red_flow.json — Node-RED MQTT flow and dashboard logic.
- MDK-ARM/IOT_project.uvprojx — Keil MDK-ARM project.
- MDK-ARM/startup_stm32f401xe.s — startup assembly.
- dashboard_flow.jpg, dashboard_live_meters.png, dashboard_predictions_charts.jpg — dashboard-related images included in this folder.

No CAT15 evaluation date or circuit diagram is recorded here because a verified date and a file named circuit.png were not available in the CAT15 folder at inspection time.
