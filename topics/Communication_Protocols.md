---
title: Communication_Protocols
consolidated: true
sources: 3
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md']  # This would be a timestamp
---

## Title
Secure Communication and Alarm Management for 8864 DAS and StackVision Systems

---

## Overview
The 8864 Data Acquisition System (DAS) and StackVision software are critical components in environmental monitoring and compliance reporting. Ensuring secure, reliable communication between these systems is essential for data integrity, regulatory compliance, and operational continuity. This consolidated guide covers secure communication setup, network port considerations, and alarm configurations for detecting communication failures between the 8864 and StackVision.

---

## Key Concepts

### 8864 DAS
A hardware device used for environmental data acquisition, often integrated with StackVision for data processing, visualization, and reporting.

### StackVision
A software platform for managing environmental data, providing tools for data acquisition, analysis, and compliance reporting.

### Secure Communications
A method of encrypting and authenticating data transfer between the 8864 and StackVision to prevent unauthorized access and ensure data integrity.

### Communication Alarms
Automated alerts triggered when communication between the 8864 and StackVision fails, enabling rapid response to potential data loss or system downtime.

---

## Technical Details

### Secure Communication Implementation
Beginning with firmware version 5.02, the 8864 supports secure communications via **SSH reverse tunneling**:
- **Connection Direction**: Initiated from the 8864 to the StackVision server, eliminating the need for inbound firewall rules.
- **Authentication**: Uses 2048-bit RSA public/private key pairs.
  - Public key of each 8864 must be installed on the StackVision server’s SSH service.
  - Public key of the StackVision server must be installed on each 8864.
- **Encryption & Signing**:
  - AES-128 encryption
  - HMAC-SHA256 message signing
  - Diffie-Hellman key exchange for session keys
- **Security Note**: Public keys can be transmitted over insecure channels, but installation must be strictly controlled to prevent unauthorized devices from connecting.

### Network Port Considerations
From the 2016 secure communication port specifications:
- **No inbound firewall penetration required** for 8864-to-StackVision communication.
- Modbus connections:
  - DCS or Instrument (Modbus Client) → StackVision Client: No inbound ports.
  - DCS or Instrument (Modbus Server) → Instrument inbound port: Can be closed if unused.
- All communications are encrypted and authenticated as described above.

### Communication Alarm Configuration
An engineering standard exists for configuring alarms to detect communication failures:
- Historically implemented via **Windows Task Scheduler** scripts.
- Recommended approach uses **StackVision polling alarms** configured entirely within **StackStudio**.
- Benefits:
  - Detects failures even if StackVision core services stop.
  - Uses an **8864 counter channel** for monitoring.
- Future goal: Integrate alarm functionality directly into 8864 firmware.

---

## Best Practices

1. **Secure Key Management**
   - Maintain strict control over public key installation.
   - Regularly audit keys on both the 8864 and StackVision server.

2. **Firewall Configuration**
   - Leverage outbound-only connections from the 8864 to minimize attack surface.
   - Close unused ports, especially Modbus server ports, when not required.

3. **Alarm Setup**
   - Use StackVision’s internal polling alarms for robust detection.
   - Configure alarms to monitor both communication status and core service health.

4. **Firmware Updates**
   - Keep 8864 firmware updated to benefit from the latest secure communication features.
   - Plan for future firmware releases that may integrate alarm functionality.

5. **Testing & Validation**
   - Test secure communication setup in a controlled environment before deployment.
   - Simulate communication failures to verify alarm functionality.

---

## Source Attribution

- **Document 1 (Engineering Standard - 8864 DAS Communication Alarm)**: Provided details on communication alarm configuration using StackVision polling alarms, benefits over Windows Task Scheduler, and use of an 8864 counter channel.
- **Document 2 (Setting up Secure Communications r4)**: Explained the SSH reverse tunneling method, RSA key authentication process, and firewall considerations for secure communication between 8864 and StackVision.
- **Document 3 (ESC Secure Communication Ports)**: Outlined network port usage, encryption and authentication methods, and confirmed no inbound firewall penetration is required for secure communications.

---

If you’d like, I can also create a **diagram showing the secure communication flow and alarm monitoring architecture** to make this knowledge base entry more visual and easier to understand. Would you like me to add that?

## Glossary

- **8864**: Data controller platform used by engineering
- **MODBUS**: Serial communications protocol for industrial automation
