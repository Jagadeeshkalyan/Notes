* IP Address: Unique address given to a system in a network to communicate.
	--> There are currently two main versions of IP Address
		==> IPv4: This is a 32 bit address represented in decimal
		==> IPv6: This is 128 bit address represented in hexadecimal

* IpV4:
	--> This is represented as x.x.x.x. Each x represents an octet (8-bit). 
	--> In Each octet we can have the decimal values ranging from 0 to 255
	--> min => 0.0.0.0 max => 255.255.255.255

* IP Address = Network Id + Host Id
	--> e.g. Input : 1.4.5.5
	Output :
		Given IP address belongs to Class A so, subnet mask = 255.0.0.0
		Network ID is 1
		Host ID is 4.5.5
		Size of host id = 3*8 =24
		No. of host in this network = (2^24) -2

	--> e.g. Input : 130.45.151.154
	Output :
		Given IP address belongs to Class B. so, subnet mask = 255.255.0.0
		Network ID is 130.45
		Host ID is 151.154
		Size of host id(n)= 2*8 =16
		No. of host in this network = (2^n)-2 = (2^16) -2

explanation: 1. For determining the class: The idea is to check the first octet of the IP addresses. As we know, 
	for class A first octet will range from 1 � 126, 
	for class B first octet will range from 128 � 191, 
	for class C first octet will range from 192- 223, 	
	for class D first octet will range from 224 � 239, 
	for class E first octet will range from 240 � 255. 
	2. For determining the Network and Host ID: We know that Subnet Mask 
	for Class A is 8, 
	for Class B is 16 and 	
	for Class C is 24 whereas 	
	Class D and E are not divided into Network and Host ID.
NOTE: 2^n -2 (minus 2 is for multicast & reserved)
	
* CIDR --> This stands for Classless Inter-Domain Routing

	--> ip : 192.168.0.100
	    SM : 255.255.255.0
               : 11111111.11111111.11111111.00000000 => 192.168.0.100/24
	
	--> cidr: 192.168.0.0/23
	    n = 32-23 =9 
	    No. of host in this network = (2^n)-2 = (2^9) -2 = 512-2 = 510

	--> cidr: 192.168.0.0/25
	    n = 32-25 = 7
	    No. of host in this network = (2^n)-2 = (2^7) -2 = 128-2 = 126

* Convention of Public Networks and Private Networks:
	--> Public Networks are ip addresses which are accessible over internet
	--> Private networks are for private usage & there are some reserved ip ranges for private networking. In all the clouds and in the 
	enterprise when we configure networking its always private network.
		1. 192.168.0.0/16
		2. 10.0.0.0/8
		3. 172.16.0.0/12
* Create 4 subnets from the overall network 192.168.0.0/21 
cidr: 192.168.0.0/21
sm: 11111111.11111111.11111000.00000000
	n = 32-21 = 11
	2^11 = 2048 
	2048/4 = 512
so, in block size of network = 512 = 2^9, n = 9
	n = 32 - cidr value
	9 = 32 - cidr value
	cidr value = 32-9 = 23
now overall sm = 11111111.11111111.11111000.00000000
      block sm = 11111111.11111111.11111110.00000000
		 -----------------------------------
		 11111111.11111111.11111xx0.00000000
block 1 : 11000000.10101000.00000000.00000000 = 192.168.0.0/23
block 2 : 11000000.10101000.00000010.00000000 = 192.168.2.0/23
block 3 : 11000000.10101000.00000100.00000000 = 192.168.4.0/23
block 4 : 11000000.10101000.00000110.00000000 = 192.168.6.0/23

* Routing: The basic functionality of Router is to forward the packet from one network to another.

* Each subnet will have router with some rule defined to forward the packets. These rules are referred as Route Tables.

* Traceroute: (tracert (Windows) traceroute (linux)) will show the hops to reach to the desired device. 

* NAT Gateway: NAT gateway provides outbound internet connectivity for one or more subnets of a virtual network. 
	--> Once NAT gateway is associated to a subnet, NAT provides source network address translation (SNAT) for that subnet.
	--> NAT gateway specifies which static IP addresses virtual machines use when creating outbound flows.

* Domain Name:
	--> A website is made up of files like HTML pages, website builder software, images, and more.
	--> If the domain name is the web address of your website, then web hosting is the home where your website lives. 
	--> The most popular one is .com. There are many other options like .org, .net, .tv, .info, .io, and more.
	--> Different types of domain names available:
		--> Top Level Domain � TLD:
			* These are generic domain extensions that are listed at the highest level in the domain name system.
			* There are hundreds of TLDs, but the most popular ones are .com, .org, and .net. 
			* Other TLDs are lesser known and we don�t recommend using them. For example, .biz, .club, .info, .agency, and many more.
		--> Country Code Top Level Domain � ccTLD:
			* These are country specific domain names which end with country code extension like .uk for the United Kingdom, .de for 
			Germany, .in for India.
		--> Sponsored Top Level Domain � sTLD:
			* It is a category of TLDs that has a sponsor representing a specific community served by the domain extension.
			* For example, .edu for education-related organizations, .gov for the United States government, .mil for the United States 
			military, and more.






* Networking capabilities:
	1. Connectivity services
	2. Application protection services
	3. Application delivery services
	4. Network monitoring services
* Peering is used to ping from one private network to other private network.

Network types
-------------
  1. Personal area network:
	* Let devices connect and communicate over the range of a person. E.g. connecting Bluetooth devices.
  2. Local area network:
	* It is a privately owned network that operates within and nearby a single building like a home, office, or factory.
  3. Metropolian area network:
	* It connects and covers the whole city. E.g. TV Cable connection over the city.
  4. Wide area network:
	* It spans a large geographical area, often a country or continent. The Internet is the largest WAN.
  5. Global area network:
	* It is also known as the Internet which connects the globe using satellites. The Internet is also called the Network of WANs.

VPN (Virtual Private Network)
---
* Virtual Private Network is a private WAN (Wide Area Network) built on the internet. 
* It allows the creation of a secured tunnel (protected network) between different networks using the internet (public network). 
* By using the VPN, a client can connect to the organization’s network remotely.
* Advantages of using a VPN:
	1. It is used to connect offices in different geographical locations remotely and is cheaper when compared to WAN connections.
	2. It is used for secure transactions and confidential data transfer between multiple offices located in different geographical locations.
	3. keeps an organization’s information secured against any potential threats or intrusions by using virtualization.
	4. encrypts the internet traffic and disguises the online identity.
   
Types of VPN:
------------


* Node: 
  * Any communicating device in a network is called a Node.
  * Node is the point of intersection in a network. It can send/receive data and information within a network.
  E.g.: computers, laptops, printers, servers, modems, etc.

* Link: 
  * A link or edge refers to the connectivity between two nodes in the network.
  * It includes the type of connectivity (wired or wireless) between the nodes and protocols used for one node to be able to communicate with the other.

* Network topology:
  * Network topology is a physical layout of the network, connecting the different nodes using the links. It depicts the connectivity between the computers, devices, cables, etc.
  * Types of network topology:
		1. Bus Topology:
			* All the nodes are connected using the central link known as the bus.
			* It is useful to connect a smaller number of devices.
			* If the main cable gets damaged, it will damage the whole network.
		2. Star Topology:
			* All the nodes are connected to one single node known as the central node.
			* It is more robust.
			* If the central node fails the complete network is damaged.
			* Easy to troubleshoot.
			* Mainly used in home and office networks.
		3. Ring Topology:
			* Each node is connected to exactly two nodes forming a ring structure.
			* If one of the nodes are damaged, it will damage the whole network.
			* It is used very rarely as it is expensive and hard to install and manage
		4. Mesh Topology:
			* Each node is connected to one or many nodes.
			* It is robust as failure in one link only disconnects that node.
			* It is rarely used and installation and management are difficult.
		5. Tree Topology:
			* A combination of star and bus topology also know as an extended bus topology.
			* All the smaller star networks are connected to a single bus.
			* If the main bus fails, the whole network is damaged.
		6. Hybrid:
			* It is a combination of different topologies to form a new topology.
			* It helps to ignore the drawback of a particular topology and helps to pick the strengths from other.

IPv4 address:
-------------
* An IP address is a 32-bit dynamic address of a node in the network. 
* An IPv4 address has 4 octets of 8-bit each with each number with a value up to 255.

Private Address: 
----------------
* For each class, there are specific IPs that are reserved specifically for private use only.
* This IP address cannot be used for devices on the Internet as they are non-routable.
	1. 10.0.0.0/8
	2. 172.16.0.0/12
	3. 192.168.0.0/16

Special Address: 
----------------
* IP Range from 127.0.0.1 to 127.255.255.255 are network testing addresses also known as loopback addresses are the special IP address.

Open System Interconnections (OSI):
-----------------------------------
* It is a network architecture model based on the ISO standards
* 7 layers of the OSI reference model:
  1. Physical
  2. Data Link
  3. Network
  4. Transport
  5. Session
  6. Presentation
  7. Application
   
TCP/IP Reference Model:
----------------------
* It is a compressed version of the OSI model with only 4 layers.
* TCP (Transmission Control Protocol) and IP (Internet Protocol).
	1. Link
	2. Internet
	3. Transport
	4. Application

OSI Reference Model |	TCP/IP Reference Model
------------------------------------------>
7 layered architecture |	4 layered architecture
Fixed boundaries and functionality for each layer |	Flexible architecture with no strict boundaries between layers
Low Reliability|	High Reliability
Vertical Layer Approach |	Horizontal Layer Approach

HTTP and the HTTPS protocol:
---------------------------
* HTTP is the HyperText Transfer Protocol which defines the set of rules and standards on how the information can be transmitted on the World Wide Web (WWW).
* It is an application layer protocol built upon the TCP. It uses port 80 by default.
* HTTPS is the HyperText Transfer Protocol Secure or Secure HTTP. It is an advanced and secured version of HTTP. 
* On top of HTTP, SSL/TLS protocol is used to provide security. 
* It enables secure transactions by encrypting the communication and also helps identify network servers securely. It uses port 443 by default.

SMTP protocol:
-------------
* Simple Mail Transfer Protocol sets the rule for communication between servers.
* This set of rules helps the software to transmit emails over the internet. 
* It supports both End-to-End and Store-and-Forward methods. 
* It is in always-listening mode on port 25.

DNS:
---
* DNS is the Domain Name System. 
* It is considered as the devices/services directory of the Internet. 
* It is a decentralized and hierarchical naming system for devices/services connected to the Internet. 
* It translates the domain names to their corresponding IPs. For e.g. interviewbit.com to 172.217.166.36. It uses port 53 by default.

Router
------
* The router is a networking device used for connecting two or more network segments. It directs the traffic in the network. 
* It transfers information and data like web pages, emails, images, videos, etc. from source to destination in the form of packets. It operates at the network layer. 
* The gateways are also used to route and regulate the network traffic but, they can also send data between two dissimilar networks while a router can only send data to similar networks.

Diff b/w TCP & UDP
------------------

TCP | UDP User Datagram Protocol
Connection-Oriented Protocol |	Connectionless Protocol
More Reliable |	Less Reliable
Slower Transmission | Faster Transmission
Packets order can be preserved or can be rearranged |	Packets order is not fixed and packets are independent of each other
Uses three ways handshake model for connection |	No handshake for establishing the connection
TCP packets are heavy-weight |	UDP packets are light-weight
Offers error checking mechanism | No error checking mechanism
Protocols like HTTP, FTP, Telnet, SMTP, HTTPS, etc use TCP at the transport layer |	Protocols like DNS, RIP, SNMP, RTP, BOOTP, TFTP, NIP, etc use UDP at the transport layer

ICMP protocol:
--------------
* ICMP is the Internet Control Message Protocol. 
* It is a network layer protocol used for error handling. 
* It is mainly used by network devices like routers for diagnosing the network connection issues and crucial for error reporting and testing if the data is reaching the preferred destination in time. It uses port 7 by default

DHCP Protocol:
--------------
* Dynamic Host Configuration Protocol.
* It is an application layer protocol used to auto-configure devices on IP networks enabling them to use the TCP and UDP-based protocols. 
* The DHCP servers auto-assign the IPs and other network configurations to the devices individually which enables them to communicate over the IP network. 
* It helps to get the subnet mask, IP address and helps to resolve the DNS. It uses port 67 by default

ARP Protocol:
-------------
* ARP is Address Resolution Protocol. It is a network-level protocol used to convert the logical address i.e. IP address to the device's physical address i.e. MAC address. 
* It can also be used to get the MAC address of devices when they are trying to communicate over the local network

FTP Protocol:
-------------
* FTP is a File Transfer Protocol. It is an application layer protocol used to transfer files and data reliably and efficiently between hosts. It can also be used to download files from remote servers to your computer. It uses port 27 by default.

MAC address:
------------
MAC address is the Media Access Control address. It is a 48-bit or 64-bit unique identifier of devices in the network. It is also called the physical address embedded with Network Interface Card (NIC) used at the Data Link Layer. NIC is a hardware component in the networking device using which a device can connect to the network.

Diff b/w MAC & IP Address:
--------------------------
Media Access Control Address |	Internet Protocol Address
6 or 8-byte hexadecimal number |	4 (IPv4) or 16 (IPv6) Byte address
It is embedded with NIC	| It is obtained from the network
Physical Address |	Logical Address
Operates at Data Link Layer |	Operates at Network Layer.
Helps to identify the device |	Helps to identify the device connectivity on the network.

Subnet:
-------
* A subnet is a network inside a network achieved by the process called subnetting which helps divide a network into subnets. It is used for getting a higher routing efficiency and enhances the security of the network. It reduces the time to extract the host address from the routing table.

* MAC Address | IP Address
	1. Operates at Physical Layer |	Operates at Data Link Layer
	2. Half-Duplex transmission mode	| Full-Duplex transmission mode
	3. Ethernet devices can be connectedsend	| LAN devices can be connected
	4. Less complex, less intelligent, and cheaper	| Intelligent and effective
	5. No software support for the administration |	Administration software support is present
	6. Less speed up to 100 MBPS |	Supports high speed in GBPS
	7. Less efficient as there is no way to avoid collisions when more than one nodes sends the packets at the same time |	More efficient as the collisions can be avoided or reduced as compared to Hub

* ipconfig	| ifconfig
	1. Internet Protocol Configuration	| Interface Configuration
	2. Command used in Microsoft operating systems to view and configure network interfaces |	Command used in MAC, Linux, UNIX operating systems to view and configure network interfaces
Used to get the TCP/IP summary and allows to changes the DHCP and DNS settings

* Firewall:
	* The firewall is a network security system that is used to monitor the incoming and outgoing traffic and blocks the same based on the firewall security policies. 
	* It acts as a wall between the internet (public network) and the networking devices (a private network). 
	* It is either a hardware device, software program, or a combination of both. It adds a layer of security to the network.

* Unicasting: 
  * If the message is sent to a single node from the source then it is known as unicasting. This is commonly used in networks to establish a new connection.

* Anycasting: 
  * If the message is sent to any of the nodes from the source then it is known as anycasting.
  * It is mainly used to get the content from any of the servers in the Content Delivery System.

* Multicasting: 
  * If the message is sent to a subset of nodes from the source then it is known as multicasting. Used to send the same data to multiple receivers. 
* Broadcasting: 
  If the message is sent to all the nodes in a network from a source then it is known as broadcasting. DHCP and ARP in the local network use broadcasting.



