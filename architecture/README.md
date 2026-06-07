# AWS Transit Gateway Multi-VPC Networking Architecture

![AWS Transit Gateway Multi-VPC Networking Architecture](./archyi.png)

## Overview

This architecture demonstrates secure and scalable communication between multiple Amazon VPCs using AWS Transit Gateway. Instead of creating complex VPC peering connections, a centralized Transit Gateway acts as a routing hub, enabling efficient hub-and-spoke networking.

The implementation consists of two isolated VPCs connected through a Transit Gateway, allowing EC2 instances in different networks to communicate using private IP addresses while maintaining network isolation and centralized route management.

---

## Architecture Components

### VPC-A
- CIDR Block: `10.0.0.0/16`
- Public Subnet: `10.0.1.0/24`
- EC2 Instance Private IP: `10.0.1.10`
- Internet Gateway attached
- Route Table configured for Transit Gateway communication

### VPC-B
- CIDR Block: `10.1.0.0/16`
- Public Subnet: `10.1.1.0/24`
- EC2 Instance Private IP: `10.1.1.144`
- Internet Gateway attached
- Route Table configured for Transit Gateway communication

### AWS Transit Gateway
- Acts as a centralized routing hub
- Connected to both VPCs through Transit Gateway Attachments
- Enables dynamic route propagation
- Simplifies multi-VPC connectivity management
- Eliminates the need for multiple VPC peering connections

### Security Components
- Security Groups for instance-level traffic control
- Network ACLs for subnet-level protection
- ICMP enabled for connectivity validation
- SSH access enabled for administration
- Private IP communication between VPCs

---

## Traffic Flow

### Cross-VPC Communication Flow

1. EC2 Instance in VPC-A (`10.0.1.10`) initiates communication.
2. Route Table in VPC-A forwards traffic destined for `10.1.0.0/16` to the Transit Gateway.
3. Transit Gateway receives the packet and consults its route table.
4. Transit Gateway forwards traffic to the VPC-B attachment.
5. EC2 Instance in VPC-B (`10.1.1.144`) receives the packet.
6. Response traffic follows the reverse path through the Transit Gateway.

All communication occurs using private IP addresses without traversing the public internet.

---

## Routing Configuration

### VPC-A Route Table

| Destination | Target |
|------------|---------|
| 10.1.0.0/16 | Transit Gateway |
| 0.0.0.0/0 | Internet Gateway |

### VPC-B Route Table

| Destination | Target |
|------------|---------|
| 10.0.0.0/16 | Transit Gateway |
| 0.0.0.0/0 | Internet Gateway |

### Transit Gateway Route Table

| Destination | Target |
|------------|---------|
| 10.0.0.0/16 | VPC-A Attachment |
| 10.1.0.0/16 | VPC-B Attachment |

### Dynamic Routing Features

- Route Propagation Enabled
- Dynamic Route Learning Enabled
- Centralized Route Management
- Simplified Multi-VPC Connectivity

---

## Connectivity Validation

Connectivity was successfully verified using ICMP (ping) between EC2 instances located in different VPCs.

Example validation:

```bash
ping 10.1.1.144
```

Successful responses confirmed:

- Transit Gateway routing is functioning correctly
- Cross-VPC communication is operational
- Private IP connectivity is established
- Security Group and Route Table configurations are correct

---

## Security Controls Implemented

### Security Groups
- Stateful firewall protection
- ICMP allowed for testing
- SSH access enabled on port 22

### Network ACLs
- Stateless subnet-level security
- Additional traffic filtering layer

### Network Isolation
- Separate VPC CIDR ranges
- Controlled routing through Transit Gateway
- Private communication path

---

## Enterprise Benefits

### Hub-and-Spoke Architecture
Provides centralized network connectivity for multiple VPCs.

### Centralized Routing
All VPC communication is managed through a single Transit Gateway.

### Simplified Network Management
Reduces operational complexity compared to VPC peering.

### Scalable Multi-VPC Connectivity
Supports growth from a few VPCs to hundreds of connected networks.

### Reduced Peering Complexity
Avoids the full-mesh peering model required in large environments.

### Reduced Route Table Management
Centralized route propagation minimizes manual routing updates.

### Production-Ready Design
Follows AWS recommended architecture patterns for enterprise networking.

---

## Project Outcomes

- Created two isolated VPCs
- Established private cross-VPC communication
- Configured Transit Gateway attachments
- Implemented cross-VPC routing
- Enabled private communication using Transit Gateway
- Validated connectivity using ICMP
- Demonstrated hub-and-spoke networking architecture
- Implemented dynamic route propagation
- Simplified multi-VPC connectivity management

---

## AWS Services Used

- Amazon VPC
- AWS Transit Gateway
- Amazon EC2
- Route Tables
- Security Groups
- Network ACLs
- Internet Gateway

---

## Future Enhancements

- Multi-Region Transit Gateway Architecture
- Transit Gateway Peering
- Site-to-Site VPN Integration
- AWS Direct Connect Integration
- Shared Services VPC
- AWS Network Firewall Integration
- Centralized Security Inspection
- Multi-Account Connectivity

---

## Conclusion

This project demonstrates how AWS Transit Gateway enables scalable, centralized, and secure communication between multiple VPCs. By implementing a hub-and-spoke architecture with dynamic route propagation, the solution simplifies network management while providing reliable private connectivity across isolated AWS environments.
