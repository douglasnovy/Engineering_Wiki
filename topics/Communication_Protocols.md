---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision and 8864 Data Acquisition System (DAS) – Secure Communication, Alarm Monitoring, and Network Configuration Standards**

---

## Overview
This document consolidates engineering standards, configuration procedures, and diagnostic practices for integrating and maintaining secure communications between StackVision systems and 8864 Data Acquisition Systems (DAS). It also covers alarm monitoring strategies, TCP/IP port usage, and diagnostic analyzer range evaluations. These practices are critical for ensuring data integrity, system availability, and compliance with operational and regulatory requirements.

---

## Key Concepts

### StackVision
A data acquisition and reporting platform used for environmental monitoring and compliance reporting. It interfaces with field devices such as the 8864 DAS via secure communication channels.

### 8864 DAS
A data controller that collects and transmits environmental monitoring data to StackVision. Supports secure communications starting with firmware v5.02.

### Secure Communications
A method of encrypted, authenticated data transfer between StackVision and 8864, using SSH reverse tunneling and RSA key authentication.

### Communication Alarms
Automated alerts triggered when communication between StackVision and the 8864 DAS is interrupted or degraded.

### Diagnostic Analyzer Range Evaluation
A statistical analysis of instrument performance over a defined period, identifying operational ranges and anomalies.

---

## Technical Details

### 1. Secure Communication Configuration (8864 ↔ StackVision)
- **Method**: SSH reverse tunneling (firmware v5.02+).
- **Initiation**: Connection is initiated from the 8864 to the StackVision server (outbound only), eliminating the need for inbound firewall rules.
- **Authentication**: 2048-bit RSA public/private key pairs.
  - Public key of each 8864 installed on the StackVision server.
  - Public key of the StackVision server installed on each 8864.
- **Encryption & Integrity**:
  - AES-128 encryption
  - HMAC-SHA256 signing
  - Diffie-Hellman key exchange
- **Security Note**: Public keys can be distributed over unsecured channels, but installation must be tightly controlled to prevent unauthorized access.

### 2. Network and Port Usage
**StackVision Server – Inbound Connections**:
- From SV Client: SQL Reporting Services, StackVision Client Service, Controller Emulation.
- From FleetVision: Data Link.
- From OPC client: OPC/PI (if installed).

**StackVision Server – Outbound Connections**:
- To Data Controller (8832/8864): File transfer, polling, configuration compare, controller emulation.
- To SQL Server: Database access.

**Firewall Considerations**:
- No inbound firewall penetration required for secure communications.
- Only outbound ports from 8864 to StackVision need to be open.

### 3. Communication Alarm Standard
- **Purpose**: Detects communication failures between StackVision and 8864 DAS.
- **Implementation**:
  - Historically via Windows Task Scheduler.
  - Preferred method: StackVision polling alarms configured in StackStudio using an 8864 counter channel.
  - Advantage: Detects failures even if StackVision core services stop.
- **Future Plan**: Integration into 8864 firmware.

### 4. Diagnostic Analyzer Range Evaluation
- **Example Parameter**: S1:S1CPFLOW
- **Evaluation Metrics**:
  - % of operational range utilization.
  - Hours in specific range bands (<10%, >100%).
  - Statistical measures: Mean, Median, Mode, Min, Max.
  - Total valid hours above MPC/MPF thresholds.
- **Purpose**: Identify performance trends, detect anomalies, and ensure compliance.

---

## Best Practices

1. **Secure Key Management**:
   - Maintain strict control over RSA key installation.
   - Regularly audit installed keys on both StackVision and 8864 devices.

2. **Firewall Configuration**:
   - Allow only necessary outbound connections from 8864 to StackVision.
   - Avoid inbound firewall openings for enhanced security.

3. **Alarm Configuration**:
   - Use StackVision polling alarms within StackStudio for robust communication monitoring.
   - Periodically test alarm triggers to ensure reliability.

4. **Port Management**:
   - Document all open ports and their purposes.
   - Close unused ports to reduce attack surface.

5. **Performance Monitoring**:
   - Conduct regular diagnostic analyzer range evaluations.
   - Investigate and address any out-of-range or anomalous readings promptly.

---

## Source Attribution
- **[Document 1: Engineering Standard - 8864 DAS Communication Alarm]**: Provided details on communication alarm configuration using StackVision polling and StackStudio, with historical context and future firmware integration plans.
- **[Document 2: Diagnostic Analyzer Range]**: Supplied methodology and metrics for evaluating analyzer performance over time.
- **[Document 3: Setting up Secure Communications r4]**: Detailed SSH reverse tunneling setup, RSA key exchange process, and security considerations for 8864–StackVision communications.
- **[Document 4: ESC Secure Communication Ports]**: Outlined encryption standards (AES-128, HMAC-SHA256, RSA-2048) and firewall considerations for secure communications.
- **[Document 5: TCP/IP Ports Used by a StackVision System]**: Listed inbound/outbound port configurations for StackVision servers, clients, and controllers, including operational use cases.

---

If you’d like, I can also create a **network diagram** showing the secure communication flow between StackVision, 8864 DAS, and other components, including port usage and firewall boundaries. This would make the configuration much easier to visualize. Would you like me to prepare that?

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_8864CommunicationAlarm_8864DASCommunicationAlarmxlsm_f00d217c.xlsm](../tools/engineering_white_papers_WhitePapers_8864CommunicationAlarm_8864DASCommunicationAlarmxlsm_f00d217c.xlsm)** (0.79 MB)
- **[engineering_white_papers_WhitePapers_Alarms_8864DASCommunicationAlarmxlsm_62dbf367.xlsm](../tools/engineering_white_papers_WhitePapers_Alarms_8864DASCommunicationAlarmxlsm_62dbf367.xlsm)** (0.79 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - ---

## Key Concepts

### StackVision
A data acqui...
- [[Environmental]] - ### 8864 DAS
A data controller that collects and t...


## Glossary

- **8864**: Data controller platform used by engineering
