<div align="center">

# 🔗 Enabled Multi-VPC Communication using AWS Transit Gateway

### Designing Scalable Enterprise Networking Using Hub-and-Spoke Architecture, Centralized Routing, and Private Cross-VPC Communication

![AWS](https://img.shields.io/badge/AWS-Advanced%20Networking-orange)
![Transit Gateway](https://img.shields.io/badge/Transit-Gateway-purple)
![Amazon VPC](https://img.shields.io/badge/Amazon-VPC-blue)
![EC2](https://img.shields.io/badge/Amazon-EC2-yellow)
![Networking](https://img.shields.io/badge/Enterprise-Networking-green)

</div>

---

# 🌍 Real-World Problem Statement

As organizations grow in the cloud, they rarely operate from a single VPC.

Different teams and workloads are usually deployed in separate networks:

- Production VPC
- Development VPC
- Shared Services VPC
- Security VPC
- Data Analytics VPC

By default, Amazon VPCs are isolated from one another.

This creates a challenge:

> How can multiple VPCs communicate securely without exposing traffic to the public internet?

A common solution is **VPC Peering**.

However, as the number of VPCs increases, VPC Peering becomes difficult to manage.

For example:

```text
3 VPCs  → 3 Peering Connections
5 VPCs  → 10 Peering Connections
10 VPCs → 45 Peering Connections
20 VPCs → 190 Peering Connections
```

This creates:

❌ Complex route table management

❌ Difficult scalability

❌ Increased operational overhead

❌ Lack of centralized traffic control

Large enterprises therefore use **AWS Transit Gateway**, which acts as a centralized routing hub connecting multiple VPCs through a Hub-and-Spoke architecture.

---

# 🎯 Project Objective

The objective of this project was to design and implement a scalable AWS networking architecture using Transit Gateway.

The solution demonstrates:

✅ Multi-VPC Connectivity

✅ Hub-and-Spoke Architecture

✅ Centralized Routing

✅ Dynamic Route Propagation

✅ Private Cross-VPC Communication

✅ Enterprise Networking Best Practices

✅ Transit Gateway Attachments

✅ Route Table Integration

✅ Connectivity Validation Using ICMP

---

# 🏗️ Solution Overview

To solve the limitations of traditional VPC Peering, a centralized Transit Gateway architecture was implemented.

The architecture consists of:

### VPC-A

- CIDR: 10.0.0.0/16
- Public Subnets
- EC2 Instance

### VPC-B

- CIDR: 10.1.0.0/16
- Public Subnets
- EC2 Instance

### AWS Transit Gateway

- Centralized Routing Hub
- Dynamic Route Propagation
- Route Association Enabled
- Hub-and-Spoke Design

Traffic between both VPCs is routed privately through the Transit Gateway.

No internet routing is used for inter-VPC communication.

---

# 🏗️ Architecture Diagram

<p align="center">
    <img src="./architecture/Archyi.png" alt="AWS Transit Gateway Architecture" width="100%">
</p>

---

# 🔄 Architecture Workflow

### Step 1 — Create Two Isolated VPCs

```text
VPC-A → 10.0.0.0/16

VPC-B → 10.1.0.0/16
```

Both VPCs are independent and cannot communicate by default.

---

### Step 2 — Deploy Transit Gateway

```text
AWS Transit Gateway

ASN: 64512

Route Association: Enabled

Route Propagation: Enabled
```

Transit Gateway becomes the central routing hub.

---

### Step 3 — Create Transit Gateway Attachments

```text
VPC-A
     │
     ▼
Transit Gateway Attachment

VPC-B
     │
     ▼
Transit Gateway Attachment
```

Both VPCs are attached to the Transit Gateway.

---

### Step 4 — Configure Route Tables

VPC-A Route Table:

```text
10.1.0.0/16 → Transit Gateway
```

VPC-B Route Table:

```text
10.0.0.0/16 → Transit Gateway
```

Transit Gateway Route Table:

```text
10.0.0.0/16 → VPC-A Attachment

10.1.0.0/16 → VPC-B Attachment
```

---

### Step 5 — Validate Connectivity

Connectivity was tested using ICMP.

```bash
ping 10.1.1.144
```

Result:

```text
64 bytes from 10.1.1.144
icmp_seq=1 ttl=127 time<1ms

64 bytes from 10.1.1.144
icmp_seq=2 ttl=127 time<1ms
```

This confirms successful private communication between VPC-A and VPC-B.

---

# ☁️ AWS Services Used

| Service | Purpose |
|----------|----------|
| Amazon VPC | Isolated Network Environment |
| AWS Transit Gateway | Centralized Routing Hub |
| Amazon EC2 | Connectivity Validation |
| Route Tables | Traffic Routing |
| Internet Gateway | Internet Access |
| Security Groups | Instance-Level Security |
| Network ACLs | Subnet-Level Security |

---

# 📂 Repository Structure

```text
aws-transit-gateway-multi-vpc-networking
│
├── architecture
│
├── implementation-walkthrough
│
├── documentation
│
└── README.md
```

---

# 📚 Project Resources

## 🏗️ Architecture

➡️ [Architecture Documentation](./architecture/README.md)

---

## 📸 Implementation Walkthrough

➡️ [Implementation Walkthrough](./implementation-walkthrough/README.md)

---

## 📄 Complete Project Documentation

➡️ [Documentation README](./documentation/README.md)

➡️ [Open Presentation PDF](./documentation/AWS-Transit-Gateway-Presentation.pdf)

---

# 🔒 Security Controls Implemented

### Security Groups

- SSH Access (Port 22)
- ICMP Allowed
- Controlled Inbound Access

### Network Isolation

- Separate CIDR Blocks
- Independent Route Tables
- Transit Gateway Controlled Routing

### Private Routing

- Inter-VPC Traffic via TGW
- No Internet Routing
- No Public Communication Path

---

# 🧪 Validation Results

| Validation | Status |
|------------|---------|
| Transit Gateway Created | ✅ |
| VPC-A Attachment Created | ✅ |
| VPC-B Attachment Created | ✅ |
| Route Propagation Enabled | ✅ |
| Dynamic Route Learning Verified | ✅ |
| Route Tables Updated | ✅ |
| ICMP Connectivity Tested | ✅ |
| Private Routing Confirmed | ✅ |

---

# 📈 Project Outcomes

✅ Created two isolated VPCs

✅ Implemented AWS Transit Gateway

✅ Configured Transit Gateway Attachments

✅ Enabled Dynamic Route Propagation

✅ Established Private EC2 Communication Across VPCs

✅ Validated Cross-VPC Connectivity

✅ Demonstrated Hub-and-Spoke Architecture

✅ Implemented Enterprise-Scale Networking Pattern

---

# 🏢 Enterprise Benefits

### Hub-and-Spoke Architecture

A single Transit Gateway becomes the central connection point for all VPCs.

### Reduced Complexity

Avoids full-mesh VPC Peering.

### Centralized Routing

One routing hub instead of managing multiple peering paths.

### Dynamic Route Learning

Automatic route propagation reduces administrative effort.

### Scalable Design

Supports thousands of VPC attachments across accounts and regions.

### Production-Ready Foundation

Can be extended to:

- Direct Connect
- Site-to-Site VPN
- Shared Services VPC
- Multi-Account AWS Organizations
- Multi-Region Connectivity

---

# 🚀 Future Enhancements

- Multi-Region Transit Gateway Peering
- Site-to-Site VPN Integration
- AWS Direct Connect
- Shared Services VPC
- AWS Network Firewall
- Transit Gateway Flow Logs
- Multi-Account Networking
- AWS Resource Access Manager (RAM)

---

# 🧠 Key Learnings

- VPCs are isolated by default.
- Transit Gateway simplifies large-scale networking.
- Dynamic route propagation reduces manual configuration.
- Hub-and-Spoke architectures scale better than VPC Peering.
- Private IP communication improves security.
- Centralized routing simplifies operations.
- AWS Transit Gateway is the preferred solution for enterprise multi-VPC networking.

---

# 👨‍💻 Author

## Adhithyan Sivaraman T

AWS Student Builder Group Leader

Cloud & DevOps Enthusiast

Federal Institute of Science and Technology (FISAT)

LinkedIn: www.linkedin.com/in/adhithyan-sivaraman-t-399b5b362

GitHub: https://github.com/Adhithyan-10

---

<div align="center">

### ⭐ Building Scalable Enterprise Networking Architectures on AWS

AWS Transit Gateway • Amazon VPC • Advanced Networking • Cloud Architecture

</div>
