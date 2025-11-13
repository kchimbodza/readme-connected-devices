**Gateway Device Application (Connected Devices)**

Lab Module 12

Description

**What the Implementation does**
The GDA was extended to receive LED position data from the CDA via MQTT and forward it to the Ubidots cloud platform. New resource definitions and message handlers enable the GDA to subscribe to LED position topics, process incoming coordinates and control mode, create separate SensorData objects for horizontal and vertical position, and publish this data to the cloud service.

**How it works**

The GDA subscribes to MQTT topic piot/cda/actuator/ledposition, receives LED position JSON messages from the CDA, parses the x and y coordinates into separate SensorData objects (LedHorizontalPosition and LedVerticalPosition), and publishes them to Ubidots via HTTP REST API. ResourceNameEnum was updated with the LED position resource identifier, DeviceDataManager handles parsing incoming messages, and CloudClientConnector manages cloud publishing using proper variable naming.

Code Repository and Branch
URL: https://github.com/kchimbodza/gda-java/tree/labmodule12

**UML Design Diagram(s)**

The primary classes involved in Lab 12 GDA are: GatewayDeviceApp (main application controller), DeviceDataManager (orchestrates MQTT message reception and cloud publishing), MqttClientConnector (receives LED position data from CDA), CloudClientConnector (publishes position data to Ubidots), ResourceNameEnum (defines MQTT topic identifiers), SensorData (encapsulates position telemetry), and ActuatorData (encapsulates incoming LED position commands).

**GDA Unit Tests:**

1. DeviceDataManagerTest
2. CloudClientConnectorTest 

**GDA Integration Tests:**

1. GatewayDeviceApp.java


