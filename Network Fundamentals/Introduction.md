
Networks are simply things connected
The Internet is one giant network that consists of many, many small networks within itself.

![[Network.png]]

A network can be one of two types:  

- A private network   
- A public network


The small networks are called private networks, where as the networks connecting these small networks are called public networks or the Internet

To communicate and maintain order, devices must be both identifying and identifiable on a network.
- Identifying other devices as to who they are and
- Identifiable by others

Devices on a network are very similar to humans in the fact that we have two ways of being identified:

- Our Name
- Our Fingerprints

Devices have the same thing: two means of identification, with one being permeable. These are:

- An IP Address (can change)
- A Media Access Control (MAC) Address -- think of this as being similar to a serial number.

MAC address cannot be changed, it is etched into the Network Interface Card(NIC)

#### IP ADDRESS
An IP address (Internet Protocol) address can be used as a way of identifying a host on a network for a period of time, where that IP address can then be associated with another device without the IP address changing

IP Address are of 32 bits split into 4 octets each of 8 bits
The value in each octet can range from 0-255((2^0) to (2^8 -1))

IP address differ from device to device and they are unique inside a network.
So Internet being a large network, all devices are uniquely numbered but since there
are only 2^32 or 4294967296 IPv4 address and a lot more than that devices in our world, we use techniques like NAT(Network Address Translation) and PAT(Port Address Translation)

Devices can be on both a private and public network. Depending on where they are will determine what type of IP address they have: a public or private IP address.
A public address is used to identify the device on the Internet, whereas a private address is used to identify a device amongst other devices.

example : 
IP 1 = 192.168.57.5
IP 2 = 192.168.57.7
***These two devices will be able to use their private IP addresses to communicate with each other. However, any data sent to the Internet from either of these devices will be identified by the same public IP address. Public IP addresses are given by your Internet Service Provider (or ISP) at a monthly fee***

***Using Private IP we can communicate inside private network and by using public IP provided by the ISP we can communicate with Public Network***

IPv6 is a new iteration of the Internet Protocol addressing scheme to help tackle the issue of increasing number of devices and less number of IPv4 addresses. Benefits of IPv6

- Supports up to 2^128 of IP addresses (340 trillion-plus), resolving the issues faced with IPv4
- More efficient due to new methodologies

#### MAC ADDRESS

Devices on a network will all have a physical network interface card, which is a microchip board found on the device's motherboard. This network interface is assigned a unique address at the factory it was built at, called a **MAC** (**M**edia **A**ccess **C**ontrol ) address. The MAC address is a **twelve-character** hexadecimal number (_a base sixteen numbering system used in computing to represent numbers_) split into two's and separated by a colon. These colons are considered separators.


![[MAC.png]]


First 6 hexadecimal characters are called Organizationally Unique Identifier(OUI) which are unique to an organization and last 6 hexadecimal characters identify the NIC made by that company

However, an interesting thing with MAC addresses is that they can be faked or "spoofed" in a process known as spoofing. This spoofing occurs when a networked device pretends to identify as another using its MAC address. When this occurs, it can often break poorly implemented security designs that assume that devices talking on a network are trustworthy. Take the following scenario: A firewall is configured to allow any communication going to and from the MAC address of the administrator. If a device were to pretend or "spoof" this MAC address, the firewall would now think that it is receiving communication from the administrator when it isn't.


#### PING

Ping is one of the most fundamental network tools available to us. Ping uses **ICMP**               (**I**nternet **C**ontrol **M**essage **P**rotocol) packets to determine the performance of a connection 
between devices

The time taken for ICMP packets travelling between devices is measured by ping. This measuring is done using ICMP's echo packet and then ICMP's echo reply from the target device.

It is a protocol of Layer 3(Network Layer)


