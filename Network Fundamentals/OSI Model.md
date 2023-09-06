
### OSI(Open Systems Interconnect)

The **OSI** model (or **O**pen **S**ystems **I**nterconnection Model) is an absolute fundamental model used in networking.  This critical model provides a framework dictating how all networked devices will send, receive and interpret data.
One of the main benefits of the OSI model is that devices can have different functions and designs on a network while communicating with other devices. Data sent across a network that follows the uniformity of the OSI model can be understood by other devices.
At every individual layer that data travels through, specific processes take place, and pieces of information are added to this data

![[osi.png]]


---

### Layer 7(Application Layer)

Application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received.

Everyday applications such as email clients, browsers, or file server browsing software such as FileZilla provide a friendly, **G**raphical **U**ser **I**nterface (**GUI**) for users to interact with data sent or received. Other protocols include **DNS** (**D**omain **N**ame **S**ystem), which is how website addresses are translated into IP addresses.

---

### Layer 6(Presentation Layer)

layer in which standardization starts to take place
***This layer acts as a translator for data to and from the application layer (layer 7). The receiving computer will also understand data sent to a computer in one format destined for in another format.***
***Security features such as data encryption (like HTTPS when visiting a secure site) occur at this layer***


---

### Layer 5(Session Layer)

Once data has been correctly translated or formatted from the presentation layer (layer 6), the session layer (layer 5) will begin to ***create a connection to the other computer that the data is destined for. When a connection is established, a session is created. Whilst this connection is active, so is the session***
***The session layer (layer 5) synchronizes the two computers to ensure that they are on the same page before data is sent and received.*** Once these checks are in place, the session layer will begin to divide up the data sent into smaller chunks of data and begin to send these chunks (packets) one at a time. This dividing up is beneficial because if the connection is lost, only the chunks that weren't yet sent will have to be sent again — not the entire piece of the data
sessions are unique — meaning that data cannot travel over different sessions, but in fact, only across each session instead.


---


### Layer 4(Transport Layer)

Layer 4 of the OSI model plays a vital part in transmitting data across a network
When data is sent between devices, it follows one of two different protocols that are decided based upon several factors:

- TCP(Transmission Control Protocol)
- UDP(User Datagram Protocol)

TCP protocol is designed with reliability and guarantee in mind. This protocol reserves a constant connection between the two devices for the amount of time it takes for the data to be sent and received.
Not only this, but TCP incorporates error checking into its design. Error checking is how TCP can guarantee that data sent from the small chunks in the session layer (layer 5) has then been received and reassembled in the same order.

|   |   |
|---|---|
|**Advantages of TCP**|**Disadvantages of TCP  <br>**|
|Guarantees the accuracy of data.|Requires a reliable connection between the two devices. If one small chunk of data is not received, then the entire chunk of data cannot be used.|
|Capable of synchronising two devices to prevent each other from being flooded with data.|A slow connection can bottleneck another device as the connection will be reserved on the receiving computer the whole time.|
|Performs a lot more processes for reliability.|TCP is significantly slower than UDP because more work has to be done by the devices using this protocol.|

TCP provides reliability
TCP is used for situations such as file sharing, internet browsing or sending an email. This usage is because these services require the data to be accurate and complete


![[packets.png]]


UDP protocol is not nearly as advanced as its brother - the TCP protocol. It doesn't boast the many features offered by TCP, such as error checking and reliability. In fact, any data that gets sent via UDP is sent to the computer whether it gets there or not. There is no synchronisation between the two devices or guarantee; just hope for the best, and fingers crossed.

|   |   |
|---|---|
|**Advantages of UDP**|**Disadvantages of UDP**|
|UDP is much faster than TCP.|UDP doesn't care if the data is received.|
|UDP leaves the application layer (user software) to decide if there is any control over how quickly packets are sent.|It is quite flexible to software developers in this sense.|
|UDP does not reserve a continuous connection on a device as TCP does.|This means that unstable connections result in a terrible experience for the user.|



![[udp.png]]


UDP is useful in situations where there are small pieces of data being sent. For example, protocols used for discovering devices (_ARP_ and _DHCP_)


---

### Layer 3(Network Layer)

The third layer of the OSI model (network layer) is where the magic of routing & re-assembly of data takes place (from these small chunks to the larger chunk). Firstly, routing simply determines the most optimal path in which these chunks of data should be sent.

these protocols include **OSPF** (**O**pen **S**hortest **P**ath **F**irst) and **RIP** (**R**outing **I**nformation **P**rotocol). The factors that decide what route is taken is decided by the following:

- What path is the shortest? I.e. has the least amount of devices that the packet needs to travel across.
- What path is the most reliable? I.e. have packets been lost on that path before?
- Which path has the faster physical connection? I.e. is one path using a copper connection (slower) or a fibre (considerably faster)?

At this layer, everything is dealt with via IP addresses such as 192.168.1.100. Devices such as routers capable of delivering packets using IP addresses are known as Layer 3 devices — because they are capable of working at the third layer of the OSI model.

![[router.png]]


---

### Layer 2(Data Link Layer)

The data link layer focuses on the physical addressing of the transmission. It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical **MAC** (Media Access Control) address of the receiving endpoint. Inside every network-enabled computer is a **N**etwork **I**nterface Card (**NIC**) which comes with a unique MAC address to identify it.

MAC addresses are set by the manufacturer and literally burnt into the card; they can't be changed -- although they can be spoofed. When information is sent across a network, it's actually the physical address that is used to identify where exactly to send the information.

Additionally, it's also the job of the data link layer to present the data in a format suitable for transmission.

---

### Layer 1(Physical Layer)

this layer references the physical components of the hardware used in networking and is the lowest layer that you will find. Devices use electrical signals to transfer data between each other in a binary numbering system (1's and 0's).






