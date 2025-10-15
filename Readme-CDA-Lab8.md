**Constrained Device Application (Connected Devices)**

Lab Module 08

Description

**What the Implementation does**

The addition of a CoAP server to the CDA in my Lab Module 08 solution allows it to connect to other IoT devices via the network.  The server has three resources: one for accepting actuator instructions from distant devices, and two for distributing sensor and system performance data, to which other devices can subscribe for automated updates.  Clients may automatically discover what data is accessible thanks to the server's resource discovery feature.  The server operates in the background without affecting current MQTT and sensor functions, and all communications are in JSON format.

**How it works**

CoapServerAdapter operates an aiocoap server on port 5683 with three handlers: UpdateActuatorResourceHandler receives actuator commands via PUT/POST requests and sends them to DeviceDataManager, while GetSystemPerformanceResourceHandler and GetTelemetryResourceHandler share sensor and performance data with subscribers.  The server enables discovery via.well-known/core, arranges resources in a tree structure and operates in a background thread.  Subscribed clients receive updates from the handlers when DeviceDataManager automatically provides them with fresh data.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule08

**UML Design Diagram(s)**

UML diagram showing CoapServerAdapter managing three handlers (GetSystemPerformanceResourceHandler, GetTelemetryResourceHandler, UpdateActuatorResourceHandler), integrated with DeviceDataManager for data flow between sensors, actuators, and CoAP clients. Includes resource tree structure, JSON conversion via DataUtil, and asyncio threading model.

<img width="2208" height="1377" alt="lab8-CDA-UML" src="https://github.com/user-attachments/assets/55d98c8e-81d8-4715-b994-9c32772e0f97" />

**Log Output for CoAP Discover, CoAP GET and ResourceNameEnum resources registration**
<img width="2904" height="1431" alt="Screenshot From 2025-10-14 23-47-48" src="https://github.com/user-attachments/assets/2cfff6b7-7510-49a0-bee6-c8ed7025c63f" />


**Integration Tests Executed**

1. ConstrainedDeviceApp - CoAP requests and Data retrieval
