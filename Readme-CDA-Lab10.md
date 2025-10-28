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


**CDA MqTT Performance Results**

QoS 0: Fastest (~5.4 msgs/ms) - no acknowledgment overhead
QoS 1: 1.3x slower - requires PUBACK from broker per message
QoS 2: 1.9x slower - requires full 4-way handshake per message
Java vs Python: GDA (Java) is faster than CDA (Python) for all QoS levels

**CDA Coap Performance Results**

POST - CON (Confirmed): 608 ms for 10,000 requests
POST - NON (Non-Confirmed): 385 ms for 10,000 requests
Both tests passed - No failures or errors

Performance Analysis:
NON is faster than CON (as expected):

NON baseline: 385 ms
CON: 608 ms
Difference: 608 - 385 = 223 ms slower
Percentage: (223 / 385) × 100 = 57.9% slower with CON

This makes sense because CON (confirmed) messages require acknowledgments from the server, adding overhead. NON (non-confirmed) messages are fire-and-forget, so they're faster.

**Now comparing CDA vs GDA results:**

The CDA was tested across MQTT QoS levels 0, 1, and 2, with QoS 0 offering the fastest performance and QoS 2 being the slowest due to its four-step handshake; Python was slower than Java but maintained stable communication. During a 5-minute test, the CDA reliably generated 60 sensor readings, triggered actuator responses when thresholds were crossed, and transmitted all data securely without loss. Integration testing confirmed successful TLS setup, with encrypted sensor, command, and response messages exchanged between CDA and GDA, as verified by Wireshark packet captures. Security was enforced through TLSv1.2, certificate validation, and encrypted MQTT traffic, with key configuration settings like enableCrypt=True and secure port 8883 ensuring protected communication.

**Unit Tests Executed**

1. CDA application tests 
2. test_MqttClientPerformance
3. test_CoapClientPerformance
4. test_DeviceDataManagerCallBack

