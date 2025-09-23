---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision and 8864 Data Acquisition System (DAS) Communication, Secure Networking, and Diagnostic Evaluation Standards**

---

## Overview
This consolidated entry outlines engineering standards, secure communication configurations, network port usage, and diagnostic evaluation procedures for the StackVision system and 8864 Data Acquisition System (DAS). It integrates alarm configuration methods, secure SSH tunneling protocols, TCP/IP port specifications, and diagnostic analyzer range evaluation to provide a comprehensive reference for system engineers and administrators. The goal is to ensure reliable data acquisition, secure communications, and effective performance monitoring across StackVision deployments.

---

## Key Concepts

1. **StackVision System**  
   A data acquisition and reporting platform used for environmental monitoring, often integrated with 8864 or 8832 data controllers.

2. **8864 DAS**  
   A data controller supporting secure communications (from firmware v5.02 onward) and advanced alarm configurations.

3. **Secure Communications**  
   Implemented via SSH reverse tunneling, RSA key authentication, and AES/HMAC encryption, ensuring data integrity and confidentiality without requiring inbound firewall penetration.

4. **Diagnostic Analyzer Range Evaluation**  
   A statistical method for assessing instrument performance over a defined period, focusing on operational range compliance.

5. **Alarm Configuration**  
   Methods for detecting communication failures between StackVision and DAS controllers, including polling-based alarms and counter channel monitoring.

---

## Technical Details

### 1. Communication Alarm Configuration (8864 DAS)
- **Purpose:** Detect communication failures between StackVision and the 8864 DAS.
- **Implementation Methods:**
  - **Windows Task Scheduler:** Historically used to trigger alarms.
  - **StackVision Polling Alarms:** Preferred method; alarms when StackVision core services stop.
  - **StackStudio Configuration:** Fully contained setup using an 8864 counter channel.
- **Future Development:** Integration into 8864 firmware for native support.

---

### 2. Secure Communication Setup
- **Firmware Requirement:** v5.02 or later for 8864.
- **Method:** SSH reverse tunneling initiated by the 8864 to the StackVision server.
- **Firewall Considerations:** Only outbound connections required; no inbound ports need to be opened.
- **Authentication:**
  - 2048-bit RSA public/private keys.
  - Public keys exchanged between each 8864 and the StackVision server.
  - Keys can be distributed via unsecured channels but must be monitored to prevent unauthorized installations.
- **Encryption & Signing:**
  - AES-128 encryption.
  - HMAC-SHA256 signing.
  - Diffie-Hellman key exchange for session keys.

---

### 3. TCP/IP Port Usage
**Inbound Ports (StackVision Server):**
- SQL Reporting Services (from SV Client)
- Data Link from FleetVision
- OPC/PI (if installed)
- Controller Emulation (from SV Client)

**Outbound Ports (StackVision Server):**
- Controller file transfer (8832/8864)
- Controller emulation/configuration compare (8864 only)
- SQL Server (if remote)
- Controller polling (8832/8864)

**Client and Controller Port Behavior:**
- StackVision Client: No inbound ports; outbound to SQL Server and SV Server.
- 8832/8864 Controllers: Specific inbound ports for file transfer and emulation.

---

### 4. Diagnostic Analyzer Range Evaluation
- **Parameter Example:** `S1:S1CPFLOW`
- **Evaluation Metrics:**
  - Percentage of operational range utilization.
  - Hours within specific range thresholds (<10%, >100%).
  - Statistical measures: mean, median, mode, min, max.
  - Total valid hours above MPC/MPF thresholds.
- **Purpose:** Identify performance trends and compliance with operational specifications.
- **Sample Evaluation Period:** 01/01/2012 – 12/31/2013.

---

## Best Practices

1. **Alarm Configuration:**
   - Use StackVision polling alarms for robust detection of service interruptions.
   - Configure alarms entirely within StackStudio to simplify management.

2. **Secure Communications:**
   - Always use firmware v5.02 or later for 8864 controllers.
   - Maintain strict control over RSA key installation to prevent unauthorized access.
   - Leverage outbound-only firewall rules to reduce attack surface.

3. **Network Port Management:**
   - Document and monitor all inbound/outbound port usage.
   - Close unused ports to minimize security risks.
   - Ensure encryption and authentication protocols are active for all communications.

4. **Diagnostic Monitoring:**
   - Regularly run range evaluations to detect anomalies.
   - Compare against MPC/MPF thresholds for compliance.
   - Use statistical summaries to guide maintenance and calibration schedules.

---

## Source Attribution

- **[Document 1]:** Provided engineering standard for 8864 DAS communication alarms, including StackVision polling method and StackStudio configuration details. (Brian Perlov)
- **[Document 2]:** Supplied diagnostic analyzer range evaluation methodology and statistical reporting format.
- **[Document 3]:** Detailed secure communication setup between StackVision and 8864 using SSH reverse tunneling, RSA authentication, and encryption protocols. (Mark Shell)
- **[Document 4]:** Outlined secure communication port requirements, encryption standards, and firewall considerations for StackVision.
- **[Document 5]:** Listed TCP/IP port usage for StackVision servers, clients, and controllers, including inbound/outbound specifications. (Mark Shell)

---

If you’d like, I can create a **network diagram** showing the secure communication flow between the 8864 DAS, StackVision server, and clients, along with port assignments. This would make the consolidated entry more visual and easier to reference. Would you like me to add that?

## See Also

- [[Environmental]] - **StackVision System**  
   A data acquisition and...
- [[Calibration]] - - Use statistical summaries to guide maintenance a...


## Glossary

- **8864**: Data controller platform used by engineering
