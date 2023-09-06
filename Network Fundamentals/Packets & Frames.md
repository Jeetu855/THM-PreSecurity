

#### What are Packets and Frames?

Packets and frames are small pieces of data that, when forming together, make a larger piece of information or message.
A frame is at layer 2 - the data link layer, meaning there is no such information as IP addresses. Think of this as putting an envelope within an envelope and sending it away. The first envelope will be the packet that you mail, but once it is opened, the envelope within still exists and contains data (this is a frame).

This process is called encapsulation

when we are talking about anything IP addresses, we are talking about packets
Packets are an efficient way of communicating data across networked devices such as those
Because this data is exchanged in small pieces, there is less chance of bottlenecking occurring across a network than large messages being sent at once.
when loading an image from a website, this image is not sent to your computer as a whole, but rather small pieces where it is reconstructed on your computer

Example:The cat's picture is divided into three packets, where it is reconstructed when it reaches the computer to form the final image.


![[tcp.png]]

Packets have different structures that are dependant upon the type of packet that is being sent.


|   |   |
|---|---|
|**Header**|**Description**|
|Time to Live|This field sets an expiry timer for the packet to not clog up your network if it never manages to reach a host or escape!|
|Checksum|This field provides integrity checking for protocols such as TCP/IP. If any data is changed, this value will be different from what was expected and therefore corrupt.|
|Source Address|The IP address of the device that the packet is being sent **from** so that data knows where to **return to**.|
|Destination Address|The device's IP address the packet is being sent to so that data knows where to travel next.|


---

### TCP Three Way Handshake

The TCP/IP protocol consists of four layers and is arguably just a summarised version of the OSI model. These layers are:

- Application
- Transport
- Internet
- Network Interface

Very similar to how the OSI model works, information is added to each layer of the TCP model as the piece of data (or packet) traverses it.
this process is known as encapsulation - where the reverse of this process is decapsulation.

One defining feature of TCP is that it is **connection-based**, which means that TCP must establish a connection between both a client and a device acting as a server **before** data is sent.

TCP guarantees that any data sent will be received on the other end. This process is named the Three-way handshake


|   |   |
|---|---|
|**Advantages of TCP**|**Disadvantages of TCP**|
|Guarantees the integrity of data.|Requires a reliable connection between the two devices. If one small chunk of data is not received, then the entire chunk of data cannot be used and must be re-sent.|
|Capable of synchronising two devices to prevent each other from being flooded with data in the wrong order.|A slow connection can bottleneck another device as the connection will be reserved on the other device the whole time.|
|Performs a lot more processes for reliability|TCP is significantly slower than UDP because more work (computing) has to be done by the devices using this protocol.|

TCP packets contain various sections of information known as headers that are added from encapsulation.


_Three-way handshake -_ the term given for the process used to establish a connection between two devices. The Three-way handshake communicates using a few special messages

|   |   |   |
|---|---|---|
|**Step**|**Message**|**Description**|
|1|SYN|A SYN message is the initial packet sent by a client during the handshake. This packet is used to initiate a connection and synchronise the two devices together.|
|2|SYN/ACK|This packet is sent by the receiving device (server) to acknowledge the synchronisation attempt from the client.|
|3|ACK|The acknowledgement packet can be used by either the client or server to acknowledge that a series of messages/packets have been successfully received.|
|4|DATA|Once a connection has been established, data (such as bytes of a file) is sent via the "DATA" message.|
|5|FIN|This packet is used to _cleanly (properly)_ close the connection after it has been complete.|
|#|RST|This packet abruptly ends all communication. This is the last resort and indicates there was some problem during the process. For example, if the service or application is not working correctly, or the system has faults such as low resources.|


![[3_wayHandshake.png]]

Any sent data is given a random number sequence and is reconstructed using this number sequence and incrementing by 1.


- SYN/ACK - Server: Here's my Initial Sequence Number (ISN) to SYNchronise with (5,000), and I ACKnowledge your initial number sequence (0)
- ACK - Client: I ACKnowledge your Initial Sequence Number (ISN) of (5,000), here is some data that is my ISN+1 (0 + 1)

Because TCP reserves system resources on a device, it is best practice to close TCP connections as soon as possible.
To initiate the closure of a TCP connection, the device will send a "FIN" packet to the other device. Of course, with TCP, the other device will also have to acknowledge this packet.

![[3_wayFIN.png]]


---

### UDP/IP

UDP is a **stateless** protocol that doesn't require a constant connection between the two devices for data to be sent. For example, the Three-way handshake does not occur, nor is there any synchronisation between the two devices.
UDP is used in situations where applications can tolerate data being lost (such as video streaming or voice chat) or in scenarios where an unstable connection is not the end-all.

|   |   |
|---|---|
|Advantages of UDP|Disadvantages of UDP|
|UDP is much faster than TCP|UDP dosent care if data is received or not|
|UDP leaves the application(client software) to decide if there is any control over how quickly packets are sent|It is quite flexible to software developers in this sense|
|UDP does not reserve a continuous connection on a device like TCP does|This means that unstable connections result in a terrible experience for the user|


***No process takes place in setting up a connection between two devices. Meaning that there is no regard for whether or not data is received, and there are no safeguards such as those offered by TCP(like Checksum), such as data integrity.***
UDP packets are much simpler than TCP packets and have fewer headers

![[udpTransmission.png]]



---


Ports are an essential point in which data can be exchanged. Think of a harbour and port. Ships wishing to dock at the harbour will have to go to a port compatible with the dimensions and the facilities located on the ship. When the ship lines up, it will connect to a **port** at the harbour. Take, for instance, that a cruise liner cannot dock at a port made for a fishing vessel and vice versa.These ports enforce what can park and where


Networking devices also use ports to enforce strict rules when communicating with one another. When a connection has been established, any data sent or received by a device will be sent through these ports. In computing, ports are a numerical value between **0** and **65535** (65,535).
Because ports can range from anywhere between 0-65535, there quickly runs the risk of losing track of what application is using what port. A busy harbour is chaos! So we associate applications, software and behaviours with a standard set of rules. For example, by enforcing that any web browser data is sent over port 80, software developers can design a web browser such as Google Chrome or Firefox to interpret the data the same way as one another.

Any port that is within **0** and **1024** (1,024) is known as a common port.

|   |   |   |
|---|---|---|
|**Protocol**|**Port Number**|**Description**|
|**F**ile **T**ransfer **P**rotocol (**FTP**)|21|This protocol is used by a file-sharing application built on a client-server model, meaning you can download files from a central location.|
|**S**ecure **Sh**ell (**SSH**)|22|This protocol is used to securely login to systems via a text-based interface for management.|
|**H**yper**T**ext Transfer Protocol (**HTTP**)|80|This protocol powers the World Wide Web (WWW)! Your browser uses this to download text, images and videos of web pages.|
|**H**yper**T**ext **T**ransfer **P**rotocol **S**ecure (**HTTPS**)|443|This protocol does the exact same as above; however, securely using encryption.|
|**S**erver **M**essage **B**lock (**SMB**)|445|This protocol is similar to the File Transfer Protocol (FTP); however, along with files, SMB allows you to share devices like printers.|
|**R**emote **D**esktop **P**rotocol (**RDP**)|3389|This protocol is a secure means of logging in to a system using a visual desktop interface (as opposed to the text-based limitations of the SSH protocol).|


What is worth noting here is that these protocols only follow the standards. I.e. you can administer applications that interact with these protocols on a different port other than what is the standard (running a web server on 8080 instead of the 80 standard port).  However, applications will presume that the standard is being followed, so you will have to provide a **colon (:)** along with the port number.

