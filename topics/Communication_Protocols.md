---
title: Communication_Protocols
consolidated: true
sources: 3
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md']  # This would be a timestamp
---

## Title
Secure Communication and Alarm Management for 8864 DAS and StackVision Systems

---

## Overview
This document consolidates engineering standards and procedures for implementing secure communications between the 8864 Data Acquisition System (DAS) and StackVision, as well as configuring communication alarms to ensure system reliability.  
The 8864 DAS, when integrated with StackVision, supports advanced secure communication protocols and alarm mechanisms that safeguard data integrity, maintain operational continuity, and provide early detection of communication failures.

---

## Key Concepts

### 8864 DAS
A data acquisition system used for environmental monitoring and compliance reporting, often integrated with StackVision for data management and analysis.

### StackVision
A server-based platform for environmental data collection, processing, and reporting. It communicates with the 8864 DAS for real-time and historical data.

### Secure Communications
A method of protecting data exchange between the 8864 DAS and StackVision using encryption, authentication, and tunneling techniques.

### Communication Alarms
Automated alerts triggered when communication between the 8864 DAS and StackVision is interrupted or degraded, enabling timely intervention.

---

## Technical Details

### Secure Communication Implementation
Beginning with firmware version 5.02, the 8864 DAS supports secure communications via **SSH reverse tunneling**:
- **Connection Direction**: Initiated from the 8864 to the StackVision server, eliminating the need for inbound firewall rules.
- **Functionality**: Acts as a port-specific VPN between the devices.
- **Authentication**:  
  - Uses **2048-bit RSA public/private keys**.
  - Public keys of each 8864 must be installed on the StackVision server’s SSH service.
  - The StackVision server’s public key must be installed on each 8864.
- **Encryption & Integrity**:  
  - AES-128 encryption for data confidentiality.
  - HMAC-SHA256 for message integrity.
  - Diffie-Hellman key exchange for session key negotiation.
- **Security Considerations**:  
  - Public keys can be distributed over unsecured channels but must be carefully managed to prevent unauthorized key installation.
  - Only trusted devices should be authenticated.

### Communication Alarm Configuration
The **8864 DAS Communication Alarm** can be implemented to detect failures in data exchange:
- **Implementation Methods**:
  - Historically via **Windows Task Scheduler**.
  - Preferred method: **StackVision polling alarms** configured entirely within StackStudio.
- **Advantages of StackVision Polling**:
  - Detects failures even if StackVision core services stop.
  - Uses an **8864 counter channel** for monitoring.
- **Future Development**:
  - Planned integration of this alarm functionality directly into 8864 firmware.

### Network and Firewall Considerations
- No inbound firewall penetration is required for secure communications.
- All connections are outbound from the 8864 to StackVision.
- Ports for unused services can be closed to reduce attack surface.

---

## Best Practices
1. **Use the Latest Firmware**: Ensure 8864 DAS firmware is at least v5.02 to enable SSH reverse tunneling.
2. **Key Management**:
   - Maintain strict control over key installation.
   - Regularly audit installed keys on both the 8864 and StackVision server.
3. **Alarm Configuration**:
   - Implement communication alarms within StackVision for robust monitoring.
   - Test alarms periodically to confirm functionality.
4. **Firewall Configuration**:
   - Allow only necessary outbound connections from the 8864.
   - Close unused ports to enhance security.
5. **Documentation & Change Control**:
   - Document all configuration changes.
   - Follow engineering standards for alarm and communication setup.

---

## Source Attribution
- **Document 1**: Provided details on the 8864 DAS Communication Alarm standard, including historical implementation via Windows Task Scheduler, advantages of StackVision polling alarms, and use of an 8864 counter channel.
- **Document 2**: Described the secure communication setup between 8864 DAS and StackVision using SSH reverse tunneling, key exchange, and authentication procedures.
- **Document 3**: Outlined network connection requirements, encryption standards (AES-128, HMAC-SHA256, RSA-2048), and firewall considerations for secure communications.

---

If you’d like, I can also create a **step-by-step configuration guide** combining the secure communication setup and alarm configuration into a single operational procedure. This would make it easier for engineers to implement both security and monitoring in one workflow. Would you like me to prepare that?

## Glossary

- **8864**: Data controller platform used by engineering
