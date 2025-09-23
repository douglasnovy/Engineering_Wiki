---
title: Communication_Protocols
consolidated: true
sources: 3
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md']  # This would be a timestamp
---

## Title
Secure Communication and Alarm Configuration for StackVision and 8864 DAS Systems

---

## Overview
This knowledge base entry consolidates engineering standards and procedures for configuring secure communications between StackVision servers and 8864 Data Acquisition Systems (DAS), as well as implementing communication alarms to ensure system reliability. Secure communication is critical for protecting data integrity and preventing unauthorized access, while communication alarms provide operational assurance by detecting and alerting on connectivity or service failures.

---

## Key Concepts

### StackVision and 8864 DAS
- **StackVision**: An environmental data acquisition and reporting platform.
- **8864 DAS**: A data acquisition system used for environmental monitoring, capable of interfacing with StackVision for data transfer and control.

### Secure Communications
- **SSH Reverse Tunneling**: A method where the 8864 initiates a secure outbound connection to the StackVision server, avoiding the need for inbound firewall rules.
- **Public/Private Key Authentication**: Uses RSA-2048 keys to authenticate both ends of the connection.
- **Encryption and Signing**: Data is encrypted with AES-128, signed using HMAC-SHA256, and secured with Diffie-Hellman key exchange.

### Communication Alarms
- **Purpose**: Detects failures in communication between the 8864 DAS and StackVision, including core service outages.
- **Implementation**: Can be configured entirely within StackStudio, using an 8864 counter channel, or via Windows Task Scheduler scripts.

---

## Technical Details

### Secure Communication Configuration (Firmware v5.02+)
1. **SSH Reverse Tunnel Setup**:
   - On boot, the 8864 establishes a reverse SSH tunnel to the StackVision server.
   - This tunnel acts as a port-specific VPN, allowing secure data transfer.
   - Only outbound connections are required through the firewall.

2. **Key Management**:
   - Generate RSA-2048 public/private key pairs for each 8864 and the StackVision server.
   - Install the 8864’s public key on the StackVision server’s SSH configuration.
   - Install the StackVision server’s public key on each 8864.
   - Keys can be distributed via unsecured channels, but installation must be strictly controlled to prevent unauthorized access.

3. **Encryption and Authentication**:
   - AES-128 encryption for data confidentiality.
   - HMAC-SHA256 for message integrity.
   - RSA-2048 for authentication.
   - Diffie-Hellman key exchange for secure session key negotiation.

4. **Firewall Considerations**:
   - No inbound ports need to be opened for the 8864 connection.
   - Any unused ports (e.g., for Modbus) can be closed to reduce attack surface.

---

### Communication Alarm Configuration
1. **StackStudio Implementation**:
   - Configure an 8864 counter channel to monitor communication status.
   - Alarms trigger when polling detects failures or when StackVision core services stop.

2. **Windows Task Scheduler Method**:
   - Scripts can periodically check communication status and raise alarms.
   - This method is more flexible but requires external scheduling.

3. **Advantages of StackStudio Method**:
   - Fully integrated within the StackVision/8864 environment.
   - No reliance on external tools.
   - Can detect both network and service-level failures.

---

## Best Practices

1. **Secure Communication**:
   - Always use the latest firmware supporting SSH reverse tunneling.
   - Maintain strict control over key installation and storage.
   - Regularly audit keys to ensure no rogue devices are connected.
   - Close unused ports to minimize security risks.

2. **Alarm Configuration**:
   - Prefer integrated StackStudio alarms for simplicity and reliability.
   - Test alarm triggers regularly to ensure they detect both network and service outages.
   - Document alarm configurations for maintenance and troubleshooting.

3. **Operational Monitoring**:
   - Combine secure communication with robust alarm systems to ensure continuous data integrity and availability.
   - Implement periodic reviews of both communication security and alarm functionality.

---

## Source Attribution

- **[Document 1]**: Provided details on implementing the 8864 DAS Communication Alarm using StackStudio and Windows Task Scheduler, including the use of an 8864 counter channel and integration benefits.
- **[Document 2]**: Detailed the secure communication setup between StackVision and the 8864 using SSH reverse tunneling, RSA key authentication, and firewall considerations for firmware v5.02+.
- **[Document 3]**: Supplemented encryption and authentication specifications (AES-128, HMAC-SHA256, RSA-2048, Diffie-Hellman) and clarified network port requirements for secure StackVision connections.

---

If you’d like, I can also create a **diagram showing the secure communication flow and alarm monitoring architecture** for StackVision and 8864 DAS. This would make the relationships between components clearer. Would you like me to prepare that?

## Glossary

- **8864**: Data controller platform used by engineering
- **MODBUS**: Serial communications protocol for industrial automation
