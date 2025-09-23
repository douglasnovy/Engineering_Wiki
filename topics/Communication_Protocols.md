---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**StackVision and 8864 Data Acquisition System (DAS) – Secure Communication, Alarm Configuration, and Network Port Standards**

---

## Overview
This consolidated entry provides a comprehensive guide to configuring secure communications between StackVision and 8864 Data Controllers, setting up communication alarms, understanding diagnostic analyzer range evaluations, and managing TCP/IP port usage for StackVision systems. These topics are critical for ensuring reliable data acquisition, maintaining operational integrity, and safeguarding system communications against unauthorized access.

---

## Key Concepts

1. **StackVision** – An environmental data acquisition and reporting system used for continuous emissions monitoring and other industrial data collection tasks.
2. **8864 Data Controller** – A hardware device that interfaces with instruments and StackVision to collect and transmit data.
3. **Secure Communications** – Methods to protect data integrity and confidentiality between StackVision servers and 8864 controllers.
4. **Communication Alarms** – Automated alerts triggered when data polling or communication between StackVision and controllers fails.
5. **Diagnostic Analyzer Range Evaluation** – Statistical analysis of instrument performance over a defined period.
6. **TCP/IP Port Management** – Specification of inbound and outbound network ports used by StackVision components to ensure proper firewall configuration and connectivity.

---

## Technical Details

### 1. Secure Communications Between StackVision and 8864
Beginning with firmware v5.02, the 8864 supports secure communications via **SSH reverse tunneling**:
- **Connection Initiation**: The 8864 initiates the tunnel to the StackVision server, eliminating the need for inbound firewall openings.
- **Authentication**: Utilizes **2048-bit RSA public/private keys**.  
  - Public key of each 8864 must be installed on the StackVision server’s SSH service.
  - Public key of the StackVision server must be installed on each 8864.
- **Encryption & Signing**: AES-128 encryption, HMAC-SHA256 signing, and Diffie-Hellman key exchange.
- **Security Considerations**: Keys can be distributed over unsecured channels but must be monitored to prevent rogue installations.

### 2. Communication Alarm Configuration
The **8864 DAS Communication Alarm** can be implemented entirely within StackStudio:
- Uses an **8864 counter channel** to monitor communication status.
- Alarms trigger when StackVision polling fails or core services stop.
- Historically implemented via Windows Task Scheduler, but StackStudio integration offers direct monitoring and alarm generation.
- Future firmware updates may integrate this functionality directly into the 8864.

### 3. Diagnostic Analyzer Range Evaluation
Example evaluation for parameter `S1:S1CPFLOW`:
- Majority of readings between **20%–80%** of range.
- Statistical metrics include mean, median, mode, min, max, and cumulative percentages for ranges `<10%` and `>100%`.
- Reports generated via StackVision’s reporting tools, useful for performance verification and compliance documentation.

### 4. TCP/IP Ports Used by StackVision Systems
**Inbound Connections to StackVision Server**:
- SQL Reporting Services (from SV Client)
- Data Link from FleetVision
- OPC/PI (if installed)
- Controller Emulation from SV Client

**Outbound Connections from StackVision Server**:
- Controller file transfer (8832/8864)
- Controller configuration compare (8864 only)
- SQL Server (if remote)
- Controller polling (8832/8864)

**Security Note**:  
No inbound firewall penetration is required for secure communications; all connections from controllers are outbound.

---

## Best Practices

1. **Secure Key Management**  
   - Maintain strict control over RSA key installation.
   - Regularly audit installed keys on both server and controllers.

2. **Alarm Integration**  
   - Prefer StackStudio-based alarm configurations over external schedulers for tighter integration and reduced points of failure.
   - Test alarms periodically to ensure operational readiness.

3. **Firewall Configuration**  
   - Allow only necessary outbound ports from controllers.
   - Keep inbound ports to StackVision server restricted to documented requirements.

4. **Performance Monitoring**  
   - Use diagnostic analyzer range evaluations to identify anomalies in instrument performance.
   - Schedule periodic reviews of statistical reports for compliance and maintenance planning.

5. **Documentation and Version Control**  
   - Maintain updated records of firmware versions, port configurations, and alarm settings.
   - Align configurations with the latest engineering standards.

---

## Source Attribution

- **[Document 1: Engineering Standard - 8864 DAS Communication Alarm]**  
  Provided details on implementing communication alarms within StackStudio using an 8864 counter channel, replacing Windows Task Scheduler methods.

- **[Document 2: Diagnostic Analyzer Range]**  
  Contributed statistical evaluation methodology for analyzer performance, including range distribution and key metrics.

- **[Document 3: Setting up Secure Communications r4]**  
  Detailed SSH reverse tunneling setup, RSA key authentication, and firewall considerations for secure 8864–StackVision communications.

- **[Document 4: ESC Secure Communication Ports]**  
  Outlined encryption, signing, and authentication standards for StackVision network connections.

- **[Document 5: TCP/IP Ports Used by a StackVision System]**  
  Provided comprehensive inbound/outbound port specifications for StackVision servers, clients, and controllers.

---

If you’d like, I can create a **network diagram** showing the secure communication flow between the 8864, StackVision server, and firewall, along with port usage. This would make the configuration much easier to visualize. Would you like me to prepare that?

## See Also

- [[Environmental]] - **StackVision** – An environmental data acquisitio...


## Glossary

- **8864**: Data controller platform used by engineering
