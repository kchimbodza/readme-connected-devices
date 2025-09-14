**Gateway Device Application (Connected Devices)**

Lab Module 01

Description

**What the Implementation does**

My implementation creates the basic setup for a Java app that will run as a Gateway Device Application (GDA) in an IoT system. The GDA is designed to act as a bridge between constrained IoT devices and cloud services, handling data processing and communication. In Lab Module 1, I built the foundation by setting up the main app structure, configuration management system, and basic testing framework. The main goal was to establish a solid base that can support more complex gateway features like device communication and data processing in later labs.

**How it works**

The implementation works by using a main class called GatewayDeviceApp that controls the application lifecycle - starting and stopping the gateway services. It uses a ConfigUtil class to read settings from properties files, making the system configurable without changing code. The app includes proper logging using Java's logging framework so I can track what happens when it runs. The system is designed to run continuously as a service, managing connections and data flow between edge devices and cloud services. I included comprehensive tests to verify everything works correctly - both unit tests for individual components and integration tests for the complete system.

Code Repository and Branch
https://github.com/kchimbodza/gda-java/tree/labmodule01

**UML Design Diagram(s)**

This represents the basic Java Gateway Device Application structure from Lab Module 1, showing the foundation architecture for configuration management and application lifecycle control.
The diagram shows how the GDA initializes, loads configuration, and provides the framework that will be extended in Lab Module 2 with system performance monitoring capabilities.

**Unit Tests Executed**

1. ConfigUtilTest

**Integration Tests Executed**

1. GatewayDeviceAppTest
