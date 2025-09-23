---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision and 8864 Data Controller: Secure Communications, Network Configuration, and Alarm Standards**

---

## Overview
This consolidated entry provides a comprehensive guide to configuring secure communications between StackVision servers and 8864 Data Controllers, understanding network port usage, and implementing communication alarms for system reliability. It also includes diagnostic analyzer range evaluation concepts relevant to monitoring system performance. These topics are critical for ensuring data integrity, operational security, and timely detection of communication failures in environmental monitoring systems.

---

## Key Concepts

### StackVision
StackVision is a data acquisition and reporting system used in environmental compliance monitoring. It interfaces with Data Controllers (such as the 8864 and 8832) and various instruments via secure network connections.

### 8864 Data Controller
The 8864 is a hardware device that collects and transmits environmental monitoring data to StackVision. Beginning with firmware v5.02, it supports secure communications via SSH reverse tunneling.

### Secure Communications
Secure communications between StackVision and the 8864 use encryption, authentication, and tunneling to protect data from interception or tampering.

### Communication Alarms
Communication alarms detect and alert operators to failures in data transmission between the 8864 and StackVision, including cases where core services stop functioning.

### Diagnostic Analyzer Range Evaluation
A method for assessing whether measured parameters fall within expected operational ranges, helping to identify anomalies or equipment issues.

---

## Technical Details

### 1. Secure Communications Configuration (Firmware v5.02+)
- **Method:** SSH reverse tunneling initiated by the 8864 to the StackVision server.
- **Firewall Considerations:** Only outbound connections are required; no inbound ports need to be opened.
- **Authentication:** RSA-2048 public/private key pairs.
  - Public keys of each 8864 must be installed on the StackVision server’s SSH service.
  - The StackVision server’s public key must be installed on each 8864.
- **Key Management:** Public keys can be distributed via unsecured channels but must be monitored to prevent unauthorized installations.
- **Encryption & Integrity:**
  - AES-128 encryption
  - HMAC-SHA256 signing
  - Diffie-Hellman key exchange

### 2. Network Port Usage
#### StackVision Server – Inbound Connections:
- SQL Reporting Services (from SV Client)
- Data Link from FleetVision
- OPC/PI (if installed)
- StackVision Client Service
- Controller Emulation from SV Client

#### StackVision Server – Outbound Connections:
- Controller file transfer (8832 or 8864)
- Controller configuration compare (8864 only)
- SQL Server (if remote)
- Controller polling (8832 or 8864)

#### StackVision Client – Outbound Connections:
- SQL Reporting Services
- StackVision Client Service
- Controller Emulation to SV Server

#### Data Controllers – Inbound Connections:
- File transfer ports
- Controller emulation ports

### 3. Communication Alarm Implementation
- **Current Implementation:** Often via Windows Task Scheduler scripts.
- **Enhanced Method:** Use StackVision polling alarms configured entirely within StackStudio.
- **Benefits:** Detects failures in StackVision core services in addition to communication loss.
- **Channel Configuration:** Updated to use an 8864 counter channel.
- **Future Development:** Integration into 8864 firmware.

### 4. Diagnostic Analyzer Range Evaluation
- **Purpose:** Evaluate operational range of parameters (e.g., S1CPFLOW).
- **Example Result:** Majority of readings between 20%–80% of range.
- **Metrics:** Mean, median, mode, minimum, maximum, total valid hours above MPC/MPF.
- **Application:** Identify periods where readings fall outside expected ranges (<10% or >100%).

---

## Best Practices

1. **Secure Communications**
   - Always use the latest firmware supporting SSH reverse tunneling.
   - Maintain strict control over key installation and updates.
   - Regularly audit keys to ensure only authorized devices are connected.

2. **Network Configuration**
   - Document all inbound and outbound port usage for StackVision components.
   - Close unused ports to reduce attack surface.
   - Ensure firewall rules align with outbound-only connection requirements for 8864.

3. **Communication Alarms**
   - Prefer StackVision-based polling alarms over OS-level schedulers for integrated monitoring.
   - Configure alarms to detect both communication loss and service failures.
   - Periodically test alarm functionality.

4. **Performance Monitoring**
   - Use diagnostic analyzer range evaluations to detect anomalies early.
   - Investigate readings outside expected ranges promptly.
   - Maintain historical data for trend analysis.

---

## Source Attribution

- **[Document 1]:** Provided details on implementing 8864 DAS communication alarms using StackVision polling and StackStudio configuration, including benefits over Windows Task Scheduler.
- **[Document 2]:** Contributed diagnostic analyzer range evaluation methodology and example metrics for operational performance monitoring.
- **[Document 3]:** Detailed secure communications setup between StackVision and 8864 using SSH reverse tunneling, RSA key authentication, and firewall considerations.
- **[Document 4]:** Outlined secure communication encryption standards (AES-128, HMAC-SHA256, RSA-2048) and network connection principles without inbound firewall penetration.
- **[Document 5]:** Listed TCP/IP port usage for StackVision servers, clients, and data controllers, including inbound/outbound connection specifics.

---

If you’d like, I can create a **network diagram** showing the secure communication flow between StackVision, 8864, and other components, along with port usage mapping. Would you like me to add that?

## See Also

- [[Environmental]] - These topics are critical for ensuring data integr...
- [[Environmental]] - ---

## Key Concepts

### StackVision
StackVision ...
- [[Environmental]] - ### 8864 Data Controller
The 8864 is a hardware de...


## Glossary

- **8864**: Data controller platform used by engineering
