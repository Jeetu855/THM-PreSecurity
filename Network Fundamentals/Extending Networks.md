
### Port Forwarding

Without port forwarding, applications and services such as web servers are only available to devices within the same direct network.

Port forwarding is a network configuration technique used to redirect incoming network traffic from one network port to another, typically on a different device within a local area network (LAN). It's often used to enable external access to services or applications running on devices behind a router or firewall. Port forwarding can be useful for tasks such as setting up a web server, gaming, remote desktop access, or hosting online services.

##### How does it work?

1. **Understanding Ports:** In networking, a port is a virtual endpoint for communication. Ports are identified by numbers, ranging from 1 to 65535. Well-known ports (0-1023) are reserved for specific services (e.g., port 80 for HTTP, port 22 for SSH).
    
2. **Router Configuration:** ***Port forwarding is typically configured on a home or office router.*** You access the router's web interface using a web browser and log in with the router's admin credentials. The router's IP address and login information are usually provided by the router manufacturer.
    
3. **Choose a Port:** You select a specific external (public) port number on your router that will receive incoming traffic. This is the port through which external devices will communicate with your internal device.
    
4. **Specify the Internal IP Address:** You ***specify the internal IP address of the device on your local network that you want to forward the traffic to***. This could be the IP address of your computer, server, or any other networked device.
    
5. **Set Up the Forwarding Rule:** In your router's settings, you ***create a forwarding rule that associates the external port with the internal IP address and internal port. This tells the router to send incoming traffic on the specified external port to the internal device's port.***
    
6. **Save and Activate:** After configuring the port forwarding rule, you typically save the settings and activate the rule. Some routers may require a reboot to apply the changes.


Example:Within this network, the server with an IP address of "192.168.1.10" runs a webserver on port 80. Only the two other computers on this network will be able to access it ***this is known as an intranet and not internet***

![[portForwarding.png]]

If the administrator wanted the website to be accessible to the public (using the Internet), they would have to implement port forwarding

![[port_forwarding.png]]


With this design, Network #2 will now be able to access the webserver running on Network #1 using the public IP address of Network #1 (82.62.51.70).

port forwarding opens specific ports . In comparison, firewalls determine if traffic can travel across these ports (even if these ports are open by port forwarding).

***Port forwarding is configured at the router of a network.***



---


### Firewalls

A firewall is a device within a network responsible for determining what traffic is allowed to enter and exit. Think of a firewall as border security for a network. An administrator can configure a firewall to **permit** or **deny** traffic from entering or exiting a network based on numerous factors such as:

- Where the traffic is coming from? (has the firewall been told to accept/deny traffic from a specific network?)
- Where is the traffic going to? (has the firewall been told to accept/deny traffic destined for a specific network?)
- What port is the traffic for? (has the firewall been told to accept/deny traffic destined for port 80 only?)
- What protocol is the traffic using? (has the firewall been told to accept/deny traffic that is UDP, TCP or both?)

***Firewalls perform packet inspection to determine the answers to these questions.***

Firewalls come in all shapes and sizes. From dedicated pieces of hardware (often found in large networks like businesses) that can handle a magnitude of data to residential routers (like at your home!) or software such as Snort.

|   |   |
|---|---|
|**Firewall Category**|**Description**|
|Stateful|This type of firewall uses the entire information from a connection; rather than inspecting an individual packet, this firewall determines the behaviour of a device **based upon the entire connection**.<br><br>***This firewall type consumes many resources in comparison to stateless firewalls as the decision making is dynamic***. For example, a firewall could allow the first parts of a TCP handshake that would later fail.<br><br>If a connection from a host is bad, it will block the entire device.|
|Stateless|***This firewall type uses a static set of rules to determine whether or not individual packets are acceptable or not***. For example, a device sending a bad packet will not necessarily mean that the entire device is then blocked.<br><br>Whilst these firewalls use much fewer resources than alternatives, they are much dumber. For example, these firewalls are only effective as the rules that are defined within them. If a rule is not exactly matched, it is effectively useless.<br><br>However, these firewalls are great when receiving large amounts of traffic from a set of hosts (such as a Distributed Denial-of-Service attack)|

***Firewalls operate at network and application layer***


---

### VPN(Virtual Private Network)

***A Virtual Private Network (VPN) is a technology that allows devices on separate networks to communicate securely by creating a dedicated path between each other over the Internet (known as a tunnel). Devices connected within this tunnel form their own private network.***

Only devices within the same network (such as within a business) can directly communicate. However, a VPN allows two offices to be connected.

![[vpn.png]]

1. Network #1 (Office #1)
2. Network #2 (Office #2)
3. Network #3 (Two devices connected via a VPN)

The devices connected on Network #3 are still a part of Network #1 and Network #2 but also form together to create a private network (Network #3) that only devices that are connected via this VPN can communicate over.


  

|   |   |
|---|---|
|**Benefit**|**Description**|
|Allows networks in different geographical locations to be connected.|For example, a business with multiple offices will find VPNs beneficial, as it means that resources like servers/infrastructure can be accessed from another office.|
|Offers privacy.|VPN technology uses encryption to protect data. This means that it can only be understood between the devices it was being sent from and is destined for, meaning the data isn't vulnerable to sniffing.<br><br>This encryption is useful in places with public WiFi, where no encryption provided by the network. You can use a VPN to protect your traffic from being viewed by other people.|
|Offers anonyminity.|Journalists and activists depend upon VPNs to safely report on global issues in countries where freedom of speech is controlled.<br><br>Usually, your traffic can be viewed by your ISP and other intermediaries and therefore tracked. <br><br>The level of anonymity a VPN provides is only as much as how other devices on the network respect privacy.. For example, a VPN that logs all of your data/history is essentially the same as not using a VPN in this regard.|



TryHackMe uses a VPN to connect you to it's vulnerable machines without making them directly accessible on the Internet! This means that:

- You can securely interact with it's machines
- Service providers such as ISPs don't think you are attacking another machine on the Internet (which could be against the terms of service)
- The VPN provides security to TryHackMe as vulnerable machines are not accessible using the Internet.

|   |   |
|---|---|
|**VPN Technology**|**Description**|
|PPP|This technology is used by PPTP  to allow for authentication and provide encryption of data. VPNs work by using a private key and public certificate (similar to **SSH**). A private key & certificate must match for you to connect.<br><br>This technology is not capable of leaving a network by itself (non-routable).|
|PPTP|The **P**oint-to-**P**oint **T**unneling **P**rotocol (**PPTP**) is the technology that allows the data from PPP to travel and leave a network. <br><br>PPTP is very easy to set up and is supported by most devices. It is, however, weakly encrypted in comparison to alternatives.|
|IPSec|Internet Protocol Security (IPsec) encrypts data using the existing **I**nternet **P**rotocol (**IP**) framework.<br><br>IPSec is difficult to set up in comparison to alternatives; however, if successful, it boasts strong encryption and is also supported on many devices.|


---

### Networking Devices


##### Router

It's a router's job to connect networks and pass data between them. It does this by using routing
Routing is the label given to the process of data travelling across networks. Routing involves creating a path between networks so that this data can be successfully delivered. Routers operate at Layer 3 of the OSI model. They often feature an interactive interface (such as a website or a console) that allows an administrator to configure various rules such as port forwarding or firewalling.


##### Switch

A switch is a dedicated networking device responsible for providing a means of connecting to multiple devices. Switches can facilitate many devices (from 3 to 63) using Ethernet cables.

Switches can operate at both layer 2 and layer 3 of the OSI model. However, these are exclusive in the sense that Layer 2 switches cannot operate at layer 3.

layer 3 switches. These switches are more sophisticated than layer 2, as they can perform _some_ of the responsibilities of a router. Namely, these switches will send frames to devices (as layer 2 does) and route packets to other devices using the IP protocol.]


A technology called **VLAN** (**V**irtual **L**ocal **A**rea **N**etwork) allows specific devices within a network to be virtually split up. This split means they can all benefit from things such as an Internet connection but are treated separately. This network separation provides security because it means that rules in place determine how specific devices communicate with each other.

![[layer3switch.png]]

In the context of the diagram above, the "Sales Department" and "Accounting Department" will be able to access the Internet, but not able to communicate with each othe

