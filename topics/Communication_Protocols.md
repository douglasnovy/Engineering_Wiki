---
title: Communication_Protocols
consolidated: true
sources: 3
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md']  # This would be a timestamp
---

## Title
**Secure Communication and Alarm Integration for StackVision and 8864 DAS Systems**

---

## Overview
This consolidated entry provides guidance on configuring secure communications between StackVision servers and 8864 Data Acquisition Systems (DAS), as well as implementing communication alarms to ensure system reliability. Secure communication is critical for protecting data integrity and confidentiality, while communication alarms provide early detection of failures in data transfer or system services. Together, these measures enhance operational resilience, security, and compliance in environmental monitoring and industrial control systems.

---

## Key Concepts

### StackVision
StackVision is a data acquisition and reporting platform used in environmental compliance monitoring. It interfaces with field instruments such as the 8864 DAS to collect, process, and store emissions and operational data.

### 8864 DAS
The 8864 DAS is a hardware device used for data acquisition from environmental monitoring instruments. It supports secure communication protocols and can be integrated with StackVision for automated data transfer.

### Secure Communications
Secure communications ensure that data exchanged between the 8864 DAS and StackVision is encrypted, authenticated, and protected from unauthorized access. This is achieved using SSH reverse tunneling and cryptographic key exchange.

### Communication Alarms
Communication alarms detect and alert operators when data transfer between the DAS and StackVision fails, or when core services stop functioning. These alarms can be configured to run entirely within StackStudio or via external scheduling tools.

---

## Technical Details

### Secure Communication Implementation
Beginning with firmware version **v5.02**, the 8864 DAS supports secure communications via **SSH reverse tunneling**:
- **Connection Direction**: Initiated from the 8864 DAS to the StackVision server (outbound only), eliminating the need to open inbound firewall ports.
- **Encryption & Authentication**:
  - **RSA-2048** public/private key authentication
  - **AES-128** encryption
  - **HMAC-SHA256** message signing
  - **Diffie-Hellman** key exchange
- **Key Management**:
  - Public keys for each 8864 must be installed on the StackVision server’s SSH service.
  - The StackVision server’s public key must be installed on each 8864 DAS.
  - Keys can be distributed over unsecured channels but must be monitored to prevent unauthorized installations.

### Network Port Requirements
- **StackVision Server**: No inbound ports required for DAS connections.
- **Modbus Communication**:
  - Modbus client connections from DCS or instruments do not require inbound firewall penetration.
  - Modbus server connections require instrument inbound ports but can be closed if unused.

### Communication Alarm Configuration
- **Purpose**: Detects communication failures between StackVision and the 8864 DAS, including cases where StackVision core services stop.
- **Implementation Options**:
  - **Windows Task Scheduler**: Commonly used in past implementations.
  - **StackStudio Configuration**: Fully integrated approach using an 8864 counter channel for monitoring.
- **Advantages of StackStudio Approach**:
  - Operates entirely within the StackVision ecosystem.
  - Provides alarms even if core services fail.
  - Updated configuration supports the 8864 counter channel.
- **Future Development**: Planned integration of alarm functionality directly into 8864 firmware.

---

## Best Practices

1. **Use Outbound-Only Connections**  
   Configure the 8864 DAS to initiate connections to StackVision to minimize firewall exposure.

2. **Enforce Strong Key Management**  
   Maintain strict control over public key installation and monitor for unauthorized changes.

3. **Enable Communication Alarms**  
   Implement alarms within StackStudio for seamless integration and enhanced reliability.

4. **Regularly Test Secure Connections**  
   Verify SSH tunnel integrity and encryption settings during routine maintenance.

5. **Close Unused Ports**  
   Disable unused Modbus or other communication ports to reduce attack surface.

6. **Plan for Firmware Updates**  
   Stay current with 8864 firmware releases to leverage built-in secure communication and alarm features.

---

## Source Attribution

- **Document 1**: Provided details on communication alarm configuration using StackStudio and Windows Task Scheduler, advantages of integrated alarm monitoring, and future firmware integration plans. *(Brian Perlov, PE)*
- **Document 2**: Explained secure communication setup between StackVision and 8864 DAS using SSH reverse tunneling, RSA key authentication, and firewall considerations. *(Mark Shell)*
- **Document 3**: Outlined network port requirements, encryption standards (AES-128, HMAC-SHA256), and authentication protocols (RSA-2048, Diffie-Hellman) for StackVision secure communications.

---

If you’d like, I can create a **step-by-step configuration guide** that combines the secure communication setup with the alarm integration process so operators can deploy both measures in a single workflow. Would you like me to prepare that?

## Glossary

- **8864**: Data controller platform used by engineering
- **MODBUS**: Serial communications protocol for industrial automation
