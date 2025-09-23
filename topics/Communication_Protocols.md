---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision and 8864 Data Controller: Secure Communication, Alarm Monitoring, and Network Configuration Standards**

---

## Overview
This consolidated entry provides a comprehensive guide to configuring secure communications between StackVision servers and 8864 Data Controllers, implementing communication alarms for system reliability, and understanding TCP/IP port usage and network security considerations. It also includes diagnostic analyzer range evaluation principles for performance monitoring. These standards ensure robust data acquisition, secure data transfer, and proactive system health monitoring in industrial emissions monitoring systems.

---

## Key Concepts

### StackVision
StackVision is an environmental data acquisition and reporting system used for continuous emissions monitoring. It interfaces with Data Controllers (such as the 8864 and 8832) to collect, process, and store measurement data.

### 8864 Data Controller
The 8864 is a hardware device that collects emissions data from instruments and transmits it to StackVision. It supports secure communications, controller emulation, and alarm monitoring.

### Secure Communications
Secure communications between StackVision and the 8864 are implemented using SSH reverse tunneling and cryptographic authentication to protect data integrity and confidentiality.

### Communication Alarms
Communication alarms detect and alert operators when data transfer between StackVision and the 8864 fails, ensuring timely intervention to prevent data loss.

### Diagnostic Analyzer Range Evaluation
Analyzer range diagnostics assess whether measurement parameters remain within expected operational ranges, helping identify sensor drift or malfunction.

---

## Technical Details

### 1. Secure Communication Configuration (8864 ↔ StackVision)
- **Firmware Requirement:** v5.02 or later on the 8864.
- **Method:** SSH reverse tunneling initiated by the 8864 to the StackVision server.
- **Firewall Considerations:** No inbound ports need to be opened; all traffic is outbound from the 8864.
- **Authentication:**  
  - RSA 2048-bit public/private key pairs.  
  - Public keys must be manually installed on both the StackVision server and each 8864 unit.  
  - Keys can be distributed over unsecured channels but must be monitored to prevent unauthorized installation.
- **Encryption & Integrity:**  
  - AES-128 encryption  
  - HMAC-SHA256 signing  
  - Diffie-Hellman key exchange

*(Sources: Document 3, Document 4)*

---

### 2. Communication Alarm Implementation
- **Purpose:** Detect loss of communication between StackVision and the 8864, including failures in StackVision core services.
- **Implementation Methods:**  
  - Windows Task Scheduler scripts  
  - StackVision polling alarms configured in StackStudio
- **Advantages of StackStudio Configuration:**  
  - Fully contained within StackVision environment  
  - Uses 8864 counter channel for monitoring  
  - Can detect core service failures in addition to network issues
- **Future Development:** Potential integration into 8864 firmware for native alarm handling.

*(Source: Document 1)*

---

### 3. TCP/IP Port Usage in StackVision Systems
**Inbound Connections to StackVision Server:**
- SQL Reporting Services (from SV Client)
- Data Link from FleetVision
- OPC/PI (if installed)
- Controller Emulation from SV Client

**Outbound Connections from StackVision Server:**
- Controller file transfer (ports for 8832/8864)
- Controller emulation/configuration compare (8864 only)
- SQL Server (if remote)
- Controller polling (8832/8864)

**StackVision Client:**
- No inbound ports required
- Outbound connections to SQL Server, SV Server, and for controller emulation

**Data Controllers (8832/8864):**
- Inbound ports for file transfer and controller emulation
- Outbound connections for data polling and configuration

*(Source: Document 5)*

---

### 4. Diagnostic Analyzer Range Evaluation
- **Parameter Example:** S1:S1CPFLOW
- **Evaluation Metrics:**  
  - Percentage of operational hours within defined range (e.g., 20–80%)  
  - Hours below 10% or above 100% of range  
  - Mean, median, mode, min, max values  
  - Total valid hours above MPC/MPF thresholds
- **Purpose:** Identify anomalies in analyzer performance over a defined evaluation period.

*(Source: Document 2)*

---

## Best Practices

1. **Secure Key Management:**  
   - Maintain strict control over public key installation.  
   - Regularly audit keys on both server and controllers.

2. **Firewall Configuration:**  
   - Leverage outbound-only SSH tunnels to minimize attack surface.  
   - Close unused ports to reduce exposure.

3. **Alarm Redundancy:**  
   - Implement both software-based (StackStudio) and OS-level (Task Scheduler) alarms for maximum reliability.

4. **Port Documentation:**  
   - Maintain an up-to-date inventory of all ports used by StackVision components.  
   - Review port usage during server migrations or network changes.

5. **Performance Monitoring:**  
   - Schedule regular diagnostic analyzer range evaluations.  
   - Investigate deviations promptly to prevent data quality issues.

---

## Source Attribution
- **Document 1:** Provided details on communication alarm implementation using StackStudio and Windows Task Scheduler, including use of 8864 counter channels.
- **Document 2:** Contributed diagnostic analyzer range evaluation methodology and performance metrics.
- **Document 3:** Detailed secure communication setup between StackVision and 8864 using SSH reverse tunneling and RSA key authentication.
- **Document 4:** Outlined secure communication encryption standards (AES-128, HMAC-SHA256, RSA-2048, Diffie-Hellman) and firewall considerations.
- **Document 5:** Listed TCP/IP port usage for StackVision servers, clients, and data controllers, including inbound/outbound connection mapping.

---

If you’d like, I can create a **network diagram** showing the secure communication flow, port usage, and alarm monitoring points between StackVision and the 8864. Would you like me to add that?

## See Also

- [[Environmental]] - ---

## Key Concepts

### StackVision
StackVision ...


## Glossary

- **8864**: Data controller platform used by engineering
