**Constrained Device Application (Connected Devices)**

Lab Module 01

Description

**What the Implementation does**

My implementation creates the basic setup for a Python app that will run on IoT devices. This app is called the Constrained Device Application (CDA) and it's designed to work on small devices with limited resources. In Lab Module 1, I built the foundation by setting up the main app structure, configuration files, and basic testing. The main goal was to get everything working so I can add more IoT features in later labs.

**How it works**

The implementation works by using a main class called ConstrainedDeviceApp that starts and stops the application. It also uses a ConfigUtil class to read settings from configuration files. The app has proper logging so I can see what's happening when it runs. I can run the app for a set time (65 seconds) or make it run forever by changing a setting. I also included tests to make sure everything works correctly - both unit tests that check individual parts and integration tests that check if the whole system works together.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule01

**UML Design Diagram(s)**

This UML diagram represents your basic Lab Module 1 implementation structure showing how the main application connects to the configuration system.

**Unit Tests Executed**

1. test_ConfigUtilDefault

2. test_ConfigUtilCustom

**Integration Tests Executed**

1. test_ConstrainedDeviceApp
