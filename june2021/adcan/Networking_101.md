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
- no media access control
- no uniquely identified devices
- no device to device communications, everything is broadcast on the network


### layer-2-Data Link
- unique hardware (MAC) address
- mac address consist of 2 parts --- OUI (Organization unique identifier) and NIC (Network interface controller). In combination of these 2 things makes the MAC address on every unit a unique address.
- layer 2 provides frames and layer 1 just transmitting the frame (which consist data)
- Frame consist of various parts
  - 1 - preamble (56 bits)
  - 2 - destination MAC address (all F in case of broadcast)
  - 3 - source MAC address 
  - 4 - ET (Ether type) 16 bits - used to specify the protocol details of layer-3, which puts data frame into layer-2. example is internet protocol 
  - 5 - payload (46 bytes to 1500 bytes). its nothing but data.
  - 6 - FCS (frame check sequence) - used to identify any errors in the frame. Its a simple CRC check, allows destination to check if corruption has occured or not.
  - How layer-2 avoids collisions by (CSMA/CD)
    - Carrier-sense multiple access with collision detection (CSMA/CD) is a media access control (MAC) method used most notably in early Ethernet technology for local area networking (LAN). It uses carrier-sensing to defer transmissions until no other stations are transmitting.
    - If collisions are detected (both transmiiting at once) both backoff for a time + random. if another close collision occurs Increases random backoff time.
  - In case of Layer-2 we uses switch
    - its similar to HUB but have added advantages
    - switch has layer-2 software installed, hence it understand layer-2 functionality.
    - Switches understand frames and MAC address. They maintains MAC address table which starts off empty. As the switch receives frames on its ports, it learns which devices are connected and populates the Mac address table.
    - if MAC address is available in the MAC table, then data is sent to that specific port otherwise to all ports and create an entry of the correct destination port once the receive signal arrives.
    - Switches store and forward frames... they don't repeat blindly like HUB.
    - it means that only valid frames are forwarded - collisions are isolated on the port they occured.
    - Every X port switch has X collision domains. It allows switches to scale and be connected together.


### Summary - layer-2 - paragraph
- The data link layer builds on a functional physical layer and adds device unique IDs (MAC address) and controls access to the shared medium .. and detects and mitigates collisions. The data link layer is one of the most important layers, and creates the foundational networking layer which supports Layer 3 IP .. which is how the internet functions.
- identifiable devices (MAC address)
- Media access control (sharing)
- collision detection
- unicast.. 1:1
- Broadcast... 1:ALL
- Switches like Hubs with super powers (layer 2 software)

### What is encapsulation?
- IP packet is put inside an ethernet frame, for that part of the journey.
- when it needs to be moved into new network, that particular frame is removed and a new encapsulation frame is added around the same original packet and its moved on to the next local network.
- IP is needed, to allow you to connect to other remote networks, crossing intermediate networks on the way.

### What is Routers??
- Router is a Layer-3 device, which has layer-3 level software.
- It remove frame encapsulation and add new frame encapsulation at every hop.

### layer-3 Network 
- Why it is needed
  - layer-3 allows to connect seperate distant layer-2 networks remotely over the internet.
  - LAN1 and LAN2 are isolated local area networks. Using only layer-2, only those networks joined by direct point to point link using the same layer-2 protocol could communicate.
  - Ethernet is a layer-2 protocol used generally for local networks. long distance point to point links will use some other more suitable protocol such as PPP/MPLS/ATM, etc.
  - While, Internet protocol is a layer-3 protocol which adds cross-network IP addressing and routing to move data between local area network without direct P2P links.
  - IP packets are moved step-by-step from source to destination via intermediate networks. Encapsulated in different frames along the way.
  - Routers are used to perfom this communication.

### IP - packet structure
- two major versions at present
- IPv4
- IPv6

- There are a lot of components that make up the IP address but at this time I am focusing on only important one.

### IPv4 consist of (high imp)
- Source IP address
- Destination IP address
- Layer-4 protocol (ICMP, TCP, UDP)
- Data (payload)
- TTL (time to live) - its used to stop packet looping around forever, in-case of network issues. it defines max number of hops a packet can takes, before being discarded.

### some other points about IPv4
- All IP addresses have 'network' part and a 'host' part.
- If network part of the two IP addresses matches, then they are on same IP network.
- IP address are actually binary, 4 sets of 8 bits (octets) for a total of 32 bits.
- IP addresses are assigned by machine (DHCP-Dynamic Host control protocol) or humans.

### Subnet mask 
- This allows us to understand the IP is local or remote
- which influences if it needs to use gateway or can communicate locally.
- for example, in home network, usually router is set as default gateway
- A subnet mask represents which part of the IP address is network(1) and which part is HOST(0).
- example, 255.255.0.0/16
- A subnet mask is configured on a host device in addition to IP address
- Using subnet mark, anyone can understand the start and end of the IP address range.

### Route Tables & Routes
- Every router has route tables and thats how it detects where to send data.
- every route table consist of 2 parts, destination field and next hop/target field
- router compares packet destination IP & route table for matching destinations. The more specific prefixes are preferred (0 lowest, 32 highest). Packet is forwarded on to the Next Hop/target.
- route tables can be statically populated or there are protocols such as BGP (Border Gateway Protocol), which allows routers to communicate with each other, to exchange which networks they know about.
- But how will you determine destination IP address.
-  Thats where we use, Address resolution protocol.

### Address resolution protocol (ARP)
- you don't initially know the MAC address (for a given IP address) of the destination device 
- Its a process that runs between layer2 and layer3

### IPv6 consist of (high imp)
- Source IP address
- Destination IP address
- Data (payload)
- Hop limit (time to live) - its used to stop packet looping around forever, in-case of network issues. it defines max number of hops a packet can takes, before being discarded.


### Summary - layer-3 Network
- The network layer adds the ability for cross-network addressing (IP Addresses). It allows packets to be routed across different layer 2 networks, via L2 Frame encapsulation and forwarding decisions using routes and route tables. Its Layer 3 which allows the internet to function.

- IP addresses (IPv4/v6) - cross network addressing
- ARP - find the MAC address, for this IP
- Route - where to forward this packet
- Route tables - mulktiple routes
- Router - moves packets from SRC to DST - Encapsulating in L2 on the way
- No method for channels of communications .. we have SRC IP to DST IP only, meaning multiple applications can't communicate at the same time on the same device. (hence need layer 4). How will you identify which packet (data) is requested by which application.
- packets Can be delivered out of order (hence need layer 4)


### layer4&5 - Transport and Session Layer
- The transport layer adds Ports, error correction, retransmission, flow control and a connection orientated architecture.
- Why its needed?? What problems it solves??
  - L3 provides no ordering of the packets, send from SRC to Dest.
  - L3 doesn't guaranteed to be reliable. Packets can be lost en-route.
  - L3 per packet routing can introduce delays to packets en-route. Different packets can experience different delays.
  - With L3, there are no communication channels - packets have a source and destination OP only but no method of splitting by APP or Channel.
  - No flow control. If the source trasnmit faster than the destination can receive, it can saturate the destination causing packet loss.
- How does Layer 4 and 5 resolves above problems?
  - it adds two new protols
  - at layer 4 it adds 2 new protocols TCP and UDP
  - These both run on top of IP and used in the same way.
  - TCP (transmission control protocol)
    - its a slower / reliable connection
    - error correction
    - ordering of data
    - its a connection oriented protocol, meaning SRC and DEST builds a connection build a bi-directional communication channel
  - UDP (user datagrame protocol)
    - faster / less reliable
    - it doesn't have the overhead of TCP, meaning all the connection check requirement is not followed.
    - two devices can instantly start communicating on this for faster communication.

### TCP in more details
- **TCP Segments**
  - its another container for data
  - TCP segments are encapsulated within IP packets
  - Segments don't have SRC or DST IP's - the packet provide device addressing
  - imp parts of TCP segments
    - Source port
    - Destination port
    - sequence number
    - Acknowledgment
    - FLAGS and THINGS
    - Window
  - because of this structure of TCP segments, it allows devices to create a channel of communication
  - because of these different ports, there can be multiple channel of communication can be created
  - sequence number is incremented, its unique and can be used for error correction or retransmission.
  - Sequence number also help in ordering of packets once it arrives at destination.
  - Acknowledgment part allows devices to indicate that the packet has been received and up to what sequence number
  - FLAGS and THINGS - this allows various other controls. Flags are used to close connections, sychronize sequence number, many more.
  - Window - is the part where two parties agrees to receive specific number of bytes in between the acknowledgement.
  - checksum - used for error checking
  - urgent pointer - this allows SRC and DEST, to have seperate processing power. This allows flow control in communication. FTP and telnet are the example.
    
- **FLAGs and THINGS**
  - flags can have few very specific values that can be used in communication.
  - 'FIN' - value in flag can be used to close the connection
  - 'ACK' - used for acknowledgment
  - 'SYN' - used to synchronise sequence number
  - 'PSH' - 
  - 'RST' - 
  - 'URG' - 

- Based on these flags, TCP creates a 3-way handshake connection
- SYN --> SYN-ACK --> ACK

### Layer 5 - sessions and State
- for security we add firewall rules
- a stateless firewall would see two things (In AWS this is what NACL does)
  - outbound connection
  - response to the original outbound connection (inbound)
- A stateful firewall would sees one thing (In AWS this is what Security Group does)
  - allwoing the outbound, implicitly allows the inbound response.

### TCP well known ports
- 80 - HTTP
- 443 - HTTPs (encrypted by default)
- 22 - ssh (encrypted by default)
- 25 - SMTP (email)
- 21 - Telnet
- 3389 - remote desktop protocol (encrypted by default)
- 3306 - Mysql/MariaDB/Aurora

### Network Address Traslation (NAT) 
- Network Address Translation (NAT) is the process of adjusting packets source and destination addresses to allow transit across different networks. 
- The main types you will encounter are Static NAT, Dynamic NAT and Port Address Translation (PAT). 
- NAT is most commonly experience in home or office networks where private IPv4 addresses are translated to a single public address, allowing outgoing internet access.
- NAT is designed to overcome IPv4 shortages
- also provides some security benefits
- translates private IPv4 address to public
- Static NAT - 1 private to 1 fixed public address (IGW) - bi-directional
- Dynamic NAT - 1 private to 1st available public IP from a pool of IP addresses. Mostly used where you have more private IP address and less public IP's.
- Port Address Translation (PAT) - many private to 1 public (NAT-GW). Used most commonly in Home internet router. laptop, phone, other devices connect to same public IP. Also known as overloading. It uses port to identify individual devices. NAT Gateway and NAT instances use this within AWS.
- This is required only for IPv4.
- Since, we have huge number of IPv6 addresses, we don't need any form of private addressing and hence no translation required.
- public and private IP addresses can't communicate directly over the public internet.
- The router (NAT Device) maintains a NAT table, it maps PrivateIP : Public IP (1:1)
- The router (PAT device / NAT-GW) - it maps PrivateIP : Public IP (many:1)

### PAT (Port Address Translation)
- it maps PrivateIP : Public IP (many:1)
- The way it keeps track of devices is using private IP of device and port of device.
  - The NAT device records the source (Private) IP and Source port. 
  - It replaces the source IP with the single Public IP and a public source port allocated from a pool which allows IP overloading (many to one). meaning, NAT device translate both source IP and source port. port is allocated at random by the NAT devices, hence this combination will always be unique. And NAT table will keep track of it.
  - **very imp** - why we can't initiate traffic to these private devices??
    - because there is no entry into the NAT table (router table) for public IP to Private IP, untill a communication starts from private IP.
    - thats how NAT Gateway secures the environment.
