**Gateway Device Application (Connected Devices)**

Lab Module 07

Description

**What the Implementation does**

My implementation adds MQTT messaging capabilities to the Gateway Device Application so it can communicate with IoT devices and cloud services. I created four main exercises: implementing MQTT callback methods (connectComplete, connectionLost, deliveryComplete, messageArrived), integrating the MQTT client into DeviceDataManager's lifecycle, running integration tests with a live broker, and merging the completed work into the main branch. The system can now connect to MQTT brokers, subscribe to IoT topics, handle incoming sensor data, and send actuator commands.

**How it works**

The MqttClientConnector class uses the Eclipse Paho MQTT library to handle all messaging operations. It implements callback methods that respond automatically when connections succeed or fail, when messages are delivered, and when new messages arrive from subscribed topics. The DeviceDataManager integrates this MQTT client into its startup and shutdown processes, connecting to the broker and subscribing to four essential topics: GDA management status, CDA actuator responses, CDA sensor messages, and CDA system performance data. During testing, I ran the GDA application in one terminal while executing integration tests in my IDE to verify that messages flow correctly through a Mosquitto broker.

Code Repository and Branch URL: 
[https://github.com/kchimbodza/gda-java/tree/labmodule07]

**UML Design Diagram(s)**

The design shows MqttClientConnector implementing IPubSubClient interface, integrated into DeviceDataManager alongside SystemPerformanceManager. DeviceDataManager acts as the central coordinator managing MQTT connectivity and implementing IDataMessageListener for message handling.

<img width="1455" height="908" alt="lab7-gda-uml" src="https://github.com/user-attachments/assets/2e197dbe-f715-45a0-8e10-7a8fd4f454c4" />

**Wireshark Output - 14 Control Packets - GDA**
<img width="2721" height="1498" alt="Screenshot From 2025-10-14 23-00-37" src="https://github.com/user-attachments/assets/bee47c50-67e5-4f25-b585-54253da88f4b" />

CONNECT - Packet #84, #141 
<img width="1713" height="519" alt="CON" src="https://github.com/user-attachments/assets/08792f5d-6016-4d77-a605-16d640110d4e" />

CONNACK - Packet #86, #143
<img width="1735" height="339" alt="conack" src="https://github.com/user-attachments/assets/b3af2d42-a7ae-48f3-9751-0d6fd4689beb" />

PUBLISH - Packets #91, #92, 
<img width="2010" height="390" alt="publish" src="https://github.com/user-attachments/assets/da64dcea-c9c3-4573-ae83-f4c8002afcde" />

PUBACK - Packets #103, #105 
<img width="2010" height="390" alt="puback" src="https://github.com/user-attachments/assets/6de9070a-34e6-4a1b-97f0-d824d356171e" />

PUBREC - Packets #115, #119 
<img width="2010" height="390" alt="pubrec" src="https://github.com/user-attachments/assets/8cdd4e58-1ced-4644-8d11-cbdcc94a3bf1" />

PUBREL - Packets #117, #122 
<img width="2010" height="390" alt="pubrel" src="https://github.com/user-attachments/assets/8a86f205-d5a2-4e7e-bf7e-eb93e2fd5127" />

PUBCOMP - Packets #120, #124 
<img width="2010" height="390" alt="pubcomp" src="https://github.com/user-attachments/assets/a157f760-5df7-4f78-a3f7-3b885ea4bbb2" />

SUBSCRIBE - Packets #88, #97, #111 
<img width="2010" height="415" alt="subscribe" src="https://github.com/user-attachments/assets/76033775-e63f-496e-bc4c-dbcfa8dc9092" />

SUBACK - Packets #89, #98, #112 
<img width="2010" height="415" alt="suback" src="https://github.com/user-attachments/assets/4e9ff963-9419-4307-a2f5-f259d0e664d6" />

UNSUBSCRIBE - Packets #94, #107, #126 
<img width="2010" height="415" alt="unsubscribe" src="https://github.com/user-attachments/assets/06d1912c-d54d-49d1-a4e9-e15d7cc89c60" />

UNSUBACK - Packets #95, #109, #128 
<img width="2010" height="415" alt="unsuback" src="https://github.com/user-attachments/assets/0c303fc1-bd06-4948-ad0c-f830c4de2734" />

PINGREQ - Packet #145 
<img width="2010" height="415" alt="pingreq" src="https://github.com/user-attachments/assets/1e5cbca8-ecaa-4df8-b3f6-ae460e990fd5" />

PINGRESP - Packet #146
<img width="2010" height="415" alt="pingres" src="https://github.com/user-attachments/assets/215f18ba-c84a-467e-ad9d-126f41190dcf" />

DISCONNECT - Packet #130, #148 
<img width="2010" height="415" alt="disconnect" src="https://github.com/user-attachments/assets/9b23528a-2bbb-471f-946a-124fd5da1e93" />

**Integration Tests Executed**

1. MqttClientConnectorTest
2. MqttClientControlPacketTest (Custom 14 Control Packets)

 
