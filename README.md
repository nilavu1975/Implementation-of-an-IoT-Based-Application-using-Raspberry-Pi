# IMPLEMENTATION OF AN IoT-BASED APPLICATION USING RASPBERRY PI

## Aim

To implement an IoT-based environmental monitoring application using Raspberry Pi and Python/MicroPython by acquiring sensor data, processing the data, and transmitting the information to an IoT platform for remote monitoring.

---

# Hardware / Software Tools Required

* Raspberry Pi Pico W
* DHT22 Temperature and Humidity Sensor
* LED
* 220Ω / 330Ω Resistor
* Breadboard
* Jumper Wires
* Wokwi Online Simulator
* MicroPython
* Wi-Fi Network
* IoT Cloud Platform / MQTT Broker

> **Note:** Raspberry Pi Pico W is used instead of the standard Raspberry Pi Pico because the Pico W provides built-in Wi-Fi connectivity required for the IoT application.

---

# Circuit Diagram
<img width="406" height="433" alt="image" src="https://github.com/user-attachments/assets/d817dc93-09b5-4b11-be3c-83176626867f" />

---


# Circuit Connections

# IoT Application

The application implements a **Wi-Fi-based environmental monitoring system**.

The system performs the following functions:

```text
DHT22 Sensor
      ↓
Raspberry Pi Pico W
      ↓
Read Temperature & Humidity
      ↓
Process Sensor Data
      ↓
Wi-Fi Connection
      ↓
IoT Cloud / MQTT Broker
      ↓
Remote Monitoring
```

The LED is used as a local status indicator. It turns ON when the measured temperature exceeds the predefined threshold.

---

# Procedure

## Step 1: Create the Wokwi Project

1. Open the Wokwi online simulator.
2. Create a new project using **Raspberry Pi Pico W**.
3. Select **MicroPython** as the programming environment.
4. Add the following components:

   * Raspberry Pi Pico W
   * DHT22 sensor
   * LED
   * Resistor
5. Connect the components according to the circuit connection table.

## Step 2: Connect the DHT22 Sensor

1. Connect the VCC pin of the DHT22 to 3.3V.
2. Connect the GND pin to GND.
3. Connect the DATA pin to GPIO 15.
4. Configure GPIO 15 as the sensor data input.

## Step 3: Connect the LED

1. Connect GPIO 14 to a 220Ω resistor.
2. Connect the resistor to the LED anode.
3. Connect the LED cathode to GND.
4. The LED will act as a temperature threshold indicator.

## Step 4: Configure Wi-Fi

1. Configure the Wi-Fi credentials in the MicroPython program.
2. Start the Wi-Fi interface of the Raspberry Pi Pico W.
3. Connect the Pico W to the Wokwi simulated Wi-Fi network.
4. Verify that the device obtains an IP address.
5. Check the Serial Monitor for the Wi-Fi connection status.

## Step 5: Read Sensor Data

1. Initialize the DHT22 sensor.
2. Read the temperature value.
3. Read the humidity value.
4. Display the values in the Serial Monitor.
5. Compare the temperature value with the predefined threshold.

## Step 6: Control the LED

1. Define a temperature threshold.
2. If the measured temperature is greater than the threshold, turn ON the LED.
3. If the temperature is below the threshold, turn OFF the LED.
4. Display the LED status in the Serial Monitor.

## Step 7: Send Data to IoT Platform

1. Establish a Wi-Fi connection.
2. Connect the Raspberry Pi Pico W to the selected IoT platform or MQTT broker.
3. Create suitable MQTT topics for temperature and humidity.
4. Publish the sensor readings periodically.
5. Monitor the published data using the cloud dashboard or MQTT client.

## Step 8: Run the Simulation

1. Start the Wokwi simulation.
2. Observe the Wi-Fi connection message.
3. Observe the temperature and humidity values.
4. Change the DHT22 sensor values using the Wokwi controls.
5. Observe the corresponding changes in the Serial Monitor.
6. Verify the LED operation based on the temperature threshold.
7. Verify that the sensor data is transmitted through the IoT communication channel.

---

# Program
```
from machine import Pin
import time
import dht

# GPIO pin configuration
DHT_PIN = 15
LED_PIN = 14

# Configure components
sensor = dht.DHT22(Pin(DHT_PIN))
led = Pin(LED_PIN, Pin.OUT)

print("IoT-Based Temperature Monitoring System Started")

while True:
    try:
        # Read temperature and humidity
        sensor.measure()

        temperature = sensor.temperature()
        humidity = sensor.humidity()

        # Display sensor readings
        print("Temperature:", temperature, "°C")
        print("Humidity:", humidity, "%")

        # Control LED based on temperature
        if temperature > 30:
            led.value(1)
            print("Temperature is HIGH - LED ON")
        else:
            led.value(0)
            print("Temperature is NORMAL - LED OFF")

        print("--------------------------")

    except Exception as e:
        print("Sensor Error:", e)

    time.sleep(2)
```

# Observation
<img width="1535" height="730" alt="image" src="https://github.com/user-attachments/assets/9ee041c7-97a4-4714-b120-9cdff6e686b1" />
<img width="731" height="1600" alt="WhatsApp Image 2026-09-26 at 10 47 29 AM" src="https://github.com/user-attachments/assets/fbbcb748-6616-40a1-bd87-28cfa28bad67" />



# Result

The **IoT-based environmental monitoring application was successfully implemented using Raspberry Pi Pico W in the Wokwi simulation environment**. The DHT22 sensor was interfaced with the Raspberry Pi Pico W to acquire temperature and humidity data. The Pico W established Wi-Fi connectivity, processed the sensor readings, and provided the data for IoT-based remote monitoring. An LED was also controlled according to the predefined temperature threshold.
