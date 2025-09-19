**Gateway Device Application (Connected Devices)**

Lab Module 02

Description

**What the Implementation does**

My Lab Module 2 implementation adds system performance monitoring capabilities to the Java-based Gateway Device Application (GDA). The system collects CPU and memory utilization data at regular intervals using Java's ScheduledExecutorService for background task execution. This creates a robust foundation for monitoring gateway device health and performance in an IoT environment. The implementation follows object-oriented design principles with abstract base classes and concrete implementations for different types of system metrics.

**How it works**

The system works by having the main GatewayDeviceApp create a SystemPerformanceManager during application startup. This manager uses the ScheduledExecutorService to run telemetry collection tasks at configurable intervals (default 5 seconds). The manager creates instances of SystemCpuUtilTask and SystemMemUtilTask that extend the abstract BaseSystemUtilTask class. These concrete implementations use Java's ManagementFactory to retrieve actual system metrics - CPU load average and JVM heap memory utilization. The scheduler automatically calls the handleTelemetry() method which polls both tasks and logs the results. All configuration is managed through ConfigUtil and the PiotConfig.props file, making the system flexible and maintainable.

Code Repository and Branch
URL: https://github.com/kchimbodza/gda-java/tree/labmodule02

**UML Design Diagram(s)**

UML diagram showing the class relationships between GatewayDeviceApp, SystemPerformanceManager, BaseSystemUtilTask, SystemCpuUtilTask, SystemMemUtilTask, and ScheduledExecutorService

<img width="3060" height="1422" alt="lab2-uml-gda" src="https://github.com/user-attachments/assets/cc925f19-f93d-4fa0-af82-41b9e5ff5518" />

**Unit Tests Executed**

1. SystemCpuUtilTaskTest
2. SystemMemUtilTaskTest

**Integration Tests Executed**

1. GatewayDeviceAppTest
2. SystemPerformanceManagerTest
