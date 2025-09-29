**Gateway Device Application (Connected Devices)**

Lab Module 05

Description

**What the Implementation does**

My Lab Module 5 builds a data manager for IoT gateway devices. The DeviceDataManager collects information from sensors, actuators, and system performance. It watches the computer's CPU, memory, and disk usage every 60 seconds and shows real numbers. The system can convert data to JSON format for sending to other devices. Everything connects through callback methods that pass data between components.

**How it works**

DeviceDataManager is the main controller that handles all data. It starts SystemPerformanceManager which runs a timer to check CPU, memory, and disk usage. When new performance data is ready, SystemPerformanceManager sends it to DeviceDataManager through callback methods. GatewayDeviceApp creates the DeviceDataManager and starts/stops it. DataUtil converts Java objects to JSON text and back. The system reads settings from a config file to turn features on or off.

Code Repository and Branch
URL: https://github.com/kchimbodza/gda-java/tree/labmodule05

**UML Design Diagram(s)**

UML diagram showing GatewayDeviceApp creates DeviceDataManager, DeviceDataManager manages SystemPerformanceManager, and SystemPerformanceManager collects CPU/memory/disk data from system tasks.

<img width="2944" height="1315" alt="lab5-gda-uml" src="https://github.com/user-attachments/assets/d6b9609f-ba9c-4b8c-9598-95359e5c5381" />


**Unit Tests Executed**

1. ActuatorDataTest
2. SensorDataTest
3. SystemPerformanceDataTest
4. DataUtilTest

**Integration Tests Executed**

1. SystemPerformanceManagerTest
2. DataIntegrationTest
3. test_DeviceDataManagerNoCommsTest
4. test_GatewayDeviceAppTest
