**Constrained Device Application (Connected Devices)**

Lab Module 10

Description

**What the Implementation does**

The Constrained Device Application generates sensor data from temperature, humidity, and pressure sensors. Every 5 seconds, the sensor readings are published to an MQTT broker over an encrypted TLS connection. When the Gateway Device Application detects that sensor values have crossed configured thresholds, it sends actuator commands back to the CDA over the same encrypted channel. The CDA receives these commands, processes them, and controls physical actuators (like the HVAC system) in response. All communication between the CDA and broker is protected by TLS encryption, preventing unauthorized access to sensor readings or command interception.

**How it works**

When the CDA starts, it reads a config file to check if TLS encryption is enabled. If so, it loads a certificate and connects securely to port 8883 instead of the unencrypted port 1883. Sensor readings like temperature and humidity are generated every 5 seconds, and if they cross set limits, the CDA sends encrypted messages to the MQTT broker. It also listens for encrypted actuator commands from the GDA, processes them, and activates the HVAC system when needed. During testing, tools like Wireshark confirm that all data sent between CDA and GDA is encrypted and secure.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-java-components/tree/labmodule10

**UML Design Diagram(s)**

The classes that interact in the CDA UML are: ConstrainedDeviceApp interacts with DeviceDataManager, DeviceDataManager interacts with MqttClientConnector, SensorAdapterManager, and ActuatorAdapterManager, MqttClientConnector interacts with MqttClient, SSLContext, SensorData, and ActuatorData, SensorAdapterManager interacts with SensorData, and ActuatorAdapterManager interacts with ActuatorData.



**Wireshark Showing TLS protocol**
<img width="3840" height="2160" alt="Screenshot From 2025-10-27 19-17-19" src="https://github.com/user-attachments/assets/60f86492-4796-4bed-9c13-3c6fa2b32f3a" />

**CDA MqTT Performance Results**
<img width="1831" height="1657" alt="MqttClientPerformance_Tests" src="https://github.com/user-attachments/assets/738f75ee-dc56-4bba-934e-ffbb36efebb4" />


Connect and Disconnect: 2005.17 ms

Publish Performance (10,000 messages):
  QoS 0 (Fire and Forget):  1696.07 ms (baseline)
  QoS 1 (At Least Once):    3203.18 ms (+88.9% vs QoS 0)
  QoS 2 (Exactly Once):     5012.49 ms (+195.4% vs QoS 0)

**CDA Coap Performance Results**
<img width="1719" height="331" alt="Screenshot From 2025-10-27 13-52-37" src="https://github.com/user-attachments/assets/11e34a00-5910-4f5b-8993-ce4963af877b" />

POST Performance (10,000 messages):
  NON (Non-Confirmable):  14,961.70 ms (baseline)
  CON (Confirmable):      21,469.45 ms (+43.5% vs NON)

Status: 2 tests PASSED in 40.474s

**Now comparing CDA vs GDA results:**

Key Finding: MQTT is significantly faster than CoAP (up to 8.8x faster with QoS 0), but CoAP offers lighter-weight communication for constrained devices.

**Unit Tests Executed**

1. CDA application tests 
2. test_MqttClientPerformance
3. test_CoapClientPerformance
4. test_DeviceDataManagerCallBack

