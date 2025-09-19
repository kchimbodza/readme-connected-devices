**Constrained Device Application (Connected Devices)**

Lab Module 02

Description

**What the Implementation does**

My Lab Module 2 implementation adds system performance monitoring to the CDA. The app now collects CPU and memory usage data every 5 seconds using a background scheduler. This creates a foundation for IoT device monitoring that will be essential for tracking device health and performance over time. The implementation uses the APScheduler library to run telemetry collection tasks automatically without blocking the main application thread.

**How it works**

The system works by having the main ConstrainedDeviceApp create a SystemPerformanceManager during startup. This manager creates instances of SystemCpuUtilTask and SystemMemUtilTask that collect the actual performance data using the psutil library. The APScheduler runs a handleTelemetry() method every 5 seconds (configurable) that polls both tasks and logs the results. The scheduler starts when the app starts and shuts down cleanly when the app stops. All configuration settings are loaded from the PiotConfig.props file, making the system flexible and configurable.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule02

**UML Design Diagram(s)**

UML diagram showing SystemPerformanceManager, SystemCpuUtilTask, SystemMemUtilTask, and their relationships with ConstrainedDeviceApp and APScheduler

<img width="1939" height="957" alt="lab2-uml-cda" src="https://github.com/user-attachments/assets/7491a1e4-e39c-476a-bfd6-4a6ec7b8b0ea" />

**Unit Tests Executed**

1. test_ConfigUtilDefault
2. test_ConfigUtilCustom
3. SystemCpuUtilTaskTest
4. SystemMemUtilTaskTest

**Integration Tests Executed**

1. test_ConstrainedDeviceApp
2. SystemPerformanceManagerTest
