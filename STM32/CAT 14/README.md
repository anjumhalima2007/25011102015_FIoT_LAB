# EXPERIMENT DETAILS

**EXP:** CONTINUOUS LAB EVALUATION – 13

**DATE:** 27/10/2026

**NAME OF EXP:** BME280 Sensor Interfacing Using I²C and MQTT for Node-RED Analytics

**HARDWARE SETUP / PLATFORM:** CubeMX + Keil MDK + STM32 Nucleo Development Board + Debugger + BME280 Sensor + ESP8266 Wi-Fi Module

---

## TASK 13 – Sensor Interfacing (BME280) – MQTT – Node Analytics

### 1. Circuit Diagram

The experiment uses the BME280 environmental sensor interfaced with the STM32 development board through the I²C communication protocol. The ESP8266 Wi-Fi module is used to establish network connectivity and transmit sensor data to an MQTT broker.

- **Development Board:** STM32 Nucleo Development Board
- **Sensor:** BME280 Environmental Sensor
- **Communication Protocol:** I²C (I2C1)
- **Wi-Fi Module:** ESP8266
- **UART Communication:** USART1
- **MQTT Broker:** broker.emqx.io
- **MQTT Port:** 1883
- **MQTT Topic:** stm32/da

**Connections:**

- BME280 SDA and SCL pins are connected to the STM32 I²C1 interface.
- ESP8266 TX and RX pins are connected to the STM32 USART1 interface.
- VCC and GND connections are provided to the respective modules.

### 2. Core Logic / Pseudocode / Code Base

**Working Principle:**

The experiment demonstrates environmental parameter monitoring using the BME280 sensor and wireless data transmission using MQTT.

The BME280 sensor measures temperature, pressure, and humidity. The STM32 communicates with the sensor through the I²C protocol using STM32 HAL libraries and the BME280 driver.

The ESP8266 is initialized using the custom-built ESP8266 library and connected to a Wi-Fi network. It establishes a TCP connection with the MQTT broker.

The sensor readings are converted into JSON format and published to the MQTT topic `stm32/da` every 1000 milliseconds. The transmitted data can be received by Node-RED for monitoring and analytics.

**Pseudocode:**

1. Initialize the HAL library and configure the system clock.
2. Initialize GPIO, I²C1, and USART1 peripherals.
3. Initialize the BME280 sensor using the I²C interface.
4. Configure temperature, pressure, and humidity oversampling settings.
5. Set the BME280 sensor to normal operating mode.
6. Initialize the ESP8266 module in station mode.
7. Connect the ESP8266 to the Wi-Fi network.
8. Establish a TCP connection with the MQTT broker.
9. Initialize MQTT communication and connect to the broker.
10. Read temperature, pressure, and humidity values from the BME280 sensor.
11. Convert the sensor readings into JSON format.
12. Publish the JSON payload to the MQTT topic `stm32/da`.
13. Repeat the process every 1000 milliseconds continuously.

**Code Base:**

- `HAL_I2C_Mem_Read()` and `HAL_I2C_Mem_Write()` are used for BME280 sensor communication.
- `bme280_init()` initializes the BME280 sensor.
- `bme280_set_sensor_settings()` configures sensor oversampling and filter settings.
- `bme280_get_sensor_data()` retrieves compensated temperature, pressure, and humidity readings.
- `ESP8266_Init()` initializes the ESP8266 module.
- `ESP8266_wifiConnect()` connects the module to the Wi-Fi network.
- `ESP8266_portConnect()` establishes the TCP connection with the MQTT broker.
- `MQTT_connectBroker()` establishes the MQTT connection.
- `buildJson()` formats the sensor readings into JSON format.
- `MQTT_publishTopic()` publishes the sensor data to the MQTT topic.
- `HAL_GetTick()` is used to maintain the 1000 ms publishing interval.

### 3. Inference

The BME280 sensor was successfully interfaced with the STM32 development board using the I²C communication protocol. Temperature, pressure, and humidity readings were obtained using the BME280 driver and STM32 HAL libraries.

The ESP8266 established Wi-Fi connectivity and connected to the MQTT broker. The sensor readings were converted into JSON format and published to the MQTT topic `stm32/da` at regular one-second intervals.

Thus, the experiment demonstrates environmental data acquisition, wireless MQTT communication, and the transmission of sensor data for Node-RED-based monitoring and analytics.
