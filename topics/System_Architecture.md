---
title: System_Architecture
consolidated: true
sources: 4
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ControlCharts_CO2controlchartSVConfigurationdocx_47da83fd.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ControlCharts_StackVisionControlChartspptx_cceae59d.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

# CO2 Control Charts and StackVision System Configuration

## Overview
Control charts are a critical tool for monitoring, controlling, and improving process performance in emissions monitoring systems. In the context of CO2 emissions, they help detect anomalies such as sampling system in-leakage, which can lead to under-measurement of emissions and potential regulatory penalties. StackVision, a data acquisition and handling system (DAHS), provides built-in capabilities for generating CO2 control charts, calculating load bins, and ensuring compliance with regulatory requirements such as Subpart TTTT for CO2 mass emissions.

This consolidated guide covers:
- The purpose and use of CO2 control charts
- Data requirements and calculation methods
- Configuration steps in StackVision
- Regulatory compliance considerations
- Network communication requirements for StackVision systems

---

## Key Concepts

### Control Charts
- **Purpose**: Monitor process variation over time, distinguish between common and special causes, and guide corrective actions.
- **Benefits**: Improved process consistency, predictability, quality, and capacity; reduced costs; common language for performance discussions.
- **Application in CO2 Monitoring**: Detects deviations in CO2 concentration that may indicate equipment or process issues.

### Load Bins
- **Definition**: Groupings of operating load (e.g., MW/10) used to normalize CO2 data for analysis.
- **Importance**: Ensures comparisons are made under similar operating conditions, improving the reliability of control chart analysis.

### Regulatory Context (Subpart TTTT)
- **12-Month Average**: Rolling average of CO2 mass emissions on an output basis (lb/MWh or kg/MWh).
- **Data Validity Rules**: Exclude hours with missing/invalid load or CO2 data; include startup/shutdown; always maintain 12 operating months in the average.
- **Typical Limit**: 1000 lb/MWh for CO2 emissions.

---

## Technical Details

### Data Used for CO2 Control Charts
- **Primary Parameters**:
  - Hourly CO2 concentration (low variability within a load bin)
  - Load bin data
  - Method of Determination Code (MODC)
  - CO2 Relative Accuracy Test Audit (RATA) results
- **Calculations**:
  - Daily average CO2 concentration (minimum 6 valid hours/day)
  - 30-day baseline mean and standard deviation
- **Load Bin Calculation**:
  - Load bin = MW/10 (or MW/20 for common stacks)
  - Maximum MW example: 750 MW

### StackVision Configuration for CO2 Control Charts
1. **Enable Load Bin Calculations**:
   - In StackStudio: `Plant → Sources → Parameters`
   - On *Part 75 Settings* tab: check `Parameter Daily Record?` and `Load Range Enabled?`
2. **Configure Daily ProcessNow Sequence**:
   - In StackStudio: `ProcessNow → Sequences`
   - Select daily sequence; ensure `Task PDR` is enabled
   - Include desired parameters in PDR list
3. **Apply Changes**:
   - Click the apply icon to update the StackVision server
4. **Verify Load Bin Selection**:
   - Use DataLab to view the `Load Range` field for the parameter

### Subpart TTTT Configuration Parameters
- **CO2LBS**: `CO2T/HR * 2000 * UNITOPHR#100`
- **LOADMWH**: `(UNITLOAD * UNITOPHR#100) + (CO2LBS * 0)`
- **UNITOPHR**: OPTIME parameter for Group 0
- **Data Exclusion Rules**: No invalidation of CO2LBS based on load; LOADMWH invalid if CO2 is invalid

### StackVision Network Communication
- **Server Inbound Ports**:
  - SQL Reporting Services
  - Data link from FleetVision
  - OPC/PI (if installed)
  - StackVision Client Service
  - Controller emulation from SV Client
- **Server Outbound Ports**:
  - Controller file transfer: 8832 or 8864
  - Controller emulation/configuration compare: 8864
  - SQL Server (if remote)
  - Controller polling: 8832 or 8864
- **Client Outbound Ports**:
  - SQL Reporting Services
  - StackVision Client Service
  - Controller emulation to SV Server

---

## Best Practices
- **Data Integrity**: Ensure all relevant parameters are enabled and included in daily processing sequences.
- **Load Bin Accuracy**: Regularly verify load bin assignments in DataLab to avoid skewed control chart results.
- **Regulatory Compliance**: Follow Subpart TTTT data validity rules strictly; maintain documentation for audits.
- **Baseline Updates**: Periodically review and update baseline periods for control charts to reflect current operating conditions.
- **Network Configuration**: Maintain proper firewall and port configurations to ensure uninterrupted data flow between StackVision components.
- **Preventive Monitoring**: Use control charts proactively to detect early signs of system in-leakage or other anomalies.

---

## Source Attribution
- **[Document 1: CO2 control chart SV Configuration]**: Provided detailed StackVision configuration steps for enabling load bins, setting up daily sequences, and verifying parameter inclusion for CO2 control charts.
- **[Document 2: StackVision Control Charts]**: Explained the purpose and benefits of control charts, described data requirements, and outlined calculation methods for CO2 analysis.
- **[Document 3: Subpart TTTT Guidelines]**: Supplied regulatory requirements for 12-month CO2 mass emission averages, data validity rules, and parameter configuration details.
- **[Document 4: TCP/IP Ports Used by StackVision]**: Listed network communication requirements and port configurations for StackVision servers, clients, and controllers.

---

Would you like me to also create a **visual workflow diagram** showing the relationship between data collection, control chart generation, and regulatory compliance in StackVision? This could make the process easier to follow for operators and compliance staff.

## Glossary

- **8864**: Data controller platform used by engineering
