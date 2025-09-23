---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision–8864 Secure Communication, Alarm Configuration, and Network Port Standards**

---

## Overview
This consolidated entry provides a comprehensive guide to configuring secure communications between StackVision and 8864 Data Acquisition Systems (DAS), setting up communication alarms, understanding diagnostic analyzer range evaluations, and managing TCP/IP port usage for StackVision systems. These topics are critical for ensuring reliable data acquisition, secure network operations, and proactive system monitoring in industrial and environmental compliance contexts.

---

## Key Concepts

### StackVision and 8864 DAS
- **StackVision**: A data acquisition and reporting platform used for environmental monitoring and compliance.
- **8864 DAS**: A data controller unit that interfaces with StackVision to collect and transmit environmental data.
- **Secure Communication**: Implemented via SSH reverse tunneling and RSA key authentication to protect data integrity and confidentiality.
- **Communication Alarms**: Automated alerts triggered when data polling or core services fail, ensuring timely intervention.
- **Diagnostic Analyzer Range Evaluation**: Statistical analysis of parameter readings to assess operational performance and detect anomalies.
- **TCP/IP Port Management**: Defined inbound/outbound port usage for StackVision components to ensure proper connectivity and firewall compliance.

---

## Technical Details

### 1. Secure Communications (StackVision ↔ 8864)
- **Firmware Requirement**: v5.02 or later on 8864.
- **Method**: SSH reverse tunneling initiated by the 8864 to the StackVision server.
- **Firewall Implications**: Outbound-only connection from 8864; no inbound firewall ports need to be opened.
- **Authentication**:
  - 2048-bit RSA public/private keys.
  - Public key of each 8864 installed on StackVision server’s SSH service.
  - Public key of StackVision server installed on each 8864.
- **Encryption & Signing**:
  - AES-128 encryption.
  - HMAC-SHA256 signing.
  - Diffie-Hellman key exchange for session keys.
- **Security Note**: Keys can be distributed over unsecured channels but must be monitored to prevent rogue installations.

### 2. Communication Alarm Configuration
- **Purpose**: Detects communication failures between StackVision and 8864, including core service stoppages.
- **Implementation Options**:
  - Windows Task Scheduler scripts.
  - StackVision polling alarms configured in StackStudio.
- **Enhanced Method**: Uses an 8864 counter channel for alarm triggering.
- **Future Development**: Planned integration into 8864 firmware for native support.

### 3. Diagnostic Analyzer Range Evaluation
- **Example Parameter**: `S1:S1CPFLOW`.
- **Analysis Metrics**:
  - Percentage of readings within operational range (e.g., 20–80%).
  - Hours of operation in specific ranges (<10%, >100%).
  - Statistical measures: mean, median, mode, min, max.
  - Total valid hours above MPC/MPF thresholds.
- **Purpose**: Identifies performance trends and potential calibration or maintenance needs.

### 4. TCP/IP Ports Used by StackVision Systems
- **Server Inbound Ports**:
  - SQL Reporting Services.
  - Data Link from FleetVision.
  - OPC/PI (if installed).
  - StackVision Client Service.
  - Controller Emulation from SV Client.
- **Server Outbound Ports**:
  - Controller file transfer (8832/8864).
  - Controller configuration compare (8864 only).
  - SQL Server connections.
  - Controller polling (8832/8864).
- **Client Ports**:
  - No inbound ports.
  - Outbound to SQL Server, SV Server, and controller emulation.
- **Controller Ports**:
  - Inbound for file transfer and emulation.
  - Outbound for polling and configuration.

---

## Best Practices

1. **Secure Key Management**:
   - Maintain strict control over RSA key installation.
   - Regularly audit installed keys on both 8864 units and StackVision servers.

2. **Alarm Configuration**:
   - Prefer StackStudio-based polling alarms for integrated monitoring.
   - Use counter channels for more precise alarm triggers.
   - Test alarm functionality regularly.

3. **Firewall Configuration**:
   - Leverage outbound-only SSH tunnels to minimize firewall exposure.
   - Document all required ports and ensure they are open only as needed.

4. **Performance Monitoring**:
   - Schedule periodic diagnostic analyzer range evaluations.
   - Investigate deviations from expected operational ranges promptly.

5. **Port Documentation**:
   - Maintain an up-to-date port usage map for all StackVision components.
   - Close unused ports to reduce attack surface.

---

## Source Attribution

- **[Document 1]**: Provided details on the 8864 DAS communication alarm configuration, including StackStudio integration and counter channel usage.
- **[Document 2]**: Contributed diagnostic analyzer range evaluation methodology and statistical reporting parameters.
- **[Document 3]**: Detailed secure communication setup between StackVision and 8864 using SSH reverse tunneling and RSA key authentication.
- **[Document 4]**: Outlined secure communication encryption, signing, and authentication standards for StackVision network connections.
- **[Document 5]**: Listed TCP/IP port usage for StackVision servers, clients, and controllers, including inbound/outbound specifications.

---

If you’d like, I can create a **network diagram** showing the secure communication flow, port usage, and alarm integration between StackVision and 8864 DAS. This would make the relationships between these components much clearer. Would you like me to prepare that?

## See Also

- [[Environmental]] - These topics are critical for ensuring reliable da...
- [[Environmental]] - ---

## Key Concepts

### StackVision and 8864 DAS...
- [[Environmental]] - - **8864 DAS**: A data controller unit that interf...
- [[Calibration]] - - **Purpose**: Identifies performance trends and p...


## Glossary

- **8864**: Data controller platform used by engineering
