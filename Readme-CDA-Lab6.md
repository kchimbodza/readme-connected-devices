**Constrained Device Application (Connected Devices)**

Lab Module 06

Description

**What the Implementation does**

My implementation adds MQTT messaging to the IoT device app. The device can now connect to an MQTT broker, send sensor data, and receive commands. I built an MQTT client that handles all the network communication and connected it to the main device manager. The system can publish messages with different quality levels and subscribe to topics to get updates.

**How it works**

The MqttClientConnector class handles connecting to the MQTT broker and sending/receiving messages. The DeviceDataManager starts the MQTT client when the app runs and subscribes to actuator command topics. When sensor data is collected, it gets converted to JSON and can be published via MQTT. The system uses configuration files to know which broker to connect to and what topics to use. All the MQTT callback functions log what happens so I can see the communication working.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule06

**UML Design Diagram(s)**

[UML diagram showing ConstrainedDeviceApp, DeviceDataManager, MqttClientConnector, and data classes with their relationships]
<img width="2219" height="1017" alt="lab6-uml-cda" src="https://github.com/user-attachments/assets/768191fc-a8e8-4ef9-b2fa-2f4eb99b3ff8" />

**Wireshark Output:**

Wireshark output for the MQTT specific protocol content for all FOURTEEN (14) MQTT 3.1.1 Control Packet types
<img width="2759" height="1735" alt="Screenshot From 2025-09-27 13-07-36" src="https://github.com/user-attachments/assets/5420ac37-5cf2-481f-85eb-e7ab065877aa" />

CONNECT
<img width="2104" height="501" alt="CONNECT" src="https://github.com/user-attachments/assets/587278f0-9177-4703-99b2-744f04e62cb2" />

CONNACK - Packet #31
<img width="2104" height="501" alt="CONNACK" src="https://github.com/user-attachments/assets/1506edf1-d148-4df1-8aac-70eaca8b2e2e" />

PUBLISH (QoS 0) - Packet #54 or #55
<img width="2104" height="355" alt="PUB-QoS-0" src="https://github.com/user-attachments/assets/8922cc23-8ff2-4b35-a8d9-0d3e22c3729c" />

PUBLISH (QoS 1) - Packet #69 or #70
<img width="2113" height="501" alt="PUBLISH-QoS-1" src="https://github.com/user-attachments/assets/ca341d9b-07b5-423e-ba4c-159b2b67470b" />

PUBLISH (QoS 2) - Packet #91 or #97
<img width="2113" height="501" alt="PUBLISH-QoS-2" src="https://github.com/user-attachments/assets/b7862bd5-2118-4922-a1ed-eec06cefd476" />

PUBACK - Packet #72 or #76
<img width="2113" height="300" alt="PUBACK" src="https://github.com/user-attachments/assets/6ca59d0d-dafe-43cf-b461-56c1bddf0e65" />

PUBREC - Packet #92 or #100
<img width="2113" height="300" alt="PUBREC" src="https://github.com/user-attachments/assets/f03a5207-6417-4fd3-bdb5-dca1efb09cd7" />

PUBREL - Packet #96 or #103
<img width="2113" height="300" alt="PUBREL" src="https://github.com/user-attachments/assets/498f5bad-41dc-4322-99ac-9e8b43813bb5" />

PUBCOMP - Packet #101 or #107
<img width="2113" height="300" alt="PUBCOMP" src="https://github.com/user-attachments/assets/d4bf6e5b-22e8-4171-990b-7187c7efcdbe" />

SUBSCRIBE - Packet #49, #64, or #86
<img width="2113" height="400" alt="SUBSCRIBE" src="https://github.com/user-attachments/assets/15b4515f-796b-4fdf-bf35-98b586f57570" />

SUBACK - Packet #50, #65, or #87
<img width="2113" height="400" alt="SUBACK" src="https://github.com/user-attachments/assets/33508f49-abc8-481f-9860-e01a04b28c07" />

UNSUBSCRIBE - Packet #59, #80, or #111
<img width="2113" height="400" alt="UNSUBSCRIBE" src="https://github.com/user-attachments/assets/16e65658-12a1-462b-8cb8-7fa8343b36a9" />

UNSUBACK - Packet #60, #82, or #113
<img width="2113" height="400" alt="UNSUBACK" src="https://github.com/user-attachments/assets/a3693931-59b0-4629-ab50-945d38f3f63b" />

PINGREQ - Packet #117
<img width="2113" height="265" alt="PINGREQ" src="https://github.com/user-attachments/assets/5d9e38c4-ded3-4644-a3db-ffb985c7a5d4" />

PINGRESP - Packet #118
<img width="2113" height="265" alt="PINGRESP" src="https://github.com/user-attachments/assets/d15ce4ad-a9f8-4303-9340-b1a2bc7eec34" />

DISCONNECT - Packet #123
<img width="2113" height="265" alt="DISCONNECT" src="https://github.com/user-attachments/assets/677ed99a-a110-4cdf-855e-4ffaffd7e79f" />


**Unit Tests Executed**

1. test_MqttClientConnector.py

**Integration Tests Executed**

1. test_MqttClientConnector.py
2. test_MqttClientControlPacket.py
