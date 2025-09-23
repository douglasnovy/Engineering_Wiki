---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

# Consolidated Knowledge Base Entry  
## **StackVision and 8864 Data Acquisition System (DAS) – Secure Communication, Alarm Monitoring, and Network Configuration**

---

## **Overview**
The StackVision system, in conjunction with the 8864 Data Acquisition System (DAS), is a critical platform for environmental data collection, monitoring, and reporting. Reliable communication between the 8864 and StackVision is essential for continuous data integrity, regulatory compliance, and operational efficiency. This document consolidates engineering standards, secure communication setup procedures, network port requirements, and diagnostic/alarm monitoring practices to provide a comprehensive technical reference.

---

## **Key Concepts**

### **1. StackVision–8864 Communication**
- The 8864 DAS communicates with StackVision for data transfer, configuration, and control.
- Communication reliability is critical; interruptions can result in data loss or regulatory non-compliance.
- Secure communication methods are available starting with 8864 firmware v5.02, using SSH reverse tunneling.

### **2. Secure Communications**
- Implemented via **SSH reverse tunneling** initiated by the 8864 to the StackVision server.
- Uses **RSA-2048 public/private key authentication** to ensure trusted endpoints.
- Eliminates the need for inbound firewall openings, reducing security risks.

### **3. Alarm Monitoring**
- Communication alarms can be configured within StackStudio to detect failures, including StackVision core service outages.
- Alarm logic can be implemented using an **8864 counter channel** for enhanced reliability.

### **4. Network Port Management**
- Understanding TCP/IP port usage is essential for firewall configuration, troubleshooting, and secure deployment.
- StackVision and FleetVision components use specific inbound and outbound ports for data transfer, SQL reporting, and controller communication.

### **5. Diagnostic Analyzer Range Evaluation**
- Diagnostic tools can assess analyzer performance over time, identifying operational ranges and anomalies.
- Reports include statistical summaries (mean, median, mode, min, max) and compliance with MPC/MPF thresholds.

---

## **Technical Details**

### **Secure Communication Setup (Firmware v5.02 and later)**
1. **Reverse SSH Tunnel**
   - Initiated from the 8864 to the StackVision server.
   - Functions like a port-specific VPN.
   - Outbound-only connection through firewalls.

2. **Key Exchange**
   - **Public key of each 8864** installed on the StackVision server.
   - **Public key of the StackVision server** installed on each 8864.
   - Keys can be distributed over insecure channels but must be protected from unauthorized installation.

3. **Encryption & Authentication**
   - RSA-2048 for authentication.
   - AES-128 encryption.
   - HMAC-SHA256 signing.
   - Diffie-Hellman key exchange.

---

### **Communication Alarm Configuration**
- Historically implemented via **Windows Task Scheduler**.
- Recommended approach: configure entirely within **StackStudio**.
- Benefits:
  - Detects both network failures and StackVision service outages.
  - Uses **8864 counter channel** for robust monitoring.
- Future goal: integrate directly into 8864 firmware.

---

### **TCP/IP Port Usage**
**StackVision Server – Inbound Ports**
- SQL Reporting Services (from SV Client)
- Data Link from FleetVision
- OPC/PI (if installed)
- Controller Emulation from SV Client

**StackVision Server – Outbound Ports**
- Controller file transfer (8832/8864)
- Controller polling
- SQL Server (if remote)
- Controller configuration compare

**StackVision Client – Outbound Ports**
- SQL Reporting Services
- StackVision Client Service
- Controller Emulation to SV Server

**Controller (8832/8864) – Inbound Ports**
- File transfer
- Controller emulation

---

### **Diagnostic Analyzer Range Evaluation**
- Example parameter: **S1:S1CPFLOW**
- Evaluation metrics:
  - % of range utilization (e.g., majority between 20–80%)
  - Hours in specific ranges (<10%, >100%)
  - Statistical measures (mean, median, mode, min, max)
  - Compliance with MPC/MPF thresholds
- Useful for performance tuning and maintenance planning.

---

## **Best Practices**
1. **Secure Communications**
   - Always use SSH reverse tunneling for 8864–StackVision connections where supported.
   - Maintain strict control over RSA key installation.
   - Regularly audit keys to prevent unauthorized access.

2. **Alarm Monitoring**
   - Implement communication alarms within StackStudio rather than relying solely on OS-level schedulers.
   - Use counter channels for more reliable detection.

3. **Network Configuration**
   - Document all required ports for StackVision, FleetVision, and controllers.
   - Configure firewalls to allow only necessary outbound connections.
   - Close unused ports to reduce attack surface.

4. **Diagnostics**
   - Schedule regular analyzer range evaluations.
   - Investigate deviations from expected operational ranges promptly.

---

## **Source Attribution**
- **[Document 1: Engineering Standard – 8864 DAS Communication Alarm]**  
  Provided alarm configuration methodology using StackStudio and counter channels; highlighted benefits over Windows Task Scheduler.

- **[Document 2: Diagnostic Analyzer Range Evaluation]**  
  Supplied example diagnostic report structure, statistical metrics, and performance evaluation methodology.

- **[Document 3: Setting up Secure Communications r4]**  
  Detailed SSH reverse tunneling setup, RSA key exchange process, and security considerations for 8864–StackVision communication.

- **[Document 4: ESC Secure Communication Ports]**  
  Outlined encryption/authentication methods (AES-128, HMAC-SHA256, RSA-2048, Diffie-Hellman) and firewall considerations.

- **[Document 5: TCP/IP Ports Used by a StackVision System]**  
  Provided comprehensive inbound/outbound port listings for StackVision server, client, and controllers.

---

If you’d like, I can also create a **network diagram** showing the 8864, StackVision server, and firewall with port flows and secure tunnel paths to visually complement this documentation. Would you like me to prepare that?

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

# Consolida...


## Glossary

- **8864**: Data controller platform used by engineering
