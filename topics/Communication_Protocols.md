---
title: Communication_Protocols
consolidated: true
sources: 3
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md']  # This would be a timestamp
---

## Title
Secure Communication and Alarm Standards for StackVision and 8864 DAS Systems

---

## Overview
This consolidated entry outlines the standards, configurations, and best practices for implementing secure communications between StackVision servers and 8864 Data Acquisition Systems (DAS), as well as establishing reliable communication alarms to monitor system health. These measures are critical for ensuring data integrity, operational continuity, and proactive fault detection in environmental monitoring and industrial control systems.

---

## Key Concepts

### StackVision and 8864 DAS
- **StackVision**: A data acquisition and reporting software platform used in emissions monitoring and industrial process control.
- **8864 DAS**: A hardware device that collects and transmits environmental and process data to StackVision.

### Secure Communications
- **Reverse SSH Tunneling**: A secure method where the 8864 initiates an outbound connection to the StackVision server, creating a port-specific VPN-like tunnel.
- **Public/Private Key Authentication**: Uses RSA-2048 keys to authenticate both the 8864 and the StackVision server.
- **Encryption and Signing**: Data is encrypted with AES-128, signed using HMAC-SHA256, and secured via Diffie-Hellman key exchange.

### Communication Alarms
- **DAS Communication Alarm**: A monitoring mechanism that triggers alerts when communication between the 8864 and StackVision fails or when core services stop.
- **Polling Alarms**: StackVision can poll the 8864 to verify connectivity and trigger alarms if responses are not received.

---

## Technical Details

### Secure Communication Setup (Firmware v5.02+)
1. **Initiation**: On boot, the 8864 establishes a reverse SSH tunnel to the StackVision server.
2. **Firewall Considerations**: Only outbound connections are required; no inbound ports need to be opened.
3. **Key Installation**:
   - Install the 8864’s public key on the StackVision server’s SSH configuration.
   - Install the StackVision server’s public key on each 8864.
4. **Authentication**:
   - RSA-2048 public/private key pairs ensure mutual authentication.
   - Keys can be distributed over unsecured channels but must be monitored to prevent unauthorized installations.
5. **Encryption**:
   - AES-128 encryption for data confidentiality.
   - HMAC-SHA256 for message integrity.
   - Diffie-Hellman key exchange for secure session key negotiation.

### Communication Alarm Configuration
- **Implementation Methods**:
  - **Windows Task Scheduler**: Historically used to run scripts or checks.
  - **StackVision Polling**: Preferred method that integrates directly into StackStudio, allowing alarms to trigger if StackVision core services fail.
- **8864 Counter Channel**: Updated configurations use a counter channel within the 8864 for monitoring.
- **Future Integration**: Plans to embed alarm functionality directly into 8864 firmware.

---

## Best Practices

1. **Secure Key Management**:
   - Maintain strict control over key installation.
   - Regularly audit installed keys on both the 8864 and StackVision server.
2. **Firewall Configuration**:
   - Allow outbound connections from the 8864 to the StackVision server.
   - Avoid opening unnecessary inbound ports.
3. **Alarm Reliability**:
   - Use StackVision’s integrated polling alarms for more comprehensive monitoring.
   - Configure alarms to detect both communication failures and service outages.
4. **Firmware Updates**:
   - Keep 8864 firmware updated to leverage built-in secure communication features.
5. **Documentation and Testing**:
   - Document all configurations and changes.
   - Test secure communication and alarm systems regularly to ensure operational readiness.

---

## Source Attribution

- **Document 1**: Provided details on DAS communication alarm configurations, historical use of Windows Task Scheduler, integration into StackVision polling, and use of 8864 counter channels. Highlighted plans for future firmware integration.
- **Document 2**: Explained the secure communication setup between StackVision and the 8864 using reverse SSH tunneling, RSA-2048 key authentication, and firewall considerations. Detailed key installation procedures and security implications.
- **Document 3**: Supplemented encryption and authentication details, specifying AES-128 encryption, HMAC-SHA256 signing, RSA-2048 authentication, and Diffie-Hellman key exchange. Clarified that no inbound firewall penetration is required.

---

If you’d like, I can also create a **diagram showing the secure communication flow and alarm triggering process** to make this knowledge base entry more visual and easier to understand. Would you like me to add that?

## Glossary

- **8864**: Data controller platform used by engineering
