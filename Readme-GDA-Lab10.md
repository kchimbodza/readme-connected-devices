**Gateway Device Application (Connected Devices)**

Lab Module 10

Description

**What the Implementation does**

The Gateway Device Application (GDA) receives encrypted sensor data from multiple CDAs through an MQTT broker. It checks the data in real time to see if any values go beyond set limits—for example, turning the humidifier on if humidity drops below 35%, or off if it goes above 45%. All sensor messages and actuator commands are protected with TLS encryption to keep them secure. The GDA also tracks system performance like CPU, memory, and disk usage, and sends this data securely for remote monitoring. changes.

**How it works**

When the GDA starts, it reads the config file to check if TLS encryption is enabled and loads the CA certificate to connect securely to port 8883. During initialization, the GDA sets up a secure SSL context using Java libraries and validates the broker’s certificate to ensure a trusted connection. It subscribes to encrypted MQTT topics to receive sensor data, system performance metrics, actuator responses, and management status, then parses and forwards this data for analysis. The GDA checks for threshold crossings using time-windowed logic and sends encrypted actuator commands when needed, while also securely publishing its own system health metrics for remote monitoring.

Code Repository and Branch
URL: https://github.com/kchimbodza/gda-java/tree/labmodule10

**UML Design Diagram(s)**

The GDA Lab Module 10 UML diagram contains ten classes: GatewayDeviceApp, DeviceDataManager, MqttClientConnector, ThresholdAnalyzer, SSLContext, SensorData, ActuatorData, test_MqttClientPerformance, test_CoapClientPerformance, and test_DeviceDataManagerSimpleCDAActuation.


**GDA MqTT Performance Results**

Connect and Disconnect: 2307 ms

Publish Performance (10,000 messages):
  QoS 0 (Fire and Forget):  1865 ms (baseline)
  QoS 1 (At Least Once):    2461 ms (+32.0%)
  QoS 2 (Exactly Once):     3601 ms (+93.1%)

Status: 4 tests PASSED in 19.959s

**GDA CoAP Performance Test Results **

POST Performance (10,000 messages):
  NON (Non-Confirmable):  385 ms (baseline)
  CON (Confirmable):      608 ms (+57.9%)

Status: 2 tests PASSED in completion

**Now comparing CDA vs GDA results:**

The GDA (Java) is significantly faster than the CDA (Python) for CoAP communication, which is typical since Java has better networking performance and Californium is optimized for CoAP.

**Unit Tests Executed**

1. MqttClientConnector test
2. MqttClientPerformanceTest
3. CoapClientPerformanceTest
4. DeviceDataManagerSimpleCDAActuationTest

**Integration Test**

1. GDA application


