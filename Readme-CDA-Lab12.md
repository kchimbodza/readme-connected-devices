**Constrained Device Application (Connected Devices)**

Lab Module 11

Description

**What the Implementation does**

The CDA now includes pitch sensor support and LED position control with dual input modes. Users can control an LED dot on the SenseHAT display either through joystick buttons (manual mode with green LED indicator) or by tilting the device using the pitch sensor (automatic mode with blue LED indicator). LED position data is published to the GDA via secure MQTT for cloud logging on the Ubidots platform.

PitchSensorEmulatorTask reads pitch orientation data from the SenseHAT IMU, converts the values from radians to degrees, and returns the data as SensorData objects. LEDDisplayActuator receives position commands as ActuatorData containing x and y coordinates within the 0-7 range and displays the LED dot at the specified location, using green to indicate manual control mode and blue to indicate tilt-based automatic mode.

**How it works**

In manual mode, users interact with the joystick to move the LED dot: pressing LEFT or RIGHT moves the dot horizontally, pressing UP or DOWN moves it vertically, and pressing the MIDDLE button toggles between manual and tilt control modes. In tilt mode, the pitch sensor continuously reads the device orientation angle and automatically maps it to the LED vertical position, creating an intuitive interface where tilting the device forward moves the LED down and tilting backward moves it up.
When the LED position changes, DeviceDataManager publishes the current x and y coordinates along with the control mode to the MQTT topic piot/cda/actuator/ledposition as a JSON message. This data flows through the GDA to the Ubidots cloud platform where it can be visualized and analyzed in real-time.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-java/tree/labmodule12

**UML Design Diagram(s)**

The UML class diagram shows the relationships between the following classes: ConstrainedDeviceApp , DeviceDataManager , SensorAdapterManager , ActuatorAdapterManager , PitchSensorEmulatorTask , LEDDisplayActuator , MqttClientConnector , SensorData , ActuatorData, ConfigUtil, and SenseHAT (provides hardware interface for IMU, LED matrix, and joystick).


**Verification**
Screenshots show: (1) Ubidots dashboard with 3+ variables displaying real-time data, (2) LED variable showing ON/OFF transitions, (3) GDA console logs showing "Received LED enablement message" events. All three screenshots confirm successful end-to-end cloud integration and actuation.

**Unit Tests:**

1. test_PitchSensorEmulatorTask 
2. test_LEDDisplayActuator. 

**Integration Tests:**


