**Constrained Device Application (Connected Devices)**

Lab Module 12

Description

**What the Implementation does**

The CDA now includes pitch sensor support and LED position control with dual input modes. Users can control an LED dot on the SenseHAT display either through joystick buttons (manual mode with green LED indicator) or by tilting the device using the pitch sensor (automatic mode with blue LED indicator). LED position data is published to the GDA via secure MQTT for cloud logging on the Ubidots platform.

PitchSensorEmulatorTask reads pitch orientation data from the SenseHAT IMU, converts the values from radians to degrees, and returns the data as SensorData objects. LEDDisplayActuator receives position commands as ActuatorData containing x and y coordinates within the 0-7 range and displays the LED dot at the specified location, using green to indicate manual control mode and blue to indicate tilt-based automatic mode.

**How it works**

In manual mode, users interact with the joystick to move the LED dot: pressing LEFT or RIGHT moves the dot horizontally, pressing UP or DOWN moves it vertically, and pressing the MIDDLE button toggles between manual and tilt control modes. In tilt mode, the pitch sensor continuously reads the device orientation angle and automatically maps it to the LED vertical position, creating an intuitive interface where tilting the device forward moves the LED down and tilting backward moves it up.
When the LED position changes, DeviceDataManager publishes the current x and y coordinates along with the control mode to the MQTT topic piot/cda/actuator/ledposition as a JSON message. This data flows through the GDA to the Ubidots cloud platform where it can be visualized and analyzed in real-time.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule12

**UML Design Diagram(s)**

The UML class diagram shows the relationships between the following classes: ConstrainedDeviceApp , DeviceDataManager , SensorAdapterManager , ActuatorAdapterManager , PitchSensorEmulatorTask , LEDDisplayActuator , MqttClientConnector , SensorData , ActuatorData, ConfigUtil, and SenseHAT (provides hardware interface for IMU, LED matrix, and joystick).
<img width="988" height="629" alt="Lab12CDAuml" src="https://github.com/user-attachments/assets/3fa8b0ad-a30a-4487-a522-0e751a2d65a0" />



**Verification**
Screenshots shows that the dashboard displays 9 variables in real-time from Lab 12 CDA system: three environmental sensors (temperature: 25°C, humidity: 22%, pressure: 378.3 mbar), LED position coordinates (horizontal: 4, vertical: 3), actuator states, and system performance metrics. All variables show recent activity (3-5 minutes ago), confirming the CDA-GDA-Ubidots data pipeline is fully operational with live sensor telemetry and LED control position tracking being successfully transmitted to the cloud platform.
<img width="2070" height="1123" alt="Screenshot From 2025-11-05 23-16-11" src="https://github.com/user-attachments/assets/ad89c37c-e068-4d41-a492-549e8c6797d6" />

**Unit Tests:**

1. test_PitchSensorEmulatorTask 
2. test_LEDDisplayActuator. 

**Integration Tests:**
1. test_ConstrainedDeviceApp

