# 💻 CLI Commands Used

## Overview

This document contains the Linux and networking commands used to validate connectivity between multiple VPCs connected through AWS Transit Gateway.

The commands were executed on Amazon EC2 instances deployed in separate VPCs to verify successful communication through the Transit Gateway.

---

# 1. Enable ICMP Response

Amazon Linux may ignore ICMP echo requests depending on configuration.

Command:

```bash
sudo sysctl -w net.ipv4.icmp_echo_ignore_all=0
```

Purpose:

- Enable ping responses
- Allow ICMP testing between VPCs

Expected Output:

```text
net.ipv4.icmp_echo_ignore_all = 0
```

---

# 2. Verify Private IP Address

Used to identify the private IP of the EC2 instance.

Command:

```bash
hostname -I
```

Example Output:

```text
10.1.1.144
```

Purpose:

- Obtain private IP address
- Used as destination for connectivity testing

---

# 3. Test Cross-VPC Connectivity

Executed from the EC2 instance located in VPC-A.

Command:

```bash
ping <private-ip-of-vpc-b-instance>
```

Example:

```bash
ping 10.1.1.144
```

Expected Output:

```text
64 bytes from 10.1.1.144
icmp_seq=1 ttl=127 time=1.23 ms
```

Purpose:

- Validate Transit Gateway routing
- Validate Security Group rules
- Validate Route Table configuration
- Confirm successful communication between VPCs

---

# 4. Stop Ping Test

Command:

```bash
Ctrl + C
```

Purpose:

- Stop continuous ping testing

---

# Validation Checklist

Successful ping responses confirm:

✅ Transit Gateway Attachments working

✅ Route Tables configured correctly

✅ Security Groups allow ICMP

✅ VPC-to-VPC communication established

✅ Hub-and-Spoke architecture functioning correctly

---

# Networking Concepts Demonstrated

- AWS Transit Gateway
- Multi-VPC Communication
- Route Propagation
- Security Groups
- ICMP Connectivity Testing
- Private Network Communication
- Hub-and-Spoke Network Architecture

---

# Outcome

The CLI commands successfully validated private communication between EC2 instances located in different VPCs connected through AWS Transit Gateway.
