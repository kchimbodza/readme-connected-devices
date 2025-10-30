**Constrained Device Application (Connected Devices)**

Lab Module 11

Description

**What the Implementation does**

The GDA collects environmental sensor data (temperature, humidity, pressure) from the CDA on three separate MQTT topics and transmits it to Ubidots cloud service. It subscribes to Ubidots LED actuation events that trigger based on sensor threshold rules. When cloud commands arrive, the GDA processes them and forwards them back to the CDA for device actuation.

**How it works**

The CloudClientConnector manages secure TLS communication with Ubidots and provisions the LED topic on successful connection. The DeviceDataManager subscribes to three sensor-specific topics locally and routes sensor messages to the cloud via sendEdgeDataToCloud(). When Ubidots publishes an LED command, the LedEnablementMessageListener converts it to ActuatorData and forwards it to the CDA via local MQTT.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule11

**UML Design Diagram(s)**

The primary classes involved in Lab Module 11 implementation are CloudClientConnector, MqttClientConnector, LedEnablementMessageListener, and DeviceDataManager. Supporting interfaces include ICloudClient, IConnectionListener, and IDataMessageListener. Data model classes are SensorData, ActuatorData, and SystemPerformanceData. Utility classes are DataUtil and ResourceNameEnum.


**Verification**
Screenshots show: (1) Ubidots dashboard with 3+ variables displaying real-time data,  
integration and actuation.
<img width="1488" height="1239" alt="Screenshot From 2025-10-29 17-13-28" src="https://github.com/user-attachments/assets/f56010b0-77c3-40af-98bb-1b783b84b91b" />

(2) LED variable showing ON/OFF transitions,
<img width="2671" height="1386" alt="Screenshot From 2025-10-30 02-08-53" src="https://github.com/user-attachments/assets/2f759a02-50dd-4be2-8898-5da684f6981c" />

(3) GDA console logs showing "Received LED enablement message" events. All three screenshots confirm successful end-to-end cloud 
<img width="1432" height="1386" alt="Screenshot From 2025-10-30 03-18-35" src="https://github.com/user-attachments/assets/ba03ae9c-bd00-4afc-be35-95854207fea0" />


**Unit Tests:**

TimeAndValuePayloadDataTest.java
DataUtilTest.java

**Integration Tests:**

CloudClientConnectorTest.java

