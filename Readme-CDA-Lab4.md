**Constrained Device Application (Connected Devices)**

Lab Module 04

Description

**What the Implementation does**

My Lab Module 4 creates a hardware-interfaced IoT emulation system using the SenseHAT emulator. It reads real environmental data from emulated temperature, humidity, and pressure sensors through the pisense library. When actuator commands are received, the system displays visual feedback on the SenseHAT LED matrix - showing "HVAC ON: 22.5C" or "HUMIDIFIER OFF" messages that scroll across the 8x8 display. The DeviceDataManager can trigger these actuations based on sensor thresholds, creating a complete sense-decide-act loop. Unlike Lab 3's pure simulation, this system interfaces with hardware APIs and provides visual feedback, demonstrating the bridge between software logic and physical device interaction.

**How it works**

The system extends Lab 3's architecture by adding an emulation layer alongside the existing simulation components. When enableEmulator = True, the SensorAdapterManager and ActuatorAdapterManager dynamically load emulator tasks using import_module(). The sensor emulators (TemperatureSensorEmulatorTask, HumiditySensorEmulatorTask, PressureSensorEmulatorTask) read live data from the SenseHAT emulator's environmental sensors through pisense.SenseHAT.environ properties. The actuator emulators (HvacEmulatorTask, HumidifierEmulatorTask, LedDisplayEmulatorTask) write to the LED matrix using self.sh.screen.scroll_text(). DeviceDataManager processes this real sensor data and sends actuator commands that appear as visual messages on the emulator GUI. The system maintains the same callback-driven architecture but now interfaces with hardware APIs instead of generating synthetic data.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule04

**UML Design Diagram(s)**

UML diagram showing DeviceDataManager implementing IDataMessageListener as central coordinator, SensorAdapterManager with TemperatureSensorEmulatorTask/HumiditySensorEmulatorTask/PressureSensorEmulatorTask, ActuatorAdapterManager with HumidifierEmulatorTask/HvacEmulatorTask/LedDisplayEmulatorTask, SystemPerformanceManager with SystemCpuUtilTask/SystemMemUtilTask, ConstrainedDeviceApp as main application controller, and BaseActuatorSimTask/BaseSensorSimTask as emulator task base classes.



**Unit Tests Executed**

1. test_TemperatureEmulatorTask
2. test_HumidityEmulatorTask
3. test_PressureEmulatorTask
4. test_HumidifierEmulatorTask
5. test_HvacEmulatorTask
6. test_LedDisplayEmulatorTask

**Integration Tests Executed**

1. test_SensorAdapterManager (emulator mode with live SenseHAT data collection)
2. test_ActuatorAdapterManager (emulator mode with LED display command processing)
3. test_SenseHatEmulatorQuick (SenseHAT emulator connectivity verification)
