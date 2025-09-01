# Basics

## Table of contents
1. [Protocols](#question1)
2. [Proxy server](#question2)
3. [Subnet mask](#question3)
4. [IP Address](#question4)
5. [OSI and TCP/IP models](#question5)
6. [Network topology](#question6)
7. [Difference between a LAN, WAN, and MAN](#question7)
8. [Some](#question8)
9. [Some](#question9)
10. [Some](#question10)

## 1. Protocols <a name="question1"></a>

Network protocols define the rules for data communication between systems. TCP provides reliable, connection-oriented data transfer; UDP offers faster, connectionless data transfer, often for streaming. HTTP is for transferring web content, SMTP for email, and FTP for file transfers between computers. 

Transport Layer Protocols
1. TCP (Transmission Control Protocol):
    A connection-oriented protocol that guarantees reliable, ordered, and error-checked delivery of data packets by establishing a connection between hosts before data is exchanged. 
2. UDP (User Datagram Protocol):
    A connectionless protocol that transmits data packets without requiring a connection or guaranteeing their delivery, prioritizing speed over reliability, often used in streaming and gaming applications. 

Application Layer Protocols
1. HTTP (Hypertext Transfer Protocol):
    The foundation of data communication on the World Wide Web, used to transmit web pages and other content, such as HTML, between a client (like a web browser) and a server. 
2. FTP (File Transfer Protocol):
    A standard network protocol for transferring files between a client and a server, enabling the sharing of large volumes of data efficiently. 
3. SMTP (Simple Mail Transfer Protocol):
    The protocol used for sending and receiving emails, handling the forwarding of email messages between networks and mail servers

## 2. Proxy server <a name="question2"></a>

A proxy server is an intermediary system between your device and the internet that intercepts and forwards requests on your behalf, acting as a gateway. It uses its own IP address, allowing users to mask their real location, enhance security by filtering traffic, and improve performance by caching popular web pages. Proxies are used for personal tasks like browsing anonymously, as well as for businesses to manage internet activity, control access, and secure their internal networks.
 
How it Works
1. Request:
    When you request a web page or file, your device sends the request to the proxy server instead of directly to the website's server. 
2. Forwarding:
    The proxy server receives your request, fetches the resource from the destination server, and then sends it back to you. 
3. IP Masking:
    Since the request comes from the proxy's IP address, websites and other servers see the proxy's IP, not your own. 
4. Caching:
    Proxy servers can store copies of frequently accessed websites (cache) to deliver them faster to other users on the same network, which also saves bandwidth. 

Common Uses
- Anonymity:
    Hide your IP address and geographic location to browse the internet more privately. 
- Security:
    Prevent unauthorized access to your network and filter malicious content. 
- Content Control:
    Block or filter access to certain websites or content, often used in corporate or school environments. 
- Performance:
    Speed up web access by caching data and managing network traffic efficiently. 
- Access Geo-Restricted Content:
    "Spoof" your location to access content that may be restricted in your actual region. 

## 3. Subnet mask <a name="question3"></a>

A subnet mask is a 32-bit number that divides an IP address into its network portion and host portion, enabling network segmentation (subnetting) and more efficient network management. It works by applying a binary "bitmask" to the IP address, where '1' bits in the mask correspond to the network portion and '0' bits to the host portion, determining the size and usable address range of a network or subnet. This allows for breaking large networks into smaller, more manageable subnets, which helps reduce network congestion, improve security by isolating segments, and allow for more flexible IP address allocation.
 
How a Subnet Mask Works
1. Splitting the IP Address:
    Each IPv4 address (a 32-bit number) is paired with a 32-bit subnet mask, structured like an IP address but in dotted-decimal notation. 
2. Binary Representation:
    The subnet mask is made of binary ones and zeros. 
    - Ones (1s): Indicate the part of the IP address that belongs to the network. 
    - Zeros (0s): Indicate the part of the IP address that identifies the specific device (host) within that network or subnet. 
3. Network Segmentation:
    By applying a subnet mask, an entire large network can be divided into smaller, logical "subnets". 
4. CIDR Notation:
    Subnet masks are also represented in Classless Inter-Domain Routing (CIDR) notation, such as /24, which signifies 24 bits in the network portion. 

Purpose and Benefits
- Efficient IP Allocation:
    Subnetting helps to allocate IP addresses more efficiently, preventing wastage and allowing for larger networks. 
- Reduced Network Congestion:
    By segmenting a network into smaller subnets, broadcasts are contained within their respective subnets, reducing overall network traffic and improving performance. 
- Enhanced Security:
    Subnets allow for the isolation of different network segments, such as a development network from a production network, which enhances security and control. 
- Organizational Benefits:
    It allows for the logical grouping of devices, such as separating different departments within a company, making it easier to manage and apply network policies. 

## 4. IP Address <a name="question4"></a>

An IP address (Internet Protocol address) is a unique numeric identifier assigned to devices on a network, serving as a digital address that allows for data to be sent and received between devices. Like a postal address for data, it provides the necessary information for devices to locate and communicate with each other across the internet or within a local network. 

- Identification:
    An IP address serves two main functions: it identifies a network interface (like your phone or computer) and serves as a location address for data transmission. 
- Data Routing:
    When you visit a website, your computer doesn't understand the website's name directly. Instead, it uses the website's IP address to find and load the content. 
- Network Communication:
    Without IP addresses, devices on a network wouldn't be able to differentiate themselves, making it impossible to send information to the correct destination. 

Key characteristics:
- Uniqueness: 
    Every device connected to the internet or a local network is assigned a unique IP address. 
- Format:
    - IPv4: A 32-bit number typically written as four sets of digits (0-225) separated by periods, such as 192.0.2.1. 
    - IPv6: A longer, hexadecimal address format, such as 1301:7db8:86a3:3010::8a4e:0474:7104. 
- Assignment: 
    IP addresses are assigned by Internet Service Providers (ISPs). 

Why it matters:
- Connectivity:
    Your IP address is essential for accessing the internet and all online services. 
- Location:
    An IP address can reveal your general location and the Internet Service Provider you are using. 
- Security:
    While necessary for communication, your IP address can also be a privacy and security concern, as it can be used by third parties to track your online activities. 

## 5. OSI and TCP/IP models <a name="question5"></a>

The OSI and TCP/IP models are both conceptual frameworks for computer networking, but the OSI model is a theoretical, seven-layer standard for network communication, while the TCP/IP model is a four-layer, practical model that forms the basis of the internet and real-world networks. The OSI model is used for learning and understanding, whereas the TCP/IP model is used for practical implementation and troubleshooting. 

1. OSI Model (Open Systems Interconnection) 
    - Purpose:
        To provide a universal language and comprehensive framework for all types of network communication. 
    - Structure:
        A seven-layer model, with each layer performing distinct, strictly separated functions. 
    - Layers: 
        - Physical Layer 
        - Data Link Layer 
        - Network Layer 
        - Transport Layer 
        - Session Layer 
        - Presentation Layer 
        - Application Layer 
    - Use:
        Primarily a theoretical tool for learning, teaching, and analyzing network communication in detail. 

2. TCP/IP Model (Transmission Control Protocol/Internet Protocol) 
    - Purpose:
        To define how devices should transmit data over a network, enabling large-scale communication. 
    - Structure:
        A four-layer model that is more pragmatic and combines functions to focus on real-world implementations. 
    - Layers: 
        - Network Access Layer (also called Link Layer) 
        - Internet Layer 
        - Transport Layer 
        - Application Layer 
    - Use:
        The foundation of the internet, used for practical networking and to achieve specific communication goals. 

Key Differences
1. Theoretical vs. Practical:
    OSI is a comprehensive, protocol-independent theoretical framework, while TCP/IP is a functional, protocol-based model for practical implementation. 
2. Layers:
    OSI has seven layers, whereas TCP/IP has four. 
3. Standards:
    OSI was developed by the International Organization for Standardization (ISO) as a standard, while TCP/IP was developed by the U.S. Department of Defense to support the internet. 
4. Implementation:
    The TCP/IP model is the direct basis for how the internet operates, making it the de facto standard for real-world networking. 

## 6. Network topology <a name="question6"></a>

Network topology is the physical or logical layout and interconnection of network devices and how data flows through them. It defines the arrangement of nodes (devices like computers, routers, and switches) and links (connections like cables or wireless signals) that make up a network. Key types include star, bus, ring, mesh, tree, and hybrid topologies, each with unique benefits and drawbacks concerning performance, reliability, scalability, and cost. 
  
Physical vs. Logical Topology
- Physical Topology:
    Describes the actual, tangible placement of network components and how they are physically cabled together. 
- Logical Topology:
    Illustrates how data moves and communicates between devices, regardless of their physical arrangement. 

**Common Types of Network Topologies**
1. Star Topology:
    All devices connect to a central hub or switch.  
    - Pros: Easy to manage, failure in one device doesn't affect others.  
    - Cons: If the central hub fails, the entire network goes down.  
2. Bus Topology:
    All devices connect to a single central cable, or bus.  
    - Pros: Cost-effective and simple to implement.  
    - Cons: A single break in the cable can shut down the entire network.  
3. Ring Topology:
    Devices are connected in a closed loop, forming a ring. Data travels in one direction.  
    - Pros: Efficient for managing data flow in some applications.  
    - Cons: The network can fail if a single link breaks or a node fails.   
4. Mesh Topology:
    Devices are connected to multiple other devices, providing redundancy.   
    - Pros: High redundancy and fault tolerance.  
    - Cons: Can be expensive and complex to set up, especially with full mesh connections.   
5. Tree Topology:
    A hybrid structure combining elements of star and bus topologies.   
    - Pros: Highly scalable, good for larger networks.  
    - Cons: Can be complex to manage, and if the root node fails, the entire network may be affected.   
6. Hybrid Topology:
    A combination of two or more different topologies to leverage their strengths

## 7. Difference between a LAN, WAN, and MAN <a name="question7"></a>

The main difference between a LAN, MAN, and WAN is their geographic coverage: a LAN is a small, local network (like a home or office), a MAN covers a larger metropolitan area (like a city), and a WAN spans vast distances, connecting cities, countries, or even continents. This difference in scale also impacts other characteristics, such as speed (LANs are fastest, WANs slowest), cost (LANs are least expensive, WANs most), and complexity. 

1. LAN (Local Area Network)
    - Coverage: 
        Small, local areas like a single home, office building, or university campus. 
    - Speed: 
        Very high speeds due to short distances and limited congestion. 
    - Cost: 
        Relatively low cost to set up and maintain. 
    - Examples: 
        Your home Wi-Fi network, an office network connecting computers and printers. 
2. MAN (Metropolitan Area Network)
    - Coverage:
        A larger area than a LAN, such as a city, a large campus with multiple buildings, or a region. 
    -   Speed:
        Slower than a LAN but faster than a WAN, offering moderate speeds over distances. 
    - Cost:
        More expensive than a LAN but less expensive than a WAN, with higher maintenance complexity. 
    - Examples:
        City-wide Wi-Fi networks, connecting multiple corporate sites within a single city, or a large university campus. 
3. WAN (Wide Area Network)
    - Coverage:
        Broadest geographic coverage, connecting locations across countries or even globally. 
    - Speed:
        Slower than LANs and MANs due to the vast distances and multiple network hops, leading to longer delays. 
    - Cost:
        Most expensive and complex to design and maintain. 
    - Examples:
        The Internet, or large corporate networks that connect offices in different countries. 

## 8.  <a name="question8"></a>

## 9.  <a name="question9"></a>

## 10.  <a name="question10"></a>