**Constrained Device Application (Connected Devices)**

Lab Module 01

Description

**What the Implementation does**

My Lab Module 3 implementation creates a comprehensive IoT simulation system with automatic climate control capabilities. The CDA now generates realistic time-series sensor data for temperature, humidity, and pressure while automatically controlling HVAC systems based on configurable temperature thresholds (floor: 19°C, ceiling: 20°C). The system uses mathematical models through SensorDataGenerator to create authentic 24-hour data sets with 1440 entries each, simulating real-world sensor behavior with configurable noise levels. When temperature readings exceed boundaries, the DeviceDataManager automatically triggers HVAC actuator commands, creating a complete smart building simulation that demonstrates sensing, analysis, and actuation in a cohesive IoT system.

**How it works**

The architecture uses DeviceDataManager as the central orchestrator that manages three key subsystems through IDataMessageListener callbacks. The SensorAdapterManager employs APScheduler to collect sensor data every 5 seconds from three simulation tasks (TemperatureSensorSimTask, HumiditySensorSimTask, PressureSensorSimTask), each using either SensorDataGenerator time-series data or random value generation. Temperature readings trigger threshold analysis within DeviceDataManager - values above 20°C or below 19°C automatically generate HVAC ActuatorData commands sent to ActuatorAdapterManager. The ActuatorAdapterManager validates commands through location ID matching and routes them to appropriate simulator tasks (HvacActuatorSimTask, HumidifierActuatorSimTask) which log realistic activation/deactivation messages. Smart duplicate command filtering prevents unnecessary actuator cycling. SystemPerformanceManager continues monitoring CPU and memory utilization every 60 seconds. The entire system integrates through ConstrainedDeviceApp, providing clean startup/shutdown with proper scheduler management and exception handling.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule03

**UML Design Diagram(s)**

UML diagram showing DeviceDataManager as central orchestrator implementing IDataMessageListener, coordinating SensorAdapterManager (with TemperatureSensorSimTask, HumiditySensorSimTask, PressureSensorSimTask using SensorDataGenerator), ActuatorAdapterManager (with HvacActuatorSimTask, HumidifierActuatorSimTask), and SystemPerformanceManager. All components use APScheduler for background task execution with callback-driven data flow and automatic threshold-based climate control logic.



**Unit Tests Executed**

1. test_ActuatorData
2. test_SensorData
3. test_SystemPerformanceData
4. test_TemperatureSensorSimTask
5. test_HumiditySensorSimTask
6. test_PressureSensorSimTask
7. test_HvacActuatorSimTask
8. test_HumidifierActuatorSimTask

**Integration Tests Executed**

1. test_SensorAdapterManager (60-second comprehensive sensor data generation)
2. test_ActuatorAdapterManager (actuator command processing with ON/OFF simulation)
3. test_DeviceDataManagerNoComms (120-second full system test with automatic HVAC control)
4. test_ConstrainedDeviceApp (complete application lifecycle with clean startup/shutdown)
