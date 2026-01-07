# **University Multi-Campus Network Design**

**Course:** CSC-203L: Computer Networks Lab

**Institution:** University of Engineering and Technology (UET), Lahore

**Date:** January 8, 2026

## **📌 Project Overview**

This project involves the design and implementation of a robust, scalable university network connecting a **Main Campus** and two sub-campuses (**Kala Shah Kaku** and **RCET**).

The simulation is built using **Cisco Packet Tracer** and ensures high availability, redundancy, and security. The network follows a hierarchical star topology, utilizing Layer 3 switches for inter-VLAN routing and border routers for inter-campus communication.

## **🚀 Key Features**

* **Multi-Campus Architecture:** Connects three distinct campuses via a core layer ISP cloud/backbone.  
* **VLAN Implementation:** Traffic segregation for three distinct departments:  
  * Computer Science (VLAN 10\)  
  * Electrical Engineering (VLAN 20\)  
  * Administration (VLAN 30\)  
* **Routing:** Inter-campus connectivity using **Static Routing** to prevent single points of failure.  
* **Network Services:** \* **HTTP:** University portal accessible to all VLANs.  
  * **DNS:** Resolves URLs (e.g., www.uet.edu.pk) to web server IPs.  
  * **Email:** SMTP/POP3 services for internal communication.  
  * **FTP:** Secure file storage restricted to specific users.  
* **Security:** Implementation of **Access Control Lists (ACLs)** to restrict unauthorized access between specific sub-campuses and servers.

## **🛠️ Network Topology & Hardware**

### **Architecture**

The network uses a **Hierarchical Star Topology**:

* **Core Layer:** Inter-campus connection via ISP.  
* **Distribution Layer:** Border routers and Layer 3 switches.  
* **Access Layer:** Layer 2 switches connecting end devices.

### **Hardware Requirements**

| Device | Model | Quantity | Role |
| :---- | :---- | :---- | :---- |
| **Routers** | Cisco 2911 | 14 | Border & Campus Routing |
| **L3 Switches** | Cisco 3560 | 3 | Server Room & Inter-VLAN |
| **Access Switches** | Cisco 2960 | 33 | End Device Connectivity |
| **Servers** | Generic PT | 24 | DNS, Web, Email, FTP |
| **End Devices** | PCs | 90 | 10 per department |

## **💻 IP Addressing Scheme (VLSM)**

The network utilizes the private IP block 192.168.0.0 subdivided using VLSM.

### **1\. Main Campus**

| Department | VLAN ID | Network Address | Gateway |
| :---- | :---- | :---- | :---- |
| Computer Science | 10 | 192.168.1.0/24 | 192.168.1.1 |
| Electrical Eng. | 20 | 192.168.2.0/24 | 192.168.2.1 |
| Administration | 30 | 192.168.3.0/24 | 192.168.3.1 |

### **2\. Kala Shah Kaku Campus**

| Department | VLAN ID | Network Address | Gateway |
| :---- | :---- | :---- | :---- |
| Computer Science | 10 | 192.168.10.0/24 | 192.168.10.1 |
| Electrical Eng. | 20 | 192.168.20.0/24 | 192.168.20.1 |
| Administration | 30 | 192.168.30.0/24 | 192.168.30.1 |

### **3\. RCET Campus**

| Department | VLAN ID | Network Address | Gateway |
| :---- | :---- | :---- | :---- |
| Computer Science | 10 | 192.168.60.0/24 | 192.168.60.1 |
| Electrical Eng. | 20 | 192.168.70.0/24 | 192.168.70.1 |
| Administration | 30 | 192.168.80.0/24 | 192.168.80.1 |

## **🔒 Security Configuration (ACL)**

An Access Control List (ACL) was implemented to prevent the **Admin department (Sub-Campus 3\)** from accessing the **Web Server in CS (Sub-Campus 1\)**.

access-list 100 deny tcp 192.168.4.128 0.0.0.63 host 192.168.2.10 eq 80  
access-list 100 permit ip any any

interface GigabitEthernet0/0  
ip access-group 100 in

## **🧪 Testing & Validation**

The network passed the following validation tests:

1. **Inter-Campus Connectivity:** Successful Ping from CS Dept (Campus 1\) to EE Dept (Campus 2).  
2. **Web Server Access:** Browser successfully loads www.uet.edu.pk (or www.ee.main.edu).  
3. **Secure FTP:** Confirmed "Request Timed Out" when unauthorized Admins attempted to access FTP.  
4. **Traceroute:** Verified correct routing paths (max 30 hops) between campuses.

## **👥 Contributors**

**Submitted By:**

* **Muhammad Arslan** (2024-CS-632)  
* **Afaaq Anwar** (2024-CS-603)

* **Ahsan Shakeel** (2024-CS-638)

**Submitted To:** Ms. Ghazala

*This project was created for educational purposes as part of the Open-Ended Lab (OEL) at UET Lahore.*
