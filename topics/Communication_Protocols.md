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
The 8864 Data Acquisition System (DAS) and StackVision platform are critical components in environmental monitoring and compliance reporting. Reliable communication between these systems is essential for accurate data collection, alarm handling, and regulatory compliance. This document consolidates engineering standards and procedures for:

- Establishing secure communications between the 8864 DAS and StackVision.
- Configuring communication alarms to detect and respond to connectivity or service failures.
- Understanding network port requirements and encryption protocols.

---

## Key Concepts

### 8864 DAS
A data acquisition system used for environmental monitoring, capable of interfacing with StackVision for data collection, analysis, and reporting.

### StackVision
A server-based environmental data management system that communicates with field devices such as the 8864 DAS.

### Secure Communication
A method of ensuring that data transmitted between the 8864 and StackVision is encrypted, authenticated, and protected from unauthorized access.

### Communication Alarms
Automated alerts triggered when communication between the 8864 and StackVision is interrupted or when core services fail.

---

## Technical Details

### Secure Communications (SSH Reverse Tunneling)
- **Firmware Requirement:** Available from 8864 firmware v5.02.
- **Mechanism:** On boot, the 8864 initiates and maintains a reverse SSH tunnel to the StackVision server.
- **Firewall Considerations:** No inbound firewall ports need to be opened; the connection is outbound-only from the 8864.
- **Authentication:** Uses 2048-bit RSA public/private key pairs.
  - **Key Exchange:** Public keys are manually installed on both the 8864 and StackVision server.
  - **Security Note:** Public keys can be distributed over unsecured channels, but installation must be tightly controlled to prevent rogue device access.
- **Encryption & Integrity:**
  - AES-128 encryption
  - HMAC-SHA256 message signing
  - Diffie-Hellman key exchange for session keys

### Network Port Requirements
- **StackVision Server Inbound Ports:** None required for 8864 connections via reverse SSH tunnel.
- **DCS/Instrument Modbus Communication:** May require inbound ports if acting as a Modbus server.
- **Security:** All communications are encrypted and authenticated as above.

### Communication Alarm Configuration
- **Purpose:** Detects loss of communication between 8864 and StackVision, including failures of StackVision core services.
- **Implementation Approaches:**
  - **Windows Task Scheduler:** Historically used for monitoring and triggering alarms.
  - **StackVision Polling Alarms:** Preferred method; configured entirely within StackStudio.
    - Uses an 8864 counter channel to monitor communication status.
    - Provides alarms even if StackVision services stop.
- **Future Development:** Integration of communication alarm functionality directly into 8864 firmware is planned.

---

## Best Practices

1. **Use StackVision Polling Alarms** rather than external schedulers for more reliable detection of both network and service failures.
2. **Implement Secure Communications** via SSH reverse tunneling for all 8864–StackVision connections to eliminate inbound firewall exposure.
3. **Control Key Installation** by restricting access to personnel authorized to manage RSA public keys.
4. **Monitor Communication Channels** regularly and test alarm triggers to ensure timely detection of outages.
5. **Document Network Configurations** including port usage, firewall rules, and key management procedures for audit and troubleshooting purposes.
6. **Plan for Firmware Updates** to leverage built-in alarm features when available.

---

## Source Attribution

- **Document 1 (Engineering Standard - 8864 DAS Communication Alarm):**
  - Provided details on communication alarm configuration using StackVision polling alarms and 8864 counter channels.
  - Highlighted benefits over Windows Task Scheduler and noted future firmware integration.

- **Document 2 (Setting up Secure Communications r4):**
  - Described secure communication setup between 8864 and StackVision using SSH reverse tunneling.
  - Detailed RSA key exchange, firewall considerations, and authentication process.

- **Document 3 (ESC Secure Communication Ports):**
  - Outlined network port requirements and encryption/authentication protocols (AES-128, HMAC-SHA256, RSA-2048, Diffie-Hellman).
  - Confirmed no inbound firewall penetration needed for secure communications.

---

If you’d like, I can also create a **visual network diagram** showing the secure communication flow and alarm monitoring architecture for the 8864–StackVision system. Would you like me to prepare that?

## Glossary

- **8864**: Data controller platform used by engineering
- **MODBUS**: Serial communications protocol for industrial automation
