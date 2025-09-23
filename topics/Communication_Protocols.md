---
title: Communication_Protocols
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Alarms_EngineeringStandard-8864DASCommunicationAlarmmsg_208fb445.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_DiagnosticAnalyzerRangepdf_c93dddc1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SecureCommunication_SettingupSecureCommunicationsr4docx_3749cf68.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_ESCSecureCommunicationPortspdf_d3ae44db.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

# Consolidated Knowledge Base Entry

## Title
**StackVision and 8864 Data Acquisition System (DAS) – Secure Communication, Alarm Monitoring, and Network Configuration Standards**

---

## Overview
The StackVision system, in conjunction with the 8864 Data Acquisition System (DAS), is widely used for environmental data collection, monitoring, and reporting. Ensuring secure communications, reliable alarm monitoring, and proper network configuration is critical for system integrity, regulatory compliance, and operational continuity. This document consolidates engineering standards, secure communication setup procedures, TCP/IP port usage, and diagnostic evaluation methods into a single reference.

---

## Key Concepts

### StackVision
A server-based environmental data management platform that communicates with field data controllers (e.g., 8864 DAS) to collect, process, and report emissions and process data.

### 8864 DAS
A data acquisition controller that interfaces with plant instrumentation, performs data logging, and communicates with StackVision. Firmware version 5.02 and later supports secure SSH reverse tunneling.

### Secure Communications
A method of encrypting and authenticating data transfer between StackVision and the 8864 DAS to prevent unauthorized access and ensure data integrity.

### Communication Alarms
Automated alerts triggered when communication between StackVision and the 8864 DAS is interrupted or when core services fail.

### Diagnostic Analyzer Range Evaluation
A statistical analysis of process parameters to ensure they operate within expected ranges, identifying anomalies or performance issues.

---

## Technical Details

### 1. Secure Communication Setup (8864 ↔ StackVision)
- **Protocol**: SSH reverse tunneling (introduced in 8864 firmware v5.02).
- **Connection Direction**: Initiated from the 8864 to the StackVision server (outbound only), eliminating the need for inbound firewall rules.
- **Authentication**: 2048-bit RSA public/private key pairs.
  - Public key of each 8864 installed on the StackVision server.
  - Public key of StackVision server installed on each 8864.
- **Encryption & Integrity**:
  - AES-128 encryption
  - HMAC-SHA256 message signing
  - Diffie-Hellman key exchange
- **Security Note**: Public keys can be distributed over unsecured channels, but installation must be tightly controlled to prevent unauthorized devices from connecting.

### 2. Network Configuration and TCP/IP Ports
#### StackVision Server – Inbound Connections
- From SV Client: SQL Reporting Services, StackVision Client Service, Controller Emulation
- From FleetVision: Data Link
- From OPC Client: OPC/PI (if installed)

#### StackVision Server – Outbound Connections
- To Data Controllers (8832/8864): File transfer, polling, configuration compare
- To SQL Server: Database access (if remote)

#### StackVision Client – Outbound Connections
- To SQL Server: Reporting Services
- To SV Server: Client Service, Controller Emulation

#### 8832/8864 Data Controllers – Inbound Connections
- File transfer, polling, and emulation ports as configured

**Firewall Considerations**:
- No inbound firewall penetration required for secure SSH tunnel from 8864.
- Close unused ports to reduce attack surface.

### 3. Communication Alarm Standard
- **Purpose**: Detects loss of communication between StackVision and 8864 DAS.
- **Implementation**:
  - Historically via Windows Task Scheduler.
  - Preferred method: StackVision polling alarms configured in StackStudio.
  - Uses an 8864 counter channel to monitor communication.
  - Detects both network failures and StackVision core service stoppages.
- **Future Development**: Planned integration into 8864 firmware.

### 4. Diagnostic Analyzer Range Evaluation
- **Example Parameter**: S1:S1CPFLOW
- **Evaluation Metrics**:
  - Percentage of time parameter is within specified range (e.g., 20–80%).
  - Hours and percentage of total operation time in each range.
  - Statistical measures: mean, median, mode, min, max.
  - Compliance with MPC/MPF thresholds.
- **Purpose**: Identify operational anomalies and ensure process stability.

---

## Best Practices

1. **Secure Key Management**:
   - Maintain strict control over RSA key installation.
   - Regularly audit installed keys on both StackVision server and 8864 units.

2. **Firewall Configuration**:
   - Allow only necessary outbound ports from 8864 to StackVision.
   - Disable unused inbound ports on StackVision server.

3. **Alarm Configuration**:
   - Use StackVision polling alarms over OS-level schedulers for integrated monitoring.
   - Configure alarms to detect both communication loss and service failures.

4. **Performance Monitoring**:
   - Regularly run Diagnostic Analyzer Range Evaluations.
   - Investigate parameters operating outside expected ranges.

5. **Documentation & Change Control**:
   - Keep network diagrams, port usage lists, and alarm configurations up to date.
   - Document firmware versions and security configurations for each 8864.

---

## Source Attribution

- **[Document 1: Engineering Standard - 8864 DAS Communication Alarm]**  
  Provided details on communication alarm configuration using StackVision polling and 8864 counter channels, including benefits over Windows Task Scheduler.

- **[Document 2: Diagnostic Analyzer Range]**  
  Supplied methodology and statistical metrics for evaluating process parameters over time.

- **[Document 3: Setting up Secure Communications r4]**  
  Described SSH reverse tunneling setup, RSA key exchange, and firewall considerations for secure 8864–StackVision communication.

- **[Document 4: ESC Secure Communication Ports]**  
  Outlined encryption, authentication, and firewall requirements for secure StackVision communications.

- **[Document 5: TCP/IP Ports Used by a StackVision System]**  
  Detailed inbound/outbound port usage for StackVision servers, clients, and data controllers.

---

If you’d like, I can also create a **network diagram** showing the secure communication flow between StackVision, 8864 DAS, and clients, including port usage and firewall boundaries. This would make the configuration much easier to visualize. Would you like me to prepare that?

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

# Consolida...
- [[Environmental]] - ---

## Key Concepts

### StackVision
A server-bas...


## Glossary

- **8864**: Data controller platform used by engineering
