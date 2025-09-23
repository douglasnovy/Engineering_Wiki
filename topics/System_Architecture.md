---
title: System_Architecture
consolidated: true
sources: 4
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ControlCharts_CO2controlchartSVConfigurationdocx_47da83fd.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ControlCharts_StackVisionControlChartspptx_cceae59d.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**CO₂ Control Charts in StackVision: Configuration, Analysis, and Regulatory Compliance**

---

## Overview
CO₂ control charts are a critical tool within the StackVision emissions monitoring system, used to monitor, control, and improve process performance by analyzing variation in CO₂ emissions over time. They help detect anomalies such as sampling system in-leakage, which can lead to under-measurement of emissions and potential regulatory penalties. Proper configuration, data handling, and adherence to regulatory guidelines—such as those in Subpart TTTT—are essential for accurate reporting and compliance.

---

## Key Concepts

### Control Charts
- **Purpose**: Monitor process variation, distinguish between common and special causes, and guide corrective actions.
- **Benefits**:
  - Continuous process control
  - Improved consistency and predictability
  - Higher quality and lower operational costs
  - Common language for discussing process performance

### Load Bins
- **Definition**: Categorization of operational load into discrete ranges (e.g., MW/10 or MW/20 for common stacks).
- **Role in CO₂ Analysis**: CO₂ variability is assessed within load bins to ensure meaningful comparisons.

### Regulatory Context
- **Subpart TTTT**: Establishes guidelines for calculating and reporting 12-month average CO₂ mass emissions on an output basis (lb/MWh or kg/MWh).
- **Compliance Requirements**:
  - Use valid hourly fuel flow and load data
  - Exclude substituted or invalid data
  - Include startup and shutdown periods
  - Maintain rolling 12-month averages

---

## Technical Details

### Configuration in StackVision
1. **Enable Load Bin Calculations**:
   - Navigate to *Configuration → StackStudio → Plant-Sources-Parameters*.
   - On the *Part 75 Settings* tab, check:
     - **Parameter Daily Record?**
     - **Load Range Enabled?**
2. **Configure Daily ProcessNow Sequence**:
   - Go to *ProcessNow → Sequences*.
   - Select the daily sequence and ensure **Task PDR** is enabled.
   - Include the desired parameter in the PDR list.
3. **Apply Changes**:
   - Click the *Apply* icon to update the StackVision Server.
4. **Verify Load Bin Selection**:
   - Use DataLab to view the *Load Range* field under *Fields → Part 75*.

### Data Used for CO₂ Control Charts
- **CO₂ Concentration**:
  - Hourly values used as the control parameter due to low variability within load bins.
  - Daily averages calculated over 30 days (minimum 6 valid hours/day).
  - Baseline mean and standard deviation computed from the 30-day dataset.
- **Load Bin Data**:
  - Derived from MW output (MW/10 or MW/20).
  - Maximum MW typically 750.
- **Additional Parameters**:
  - MODC (Method of Determination Code)
  - CO₂ RATA (Relative Accuracy Test Audit)

### Subpart TTTT Compliance Calculations
- **CO₂LBS**:
  - Formula: `CO₂T/HR × 2000 × UNITOPHR#100`
  - No invalidation logic based on load.
- **LOADMWH**:
  - Formula: `(UNITLOAD × UNITOPHR#100) + (CO₂LBS × 0)`
  - Invalid if CO₂ is invalid.
- **UNITOPHR**:
  - Derived from OPTIME parameter for Group 0.
- **Data Validity Rules**:
  - Exclude hours with missing/invalid load or CO₂ lbs.
  - For no-load hours, use load = 0 with actual CO₂ lbs.

### Network Considerations for StackVision
- **Server Ports**:
  - Inbound: SQL Reporting Services, Data Link from FleetVision, OPC client connections, StackVision Client Service.
  - Outbound: Controller file transfer (ports 8832/8864), SQL Server connections, Controller polling.
- **Client Ports**:
  - Outbound: SQL Reporting Services, StackVision Client Service, Controller Emulation.
- **Data Controller Ports**:
  - Inbound: File transfer, emulation, configuration compare.

---

## Best Practices
1. **Maintain Accurate Configuration**:
   - Regularly verify load bin settings and PDR sequence inclusion for CO₂ parameters.
2. **Validate Data Integrity**:
   - Ensure hourly CO₂ and load data are valid before inclusion in averages.
   - Monitor for substituted or missing data to avoid compliance issues.
3. **Use Control Charts Proactively**:
   - Identify trends and anomalies early to prevent under-measurement penalties.
4. **Align with Regulatory Requirements**:
   - Follow Subpart TTTT guidelines for rolling 12-month averages.
   - Keep documentation of startup/shutdown data inclusion.
5. **Secure Network Communication**:
   - Confirm correct TCP/IP port configurations for StackVision components to ensure reliable data transfer.

---

## Source Attribution
- **[Document 1]**: Provided detailed StackVision configuration steps for enabling load bins and setting up daily sequences for CO₂ control chart reporting.
- **[Document 2]**: Explained the purpose and benefits of control charts, outlined data sources for CO₂ analysis, and described calculation methods for daily averages and load bins.
- **[Document 3]**: Detailed Subpart TTTT regulatory guidelines for calculating and reporting 12-month average CO₂ mass emissions, including data validity rules and parameter configurations.
- **[Document 4]**: Listed TCP/IP port usage for StackVision servers, clients, and data controllers, ensuring proper network setup for data collection and reporting.

---

Would you like me to also create a **visual workflow diagram** showing the relationship between configuration, data collection, control chart analysis, and regulatory reporting? This could make the process easier to follow for operators and compliance staff.

## Glossary

- **8864**: Data controller platform used by engineering
