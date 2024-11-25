# DEEP-IN-NET

**You need to install Cisco Packet Tracer to complete this exercise. You can install it from [here](https://www.netacad.com/cisco-packet-tracer).**

This repository contains answers to the questions in the audit page for each exercise, along with diagrams and additional explanations where necessary.

## **Introduction**

In this project, we explore various networking concepts and protocols using Cisco Packet Tracer. Each exercise focuses on a different aspect of networking, such as cables, devices, protocols, and network configurations. The answers provided below will help you understand these concepts clearly and how they are applied in networking environments.

---

## **Exercise 1**

![picture](/deep-in-net/ex01.png)

### **1. What is an RJ-45 cable?**

An RJ-45 cable is a network cable used to connect devices like computers, routers, and switches. It has an 8-pin connector and is commonly used for Ethernet connections.

### **2. Difference between straight-through and crossover RJ-45 cables:**

- **Straight-through cable**: The wires on both ends are in the same order. It connects **different** devices, like a computer to a router.
- **Crossover cable**: The wires on one end are rearranged to cross over. It connects **similar** devices, like one computer to another.

---

## **Exercise 2**

![picture](/deep-in-net/ex02.png)

### **1. The function of a switch and a hub, how they operate, and their role in networking:**

- **Switch**: Connects multiple devices in a network, sending data only to the specific device it is meant for. It uses MAC addresses to direct data to the correct port, improving efficiency and reducing congestion.
- **Hub**: Connects multiple devices in a network, but it broadcasts data to all devices, regardless of whether they need it. It does not know where specific devices are and causes more network traffic.

### **2. Differences Between Switch and Hub:**

| Feature           | Switch                          | Hub                            |
| ----------------- | ------------------------------- | ------------------------------ |
| **Data Transfer** | Directs data to specific device | Broadcasts data to all devices |
| **Efficiency**    | High                            | Low                            |
| **Traffic**       | Reduces unnecessary traffic     | Creates more traffic           |
| **Cost**          | More expensive                  | Cheaper                        |
| **Modern Use**    | Commonly used                   | Rarely used                    |

### **3. OSI Model Layer:**

- **Switch**: Operates on **Layer 2** (Data Link Layer) because it uses MAC addresses. Some advanced switches may also work on **Layer 3** (Network Layer).
- **Hub**: Operates on **Layer 1** (Physical Layer) as it simply transmits signals.

---

## **Exercise 3**

![video](/deep-in-net/ex03.gif)

### **1. Define a server and its purpose in networking.**

A **server** is a computer or device that provides services, resources, or data to other computers (clients) over a network. It manages network resources such as files, applications, or websites and provides them when requested.

### **2. Explain DHCP and how it operates in a network.**

**DHCP** (Dynamic Host Configuration Protocol) automatically assigns IP addresses and other configuration details (like gateway and DNS) to devices when they join the network.

### **3. Define DNS and its role in network communication.**

**DNS** (Domain Name System) translates domain names (like `www.example.com`) into IP addresses (like `192.168.1.1`). This helps users access websites using easy-to-remember names instead of numeric IP addresses.

### **4. Understand the purpose of HTTP and how it is used in networking.**

**HTTP** (HyperText Transfer Protocol) is used to transfer web pages over the internet. It enables browsers to request and receive data (like HTML, images) from web servers.

### **5. Explain HTTPS and how it is different from HTTP.**

**HTTPS** (HyperText Transfer Protocol Secure) is a secure version of HTTP. It encrypts data exchanged between your browser and the web server, protecting sensitive information like passwords from eavesdropping.

### **6. Understand the purpose of FTP and how it operates in network communication.**

**FTP** (File Transfer Protocol) is used to transfer files between computers over a network. It allows users to upload or download files from a server, commonly used for website file management.

### **7. Define TCP and UDP communication and differentiate between them.**

- **TCP** (Transmission Control Protocol) is reliable and ensures data is delivered in the correct order. It is slower due to error-checking.
- **UDP** (User Datagram Protocol) is faster but less reliable. It does not guarantee the order or delivery of data.

### **8. Identify the OSI model layer where TCP and UDP operate.**

Both **TCP** and **UDP** operate on **Layer 4** (Transport Layer) in the OSI model.

### **9. Define a port in networking and its function.**

A **port** is a number that identifies a specific service or process on a device, helping to direct network traffic to the correct application (e.g., HTTP typically uses port 80).

### **10. Identify the port and OSI model layer for each protocol used.**

| Protocol  | Port Number                                    | OSI Layer                   |
| --------- | ---------------------------------------------- | --------------------------- |
| **HTTP**  | 80                                             | Layer 7 (Application Layer) |
| **HTTPS** | 443                                            | Layer 7 (Application Layer) |
| **FTP**   | 21                                             | Layer 7 (Application Layer) |
| **TCP**   | Varies (Used by many protocols like HTTP, FTP) | Layer 4 (Transport Layer)   |
| **UDP**   | Varies (Used by protocols like DNS, DHCP)      | Layer 4 (Transport Layer)   |

### **11. Understand the different types of DNS records.**

- **A record**: Maps a domain name to an IPv4 address.
- **AAAA record**: Maps a domain name to an IPv6 address.
- **CNAME record**: Maps an alias to a canonical domain name.
- **MX record**: Specifies mail servers for the domain.
- **NS record**: Specifies authoritative name servers for the domain.
- **PTR record**: Used for reverse DNS lookups.
- **TXT record**: Allows the domain to store text data (e.g., SPF records for email security).

---

## **Exercise 4**

![picture](/deep-in-net/ex04.png)

### **1. What is a router and what is its role?**

A **router** is a device that connects different networks and directs data packets between them. It ensures that data reaches its correct destination, even when devices are on different subnets or networks.

### **2. Differentiate between the switch and the router.**

| Feature              | Switch                                        | Router                                           |
| -------------------- | --------------------------------------------- | ------------------------------------------------ |
| **Primary Function** | Connects devices within the same network      | Connects different networks or subnets           |
| **Data Handling**    | Forwards data based on MAC addresses          | Forwards data based on IP addresses              |
| **Network Type**     | Operates in a single local area network (LAN) | Operates between different networks (LANs, WANs) |
| **Layer**            | Operates on Layer 2 (Data Link Layer)         | Operates on Layer 3 (Network Layer)              |

### **3. Identify the OSI model layer where a router operates.**

A **router** operates on **Layer 3** (Network Layer) of the OSI model. It uses **IP addresses** to forward data packets.

### **4. Understand the term "default gateway".**

A **default gateway** is the router's IP address that allows devices in a network to communicate with devices outside their local network. It acts as the intermediary for sending data to remote networks.

---

## **Exercise 5**

![picture](/deep-in-net/ex05.png)

---

## **Exercise 6**

![picture](/deep-in-net/ex06.png)

### **What is a routing table and explain its role in routing network traffic?**

A **routing table** is a list used by routers to determine the best path for forwarding data packets. It helps routers know where to send data to reach its destination.

When a router receives a packet, it looks up the destination IP address in the routing table and forwards the packet to the next hop (another router or device) until it reaches its final destination.

---

## **Exercise 7**

![picture](/deep-in-net/ex07.png)

---

## **Exercise 8**

![picture](/deep-in-net/ex08.png)
