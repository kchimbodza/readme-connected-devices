**Constrained Device Application (Connected Devices)**

Lab Module 09

Description

**What the Implementation does**


The addition of a CoAP client to the CDA in my Lab Module 09 solution allows it to communicate with remote IoT servers over the network. The client supports all standard CoAP operations: GET requests to retrieve data, POST requests to create new resources, PUT requests to update existing data, and DELETE requests to remove resources. It can discover available resources on remote servers and observe resources for automatic updates when they change. The client works alongside existing MQTT and local sensor functions, and all data exchanges use JSON format.

**How it works**

CoapClientConnector creates an aiocoap client that connects to the GDA CoAP server on port 5683. It sends requests using both CON (confirmable, requiring acknowledgment) and NON (non-confirmable, faster) message types. For observations, the client registers interest in a resource and receives automatic notifications when the resource updates. All incoming responses are processed through callback methods that convert JSON data back into Python objects using DataUtil. The client runs asynchronously using asyncio, allowing it to handle responses without blocking other CDA operations. DeviceDataManager uses the client to communicate sensor data to the GDA and receive actuator commands back.

Code Repository and Branch
URL: https://github.com/kchimbodza/cda-python/tree/labmodule09

**UML Design Diagram(s)**

UML diagram showing CoapClientConnector with methods for discovery, GET, POST, PUT, DELETE, and observe operations, integrated with DeviceDataManager. Includes async request handlers, response callbacks (_onGetResponse, _onPostResponse, _onPutResponse, _onDeleteResponse), ResourceNameEnum for resource paths, DataUtil for JSON conversion, and asyncio event loop for non-blocking operations.

**Wireshark Output**
<img width="3097" height="1068" alt="Screenshot From 2025-10-16 00-25-20" src="https://github.com/user-attachments/assets/7439fcbe-7522-462e-b500-f6d1119d4c13" />

Discovery
<img width="1731" height="522" alt="Discovery" src="https://github.com/user-attachments/assets/bd34b45f-380a-4419-917a-27694b712df0" />
 
GET (CON & NON)
<img width="1731" height="571" alt="getcon" src="https://github.com/user-attachments/assets/bf9f9cc2-1dd2-4b0e-add2-ca340fae2ec5" />

<img width="1731" height="571" alt="getnon" src="https://github.com/user-attachments/assets/552ae061-85ba-4bb1-bf05-2bb8d5d624f8" />


POST (CON & NON)
<img width="1731" height="624" alt="postcon" src="https://github.com/user-attachments/assets/760a45af-d692-4b70-ac04-575dfd4cab9a" />

<img width="1731" height="624" alt="postnon" src="https://github.com/user-attachments/assets/4221a50f-9b5d-4296-a24e-44c65f919a67" />


PUT (CON & NON)
<img width="1731" height="624" alt="putcon" src="https://github.com/user-attachments/assets/05537722-6d01-4e69-86ad-f1311436f6e7" />
<img width="1731" height="624" alt="putnon" src="https://github.com/user-attachments/assets/dc911e67-5558-4409-8e92-96e9be3674d4" />


DELETE (CON & NON)
<img width="1731" height="624" alt="image" src="https://github.com/user-attachments/assets/7ce75588-bbcb-4d15-a3fc-bd9ab65da50a" />
<img width="1731" height="624" alt="delnon" src="https://github.com/user-attachments/assets/c505ab7e-b519-4a17-a1fd-cae559b0e399" />

OBSERVE
<img width="1731" height="624" alt="observe" src="https://github.com/user-attachments/assets/c6692be0-d1b6-4d42-a911-38470c903681" />


**Integration Tests Executed**

1.test_CoapClientConnector
