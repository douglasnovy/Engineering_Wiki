---
title: System_Architecture
consolidated: true
sources: 4
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ControlCharts_CO2controlchartSVConfigurationdocx_47da83fd.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ControlCharts_StackVisionControlChartspptx_cceae59d.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**CO₂ Control Charts and StackVision Configuration Guidelines**

---

## Overview
Control charts are a critical tool for monitoring, controlling, and improving process performance in emissions measurement systems. In the context of CO₂ emissions monitoring, they help detect anomalies such as sampling system in-leakage, which can lead to under-measurement of emissions and potential regulatory penalties. StackVision, a widely used data acquisition and handling system (DAHS), provides integrated tools for generating CO₂ control charts, calculating load bins, and ensuring compliance with regulatory standards such as Subpart TTTT of the EPA regulations.

This consolidated guide outlines the purpose and use of CO₂ control charts, the configuration steps required in StackVision, the data sources and calculations involved, and best practices for maintaining accurate and compliant emissions reporting.

---

## Key Concepts

### Control Charts
- **Purpose**: Monitor process variation over time, differentiate between common and special causes of variation, and guide corrective actions.
- **Benefits**:
  - Detect and monitor process variation
  - Provide ongoing process control
  - Improve process consistency and predictability
  - Reduce costs and increase capacity
  - Serve as a common language for process performance discussions

### CO₂ Emissions Monitoring
- **Parameters**: CO₂ concentration, load bin data, Method of Determination Code (MODC), CO₂ Relative Accuracy Test Audit (RATA)
- **Load Bins**: Grouping of operational load ranges for analysis; typically calculated as MW/10 (or MW/20 for common stacks)
- **Regulatory Context**: Subpart TTTT requires accurate calculation of CO₂ mass emissions and output-based averages over a rolling 12-month period.

---

## Technical Details

### StackVision Configuration for CO₂ Control Charts
1. **Enable Load Bin Calculations**:
   - Navigate to `Configuration → StackStudio → Plant-Sources-Parameters`.
   - Select the CO₂ parameter.
   - On the *Part 75 Settings* tab, check:
     - **Parameter Daily Record?**
     - **Load Range Enabled?**
2. **Configure Daily ProcessNow Sequence**:
   - Go to `ProcessNow → Sequences`.
   - Select the daily sequence.
   - Ensure **Task PDR** is enabled.
   - Include the CO₂ parameter in the PDR list.
3. **Apply Changes**:
   - Click the *Apply* icon to update the StackVision Server.
4. **Verify Load Bin Selection**:
   - Use DataLab to check the *Load Range* field under `Fields → Part 75`.

### Data Used for CO₂ Control Chart Analysis
- **Hourly CO₂ Concentration**:
  - Low variability within load bands; used as control parameter.
- **Daily Average CO₂ Concentration**:
  - Calculated over 30 days (minimum 6 valid hours/day).
  - Baseline mean and standard deviation derived from this dataset.
- **Load Bin Data**:
  - Derived from MW output; max MW typically 750.
- **Other Inputs**:
  - MODC codes, CO₂ RATA results.

### Subpart TTTT Compliance Guidelines
- **Hourly Calculations**:
  - Use hourly fuel flow to compute CO₂ lbs.
  - Exclude hours with missing/invalid load or CO₂ data.
- **No Load Hours**:
  - Record load as 0 with actual CO₂ lbs.
- **Rolling 12-Month Average**:
  - Include startup/shutdown data.
  - Replace non-operating months with earlier operating months to maintain 12-month dataset.
- **Limits**:
  - Typical permit limit: 1000 lb/MWh.
- **Parameters**:
  - CO2#/MWH and CO2KGMWH configured in StackVision.
- **Data Entry**:
  - Annual Energy Sold and Annual Potential Electric Output must be entered manually in EDR XML.

---

## Best Practices
- **Ensure Proper Configuration**: Verify load bin calculations and PDR sequence settings before running control chart reports.
- **Validate Data Integrity**: Regularly check for missing or invalid data in both CO₂ and load parameters.
- **Maintain Baseline Accuracy**: Recalculate baseline mean and standard deviation periodically to reflect current operating conditions.
- **Regulatory Compliance**: Follow Subpart TTTT guidelines for data inclusion/exclusion and rolling averages.
- **Network Configuration**: Ensure StackVision server and client TCP/IP ports are correctly configured for data communication (see Source Attribution for port details).
- **Documentation**: Keep detailed records of configuration changes and data validation steps for audit readiness.

---

## Source Attribution
- **[Document 1: CO₂ Control Chart SV Configuration]**: Provided detailed StackVision configuration steps for enabling load bin calculations, setting up daily sequences, and verifying load bin selection.
- **[Document 2: StackVision Control Charts]**: Explained the purpose and benefits of control charts, identified data sources for CO₂ analysis, and described calculation methods for daily averages and load bins.
- **[Document 3: Subpart TTTT Guidelines]**: Outlined regulatory requirements for CO₂ mass emissions calculations, data validity rules, rolling 12-month average methodology, and parameter configuration for compliance.
- **[Document 4: TCP/IP Ports Used by StackVision]**: Listed inbound and outbound TCP/IP port configurations for StackVision servers, clients, and data controllers, ensuring proper network communication for emissions data handling.

---

Would you like me to also integrate the **TCP/IP port configuration table** from Document 4 directly into this guide for quick reference? That would make it a single-source operational document covering both emissions monitoring and system connectivity.