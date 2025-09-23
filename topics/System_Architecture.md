---
title: System_Architecture
consolidated: true
sources: 4
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ControlCharts_CO2controlchartSVConfigurationdocx_47da83fd.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ControlCharts_StackVisionControlChartspptx_cceae59d.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**CO₂ Control Charts and StackVision Configuration for Emissions Monitoring and Compliance**

---

## Overview
CO₂ control charts are a critical tool in emissions monitoring systems, enabling operators to detect process variation, identify potential equipment issues such as sampling system in-leakage, and ensure compliance with regulatory limits. Within the StackVision platform, proper configuration of parameters, load bins, and data sequences is essential for generating accurate control chart reports. These charts support both operational optimization and adherence to regulations such as Subpart TTTT, which governs CO₂ mass emissions and output-based standards.

---

## Key Concepts

### Control Charts
- **Purpose**: Monitor, control, and improve process performance over time by studying variation and its sources.
- **Functions**:
  - Detect and monitor process variation.
  - Differentiate between common and special causes of variation.
  - Provide a basis for corrective actions.
  - Enable consistent, predictable process performance.
  - Serve as a common language for discussing process metrics.

### CO₂ as a Control Parameter
- CO₂ concentration is used due to its relatively low variability within a given load band.
- Analysis typically involves daily averages, baseline means, and standard deviations over a defined period.

### Load Bins
- Load bins categorize operational load ranges for analysis.
- Common calculation: Load bin = MW/10 (or MW/20 for common stacks).
- Accurate load bin configuration is essential for meaningful control chart data.

### Regulatory Context – Subpart TTTT
- Governs CO₂ mass emissions and output-based standards.
- Requires 12-month rolling averages of CO₂ emissions per MWh.
- Specifies data validity rules and inclusion/exclusion criteria for hourly data.

---

## Technical Details

### StackVision Configuration for CO₂ Control Charts
1. **Enable Load Bin Calculations**:
   - Navigate to *Configuration → StackStudio → Plant-Sources-Parameters*.
   - On the *Part 75 Settings* tab, check:
     - **Parameter Daily Record?**
     - **Load Range Enabled?**
2. **Configure Daily Sequence (PDR Step)**:
   - Go to *ProcessNow → Sequences*.
   - Select the daily sequence and ensure **Task PDR** is enabled.
   - Include the desired parameter in the PDR list (or leave blank to include all).
3. **Apply Changes**:
   - Click the apply icon to update the StackVision Server.
4. **Verify Load Bin Selection**:
   - Use DataLab to check the *Load Range* field under *Fields → Part 75*.

### Data Requirements for Control Chart Analysis
- **CO₂ Concentration**:
  - Hourly data used as control parameter.
  - Daily averages require ≥6 valid hours per day.
- **Load Bin Data**:
  - Derived from MW measurements.
- **Baseline Calculations**:
  - Mean and standard deviation over 30 days of valid data.
- **Additional Data**:
  - Method of Determination Code (MODC).
  - CO₂ Relative Accuracy Test Audit (RATA) results.

### Subpart TTTT Compliance Guidelines
- **Hourly CO₂ lbs Calculation**:
  - Based on hourly fuel flow data.
  - Exclude hours with missing/invalid load or CO₂ data.
- **Load MWh Calculation**:
  - Invalid if CO₂ data is invalid.
- **12-Month Rolling Average**:
  - Includes startup/shutdown data.
  - Must always cover 12 operating months (look back if months are non-operating).
- **Permit Limits**:
  - Commonly 1000 lb/MWh.
- **Data Entry**:
  - Annual Energy Sold and Potential Electric Output must be entered manually in EDR XML.

### StackVision Network Configuration (TCP/IP Ports)
- **Server Inbound Ports**:
  - SQL Reporting Services, FleetVision Data Link, OPC/PI (if installed), StackVision Client Service.
- **Server Outbound Ports**:
  - Controller file transfer (8832/8864), SQL Server connections, Controller polling.
- **Client Outbound Ports**:
  - SQL Reporting Services, StackVision Client Service, Controller Emulation.
- **Data Controller Ports**:
  - File transfer and emulation ports (8832/8864).

---

## Best Practices
1. **Ensure Parameter Configuration**:
   - Verify that all relevant CO₂ parameters have load bin calculations enabled.
2. **Maintain Data Validity**:
   - Follow Subpart TTTT rules for excluding invalid or substituted data.
3. **Regularly Review Control Charts**:
   - Identify trends or anomalies early to prevent compliance issues.
4. **Document Baseline Periods**:
   - Keep clear records of baseline mean and standard deviation calculations.
5. **Secure Network Communication**:
   - Confirm correct TCP/IP port configurations for StackVision components to ensure reliable data transfer.
6. **Integrate Regulatory Checks**:
   - Align control chart monitoring with permit limits and regulatory reporting requirements.

---

## Source Attribution
- **Document 1**: Provided detailed StackVision configuration steps for enabling load bins, setting up daily sequences, and verifying load range data for CO₂ control charts.
- **Document 2**: Explained the purpose and functions of control charts, outlined data requirements, and described baseline calculation methods for CO₂ analysis.
- **Document 3**: Detailed Subpart TTTT compliance guidelines, including data validity rules, calculation methods for CO₂ lbs and load MWh, and 12-month rolling average requirements.
- **Document 4**: Listed TCP/IP port configurations for StackVision servers, clients, and data controllers, ensuring proper network communication for emissions monitoring systems.

---

Would you like me to also create a **visual workflow diagram** showing the relationship between StackVision configuration, data collection, control chart generation, and regulatory compliance? This could make the process easier to follow for operators.

## Glossary

- **8864**: Data controller platform used by engineering
