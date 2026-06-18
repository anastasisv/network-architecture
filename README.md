# Enterprise 4-Floor Campus Network Infrastructure

## Overview

This project demonstrates the design and implementation of a secure, scalable, and highly available enterprise campus network using Cisco Packet Tracer.

The network serves a four-floor corporate environment where each department is logically segmented using VLANs and interconnected through Layer 3 switching. High availability is achieved through HSRP gateway redundancy, while dynamic routing is handled by OSPF. Centralized services such as DHCP, HTTP, and Email are hosted in a dedicated server network.

The design follows enterprise networking best practices including VLAN segmentation, port security, trunk hardening, SSH management, redundancy, and dynamic routing.

---

## Network Architecture

The network follows a hierarchical campus model:

### Access Layer

Cisco Catalyst 2960 switches provide connectivity for:

* Workstations
* Printers
* Wireless Access Points
* Mobile Devices

### Distribution Layer

Cisco Catalyst 3560 Layer 3 switches provide:

* Inter-VLAN Routing
* HSRP Gateway Redundancy
* OSPF Routing
* DHCP Relay Services

### Core/WAN Layer

Cisco 2911 Routers provide:

* Inter-floor connectivity
* Redundant routing paths
* OSPF Area 0 participation

### Server Infrastructure

Dedicated server VLAN hosting:

* DHCP Server
* HTTP Server
* Email Server

---

# Department Layout

## Floor 1

| VLAN | Department      | Network         |
| ---- | --------------- | --------------- |
| 10   | Research        | 172.16.0.0/25   |
| 20   | Management      | 172.16.0.128/25 |
| 30   | Human Resources | 172.16.1.0/25   |

---

## Floor 2

| VLAN | Department    | Network         |
| ---- | ------------- | --------------- |
| 40   | Guests        | 172.16.1.128/25 |
| 50   | Customer Care | 172.16.2.0/25   |
| 60   | Logistics     | 172.16.2.128/25 |

---

## Floor 3

| VLAN | Department | Network         |
| ---- | ---------- | --------------- |
| 70   | Accounting | 172.16.3.0/26   |
| 80   | Marketing  | 172.16.3.64/26  |
| 90   | Finance    | 172.16.3.128/26 |

---

## Floor 4

| VLAN | Department     | Network         |
| ---- | -------------- | --------------- |
| 100  | Administration | 172.16.3.192/27 |
| 110  | Server Farm    | 172.16.3.224/27 |

---

# High Availability Design

The network implements Hot Standby Router Protocol (HSRP) to eliminate single points of failure and provide gateway redundancy.

## HSRP Load Balancing

### Distribution Pair 1

Primary Gateway on SL3-FLOOR-1

* VLAN 10 (Research)
* VLAN 20 (Management)
* VLAN 30 (HR)

Primary Gateway on SL3-FLOOR-2

* VLAN 40 (Guests)
* VLAN 50 (Customer Care)
* VLAN 60 (Logistics)

---

### Distribution Pair 2

Primary Gateway on SL3-FLOOR-3

* VLAN 70 (Accounting)
* VLAN 80 (Marketing)
* VLAN 90 (Finance)

Primary Gateway on SL3-FLOOR-4

* VLAN 100 (Administration)
* VLAN 110 (Servers)

This design provides both fault tolerance and gateway load distribution across multiple Layer 3 devices.

---

# Dynamic Routing

## OSPF Area 0

The network uses Open Shortest Path First (OSPF) as the dynamic routing protocol.

### Benefits

* Automatic route propagation
* Fast convergence
* Scalability
* Reduced administrative overhead

### OSPF Functions

* Advertisement of all VLAN networks
* Route exchange between routers and Layer 3 switches
* Redundant path utilization
* Equal-Cost Multi-Path (ECMP) support

---

# DHCP Architecture

A centralized DHCP server is deployed within the Server VLAN.

### DHCP Server

| Service | Address      |
| ------- | ------------ |
| DHCP    | 172.16.3.230 |

### DHCP Relay

All Layer 3 VLAN interfaces use:

ip helper-address 172.16.3.230

This allows centralized IP address management across all departments.

---

# Server Infrastructure

| Service      | Address      |
| ------------ | ------------ |
| DHCP Server  | 172.16.3.230 |
| HTTP Server  | 172.16.3.232 |
| Email Server | 172.16.3.233 |

---

# Security Implementation

The project incorporates multiple security mechanisms commonly found in enterprise networks.

## Port Security

Implemented on access ports:

* Sticky MAC Learning
* Violation Restriction Mode
* Maximum MAC Address Limiting
* Aging Configuration

### Example

switchport port-security
switchport port-security mac-address sticky
switchport port-security violation restrict

---

## Secure Remote Management

Only SSH access is permitted for remote administration.

### Features

* Local User Authentication
* Encrypted Sessions
* Disabled Telnet Access

---

## Trunk Security

All trunk links are manually configured.

### Hardening Features

* DTP Disabled
* Explicit VLAN Allow Lists
* Dedicated Native VLAN

Example:

switchport mode trunk
switchport nonegotiate

---

## Native VLAN Isolation

A dedicated Native VLAN (200) is used for trunk links.

Benefits:

* Reduced VLAN hopping risk
* Improved network segmentation

---

## Black-Hole VLAN

Unused switch ports are:

* Disabled
* Assigned to VLAN 999

Example:

switchport access vlan 999
shutdown

This prevents unauthorized device connections.

---

# Wireless Infrastructure

Each department includes dedicated wireless connectivity through Access Points.

Supported Devices:

* Smartphones
* Laptops
* Mobile Endpoints

Wireless users remain segmented within their respective departmental VLANs.

---

# Redundancy Features

The network contains multiple redundant paths between:

* Routers
* Layer 3 Switches
* Distribution Segments

Benefits:

* Fault tolerance
* Improved uptime
* Traffic resiliency
* Alternative path selection via OSPF

---

# Enterprise Features Implemented

✅ VLAN Segmentation

✅ Inter-VLAN Routing

✅ OSPF Dynamic Routing

✅ HSRP Gateway Redundancy

✅ Centralized DHCP

✅ DHCP Relay

✅ Wireless Integration

✅ SSH Remote Management

✅ Port Security

✅ Native VLAN Isolation

✅ Trunk Hardening

✅ Black-Hole VLAN

✅ Layer 3 Switching

✅ Equal-Cost Multi-Path Routing (ECMP)

✅ Enterprise Hierarchical Design

---

# Skills Demonstrated

This project demonstrates practical experience with:

* Cisco IOS Configuration
* Enterprise Campus Design
* Layer 2 Switching
* Layer 3 Switching
* VLAN Design
* Inter-VLAN Routing
* OSPF Routing
* HSRP Configuration
* DHCP Services
* Network Security
* High Availability Design
* Infrastructure Redundancy
* Wireless Network Integration
* Troubleshooting and Validation

---

# Project Outcome

The final solution delivers a secure, scalable, and highly available enterprise network capable of supporting multiple departments across four floors while maintaining logical separation, centralized services, redundancy, and efficient routing.

This project reflects real-world enterprise networking concepts commonly encountered in CCNA, CCNP Enterprise, and production campus environments.

