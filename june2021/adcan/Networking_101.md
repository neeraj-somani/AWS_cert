# Networking_101

# Various components of Networking
- Local networking - Ethernet cable
- Routing
- Segmenting, ports & sessions
- Applications
- the OSI 7-layer model


### the OSI 7-Layer Networking Model

  - layer-1-Physical
  - layer-2-Data Link
  - layer-3-Network
  - layer-4-Transport
  - layer-5-Session
  - layer-6-Presentation
  - layer-7-Application


### Few other points
- All devices that connects to network, has software that supports and understand this 7-layer model
- for example, laptop, phones, projectors, or all IOT
- layer 1, 2, and 3 also known as - Media Layer
  - media layer dealing with how data should be moved from point A to point B
- layer 4, 5, 6, and 7 also known as - Host layer
  - host layer, deals with how the data is chopped up and reassembled for transport
  - and how its formatted so that it's understandable by both sides of a network connection



### Layer-1-Physical
- the way in which the data is transmitted onto, and received from a physical shared medium 
- example could be copper (electrical cable), fibre (light) , WIFI (RF)
- this defines the transmission and reception of RAW BIT Streams between a device and a shared physical medium. 
- It defines things like voltage levels, timing, rates, distances, modulation and connectors type.
- Network interface card is an example of this
- A hub is used to connect multiple devices
- A hub is a device, whatever it receives on one port, it transmits the same to other ports, including collisions and errors.
- At this layer, no device level addressing possible, meaning all data is processed by all devices,
- its an example of broadcast medium
- layer 1 doesn't have any media controlling devices, meaning no collision detection mechanism

### Layer-1 summary
- Physical shared medium
- standards for transmitting onto the medium
- standards for receiving from the medium
- no access control
- no uniquely identified devices
- no device to device communications, everything is broadcast on the network

