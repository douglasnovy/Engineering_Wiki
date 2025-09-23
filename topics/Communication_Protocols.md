---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision–8864 Secure Communications, Alarm Integration, and Network Configuration Standards**

---

## Overview
This consolidated entry provides a comprehensive guide to configuring secure communications between StackVision servers and 8864 Data Controllers, setting up communication alarms, understanding diagnostic analyzer range evaluations, and managing TCP/IP port usage for StackVision systems. These procedures are critical for ensuring reliable data acquisition, secure remote connectivity, and proactive system monitoring in industrial emissions monitoring and control environments.

---

## Key Concepts

### StackVision and 8864 Data Controller
- **StackVision**: A data acquisition and handling system (DAHS) used for environmental compliance monitoring.
- **8864 Data Controller**: A hardware device that interfaces with StackVision to collect and transmit environmental data.

### Secure Communications
- Implemented via **SSH reverse tunneling** starting with 8864 firmware v5.02.
- Uses **RSA-2048 public/private key authentication** to ensure trusted connections.
- Eliminates the need for inbound firewall ports by initiating outbound-only connections from the 8864.

### Communication Alarms
- Designed to detect and alert on communication failures between StackVision and the 8864.
- Can be configured entirely within StackStudio, leveraging StackVision polling to detect service interruptions.

### Diagnostic Analyzer Range Evaluation
- Statistical analysis of analyzer performance over a defined period.
- Identifies operational ranges, uptime, and compliance with measurement performance criteria (MPC/MPF).

### TCP/IP Port Management
- Proper port configuration is essential for secure and reliable data transfer between StackVision components, controllers, and clients.

---

## Technical Details

### 1. Secure Communications Configuration
**Procedure:**
1. **Firmware Requirement**: Ensure 8864 firmware is v5.02 or higher.
2. **SSH Reverse Tunnel Setup**:
   - On boot, the 8864 initiates a reverse SSH tunnel to the StackVision server.
   - Tunnel acts as a port-specific VPN, with outbound-only firewall traffic.
3. **Key Exchange**:
   - Install the 8864’s public key on the StackVision server’s SSH service.
   - Install the StackVision server’s public key on the 8864.
   - Keys are public and can be distributed via unsecured channels, but installation must be controlled to prevent rogue access.
4. **Encryption and Authentication**:
   - AES-128 encryption for data.
   - HMAC-SHA256 for message integrity.
   - RSA-2048 for authentication.
   - Diffie-Hellman for key exchange.

---

### 2. Communication Alarm Setup
**Approach:**
- Implement via Windows Task Scheduler or within StackStudio.
- Use StackVision polling alarms to detect:
  - Loss of communication with the 8864.
  - StackVision core service failures.
- Configure using an **8864 counter channel** for monitoring.
- Future firmware updates may integrate this functionality directly into the 8864.

---

### 3. Diagnostic Analyzer Range Evaluation
**Parameters:**
- Example: `S1:S1CPFLOW`
- Evaluation metrics include:
  - Percentage of operational range (e.g., 20–80%).
  - Hours in range vs. total online hours.
  - Mean, median, mode, min, max values.
  - Compliance with MPC/MPF thresholds.
- Useful for identifying performance issues and ensuring regulatory compliance.

---

### 4. TCP/IP Port Usage in StackVision Systems
**Inbound Ports (Server)**:
- SQL Reporting Services (from SV Client).
- Data Link from FleetVision.
- OPC/PI (if installed).
- Controller Emulation from SV Client.

**Outbound Ports (Server)**:
- Controller file transfer (8832/8864).
- Controller configuration compare (8864 only).
- SQL Server (if remote).
- Controller polling (8832/8864).

**Client Ports**:
- No inbound ports required.
- Outbound connections to SQL Server, SV Server, and controller emulation.

**Controller Ports**:
- 8832/8864 inbound ports for file transfer and polling.
- Outbound connections to SV Server for emulation and configuration.

---

## Best Practices
1. **Security**:
   - Use SSH reverse tunneling to avoid inbound firewall exposure.
   - Strictly control public key installation to prevent unauthorized access.
2. **Reliability**:
   - Implement communication alarms to detect failures early.
   - Use StackVision polling for comprehensive monitoring.
3. **Performance Monitoring**:
   - Regularly review diagnostic analyzer range reports to ensure compliance.
4. **Network Management**:
   - Document and verify all TCP/IP port configurations.
   - Close unused ports to reduce attack surface.
5. **Future-Proofing**:
   - Plan for firmware updates that integrate alarm functionality directly into the 8864.

---

## Source Attribution
- **[Document 1]**: Provided details on 8864 DAS Communication Alarm configuration via StackStudio and Windows Task Scheduler, including use of counter channels and polling alarms.
- **[Document 2]**: Contributed diagnostic analyzer range evaluation methodology and statistical reporting parameters.
- **[Document 3]**: Detailed secure communications setup between StackVision and 8864 using SSH reverse tunneling and RSA key authentication.
- **[Document 4]**: Outlined secure communication port requirements, encryption standards, and firewall considerations.
- **[Document 5]**: Listed TCP/IP port usage for StackVision servers, clients, and controllers, including inbound/outbound configurations.

---

If you’d like, I can create a **network diagram** showing the secure communication flow, port usage, and alarm monitoring points for StackVision–8864 systems. This would make the relationships between these components much clearer. Would you like me to prepare that?

## See Also

- [[Environmental]] - ---

## Key Concepts

### StackVision and 8864 Dat...
- [[Environmental]] - - **8864 Data Controller**: A hardware device that...


## Glossary

- **8864**: Data controller platform used by engineering


## Glossary

- **8864**: Data controller platform used by engineering


## Glossary

- **8864**: Data controller platform used by engineering
