---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision and 8864 Data Controller: Secure Communications, Alarm Standards, and Network Port Configuration**

---

## Overview
This consolidated entry provides a comprehensive guide to configuring secure communications between StackVision and the 8864 Data Controller, implementing communication alarms, understanding diagnostic analyzer range evaluations, and managing TCP/IP port usage for StackVision systems. These topics are critical for ensuring reliable data acquisition, secure system operation, and effective monitoring in industrial and environmental compliance contexts.

---

## Key Concepts

### StackVision
StackVision is a data acquisition and control system used for environmental monitoring, compliance reporting, and integration with plant instrumentation.

### 8864 Data Controller
The 8864 is a hardware device that collects, processes, and transmits environmental monitoring data to StackVision. It supports secure communications and advanced alarm configurations.

### Secure Communications
Secure communications between StackVision and the 8864 are established using SSH reverse tunneling and cryptographic authentication to protect data integrity and confidentiality.

### Communication Alarms
Communication alarms detect and alert operators when data transfer between StackVision and the 8864 is interrupted or degraded.

### Diagnostic Analyzer Range Evaluation
A statistical method for evaluating analyzer performance by measuring operational parameters against expected ranges.

### TCP/IP Port Management
Proper configuration of inbound and outbound ports ensures secure and functional communication between StackVision components and external devices.

---

## Technical Details

### 1. Secure Communications Configuration (8864 ↔ StackVision)
- **Firmware Requirement:** v5.02 or later on the 8864.
- **Method:** SSH reverse tunneling initiated by the 8864 to the StackVision server.
- **Firewall Considerations:** No inbound ports need to be opened; only outbound connections from the 8864 are required.
- **Authentication:**  
  - 2048-bit RSA public/private key pairs.
  - Public keys of each 8864 must be installed on the StackVision server’s SSH service.
  - StackVision server’s public key must be installed on each 8864.
- **Security Notes:**  
  - Public keys can be distributed over unsecure channels but must be monitored to prevent unauthorized installations.
  - Keys ensure mutual authentication between trusted devices.

**Encryption and Integrity:**
- AES-128 encryption
- HMAC-SHA256 message signing
- Diffie-Hellman key exchange

---

### 2. Communication Alarm Standard (8864 DAS)
- **Purpose:** Detects communication failures between StackVision and the 8864, including core service stoppages.
- **Implementation Methods:**
  - Historically via Windows Task Scheduler.
  - Preferred method: StackVision polling alarms configured entirely within StackStudio.
- **Configuration:** Uses an 8864 counter channel for monitoring.
- **Future Development:** Planned integration into 8864 firmware for native support.

---

### 3. Diagnostic Analyzer Range Evaluation
- **Parameter Example:** S1:S1CPFLOW
- **Evaluation Metrics:**
  - Percentage of operational time within specified range (e.g., 20%-80%).
  - Hours and cumulative percentages for ranges <10% and >100%.
  - Statistical measures: Mean, Median, Mode, Min, Max.
  - Total valid hours above MPC/MPF thresholds.
- **Purpose:** Identify performance issues and ensure analyzer reliability.

---

### 4. TCP/IP Ports Used by StackVision Systems
**Inbound Connections (Server):**
- SQL Reporting Services (from SV Client)
- Data Link from FleetVision
- OPC/PI (if installed)
- Controller Emulation from SV Client

**Outbound Connections (Server):**
- Controller file transfer (8832 or 8864)
- Controller configuration compare (8864 only)
- SQL Server (if remote)
- Controller polling (8832 or 8864)

**Client Connections:**
- No inbound ports required.
- Outbound to SQL Server, SV Server, and for controller emulation.

**Controller Ports (8832/8864):**
- Inbound: File transfer, controller emulation.
- Outbound: As configured for polling and data transfer.

---

## Best Practices

1. **Secure Key Management:**  
   Maintain strict control over RSA public key installation to prevent unauthorized access.

2. **Firewall Configuration:**  
   Leverage outbound-only connections from 8864 to minimize exposure.

3. **Alarm Integration:**  
   Use StackVision’s internal polling alarms for communication monitoring rather than external schedulers.

4. **Performance Monitoring:**  
   Regularly review diagnostic analyzer range reports to detect deviations early.

5. **Port Documentation:**  
   Keep an updated list of required TCP/IP ports for StackVision components to aid in troubleshooting and security audits.

---

## Source Attribution
- **[Document 1]:** Provided details on the 8864 DAS Communication Alarm standard, implementation methods, and configuration using StackStudio.
- **[Document 2]:** Contributed statistical evaluation methodology for diagnostic analyzer range performance.
- **[Document 3]:** Detailed secure communications setup between StackVision and the 8864, including SSH reverse tunneling and RSA key authentication.
- **[Document 4]:** Outlined encryption, authentication, and firewall considerations for secure StackVision network connections.
- **[Document 5]:** Listed inbound/outbound TCP/IP port configurations for StackVision servers, clients, and controllers.

---

If you’d like, I can create a **network diagram** showing the secure communication flow between StackVision, the 8864, and other components, along with port usage. This would make the relationships and configurations much clearer. Would you like me to do that?

## See Also

- [[Environmental]] - These topics are critical for ensuring reliable da...
- [[Environmental]] - ---

## Key Concepts

### StackVision
StackVision ...
- [[Environmental]] - ### 8864 Data Controller
The 8864 is a hardware de...


## Glossary

- **8864**: Data controller platform used by engineering
