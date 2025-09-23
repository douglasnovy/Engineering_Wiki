---
title: Communication_Protocols
consolidated: true
sources: 3
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md']  # This would be a timestamp
---

## Title
Secure Communication and Alarm Standards for StackVision–8864 Integration

---

## Overview
This knowledge base entry consolidates engineering standards and procedures for implementing secure communications between StackVision servers and 8864 Data Acquisition Systems (DAS), along with best practices for configuring communication alarms. These measures ensure reliable data transfer, robust security, and timely detection of communication failures, which are critical for maintaining compliance, operational continuity, and system integrity.

---

## Key Concepts

### StackVision–8864 Communication
- **StackVision**: An environmental data acquisition and reporting system.
- **8864 DAS**: A data acquisition device used for environmental monitoring, capable of secure communication and alarm integration.
- **Communication Alarm**: A system alert triggered when data transfer between StackVision and the 8864 DAS fails or when core services stop functioning.
- **Secure Communication**: Encrypted and authenticated data exchange between devices to prevent unauthorized access or tampering.

### Secure Communication Principles
- **SSH Reverse Tunneling**: A secure connection initiated by the 8864 to the StackVision server, functioning like a port-specific VPN.
- **Public/Private Key Authentication**: RSA-2048 keys used to verify device and server identities.
- **Encryption & Signing**: AES-128 encryption for data confidentiality and HMAC-SHA256 for message integrity.
- **Key Exchange**: Diffie-Hellman protocol for secure session key negotiation.

---

## Technical Details

### Communication Alarm Configuration
- **Implementation Methods**:
  - Historically implemented via **Windows Task Scheduler** scripts.
  - Enhanced approach uses **StackVision polling alarms** configured entirely within **StackStudio**.
- **Advantages of StackStudio Configuration**:
  - Detects failures in StackVision core services.
  - Utilizes an **8864 counter channel** for monitoring.
- **Future Development**:
  - Planned integration of alarm functionality directly into 8864 firmware.

### Secure Communication Setup (Firmware v5.02+)
1. **Connection Initiation**:
   - On boot, the 8864 establishes a reverse SSH tunnel to the StackVision server.
   - Outbound-only connection—no inbound firewall ports need to be opened.
2. **Key Installation**:
   - Install the 8864’s public key on the StackVision server’s SSH service.
   - Install the StackVision server’s public key on the 8864.
   - Keys can be distributed via unsecured channels but must be monitored to prevent rogue installations.
3. **Authentication & Encryption**:
   - RSA-2048 keys for authentication.
   - AES-128 encryption for data confidentiality.
   - HMAC-SHA256 for message integrity.
   - Diffie-Hellman for secure key exchange.

### Network Port Considerations
- **StackVision Server**:
  - No inbound ports required for client connections.
  - Modbus communication with DCS or instruments may require specific ports if acting as a Modbus server.
- **Firewall**:
  - Outbound-only connections from 8864 to StackVision server.
  - No inbound penetration required for secure communications.

---

## Best Practices

1. **Alarm Configuration**:
   - Prefer StackStudio-based alarm setups over external schedulers for integrated monitoring.
   - Use polling alarms to detect both communication failures and service stoppages.
   - Assign alarms to dedicated 8864 counter channels for clarity.

2. **Secure Communication Management**:
   - Maintain strict control over public key installation to prevent unauthorized access.
   - Regularly audit installed keys on both server and devices.
   - Use firmware v5.02 or later to leverage SSH reverse tunneling.
   - Ensure encryption and authentication settings meet compliance requirements.

3. **Firewall & Network Security**:
   - Configure firewalls to allow outbound connections from 8864 devices.
   - Close unused ports to reduce attack surface.
   - Monitor network traffic for anomalies.

---

## Source Attribution

- **Document 1**: Provided details on communication alarm implementation, advantages of StackStudio configuration, and planned firmware integration for alarms.
- **Document 2**: Explained secure communication setup between StackVision and 8864 using SSH reverse tunneling, RSA key authentication, and firewall considerations.
- **Document 3**: Outlined network port requirements, encryption standards (AES-128, HMAC-SHA256), and authentication methods (RSA-2048, Diffie-Hellman) for StackVision secure communications.

---

If you’d like, I can also create a **diagram showing the secure communication flow and alarm monitoring architecture** to visually tie these concepts together. Would you like me to prepare that?

## Glossary

- **8864**: Data controller platform used by engineering
- **MODBUS**: Serial communications protocol for industrial automation
