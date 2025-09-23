---
title: System_Architecture
consolidated: true
sources: 4
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ControlCharts_CO2controlchartSVConfigurationdocx_47da83fd.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ControlCharts_StackVisionControlChartspptx_cceae59d.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**CO₂ Control Chart Configuration, Analysis, and Compliance in StackVision Systems**

---

## Overview
CO₂ control charts are essential tools for monitoring, controlling, and improving emissions measurement processes in power generation and industrial facilities. Within the StackVision platform, control charts help detect process variation, identify potential issues such as sampling system in-leakage, and ensure compliance with regulatory requirements, including Subpart TTTT 12-month CO₂ mass emissions guidelines. Proper configuration, accurate data handling, and adherence to best practices are critical for reliable reporting and avoiding costly penalties.

---

## Key Concepts

### Control Charts
- **Purpose**: Monitor process performance over time by studying variation and its sources.
- **Functions**:
  - Detect and monitor process variation.
  - Differentiate between common and special causes of variation.
  - Provide a basis for process improvement and consistent performance.
  - Serve as a common language for discussing process metrics.

### CO₂ Parameters in StackVision
- **Primary Data Sources**:
  - Hourly and daily CO₂ concentration.
  - Load bin data (based on MW output).
  - Method of Determination Code (MODC).
  - CO₂ Relative Accuracy Test Audit (RATA) results.
- **Load Bins**: Typically calculated as MW/10 (or MW/20 for common stacks), with maximum MW values defined per facility.

### Regulatory Context
- **Subpart TTTT Guidelines**:
  - Use hourly fuel flow data to calculate CO₂ lbs.
  - Exclude data with missing or invalid load or CO₂ values.
  - Include startup and shutdown data.
  - Maintain a rolling 12-month average based on operating months.
  - Typical permit limit: 1000 lb/MWh.

---

## Technical Details

### Configuration in StackVision
1. **Enable Load Bin Calculations**:
   - Navigate to *Configuration → StackStudio → Plant-Sources-Parameters*.
   - On the *Part 75 Settings* tab, check:
     - **Parameter Daily Record?**
     - **Load Range Enabled?**
2. **Include Parameter in Daily ProcessNow Sequence**:
   - Go to *ProcessNow → Sequences*.
   - Select the daily sequence and ensure **Task PDR** is enabled.
   - If the *Parameters* field is blank, all parameters are included; otherwise, explicitly check the desired parameter.
3. **Apply Changes**:
   - Click the *Apply* icon to update the StackVision Server.

### Data Analysis Workflow
- **Daily CO₂ Averages**:
  - Use DataLab’s *Average Data Reports* to calculate daily averages (minimum 6 valid hours/day).
- **Baseline Calculations**:
  - Mean and standard deviation over a 30-day baseline period.
- **Load Bin Assignment**:
  - Verify correct load bin selection via DataLab (*Fields → Part 75 → Load Range*).

### Subpart TTTT Compliance Calculations
- **CO₂LBS**: `CO₂T/HR × 2000 × UNITOPHR#100`
- **LOADMWH**: `(UNITLOAD × UNITOPHR#100) + (CO₂LBS × 0)`
- **UNITOPHR**: Derived from OPTIME parameter for Group 0.
- **Invalid Data Rules**:
  - Exclude hours with invalid or substituted fuel flow or load data.
  - No logic for CO₂LBS invalidity based on load (load never invalid).

### Network and System Considerations
- StackVision servers and clients use specific TCP/IP ports for data transfer, reporting, and controller communication.
- Ensure proper port configuration for:
  - SQL Reporting Services.
  - Data Controller polling and file transfer (ports 8832 or 8864).
  - FleetVision data links.
  - OPC/PI connections (if installed).

---

## Best Practices

1. **Data Integrity**:
   - Regularly verify load bin assignments and baseline calculations.
   - Lock previous quarters only after confirming data accuracy.
2. **Regulatory Compliance**:
   - Maintain complete and valid hourly datasets for CO₂ and load.
   - Track rolling 12-month averages per Subpart TTTT requirements.
3. **System Configuration**:
   - Keep StackVision sequences and parameters updated.
   - Ensure TCP/IP ports are correctly configured for all components.
4. **Performance Monitoring**:
   - Use control charts to detect anomalies early.
   - Investigate special cause variations promptly to prevent compliance issues.
5. **Documentation**:
   - Record configuration changes and analysis results for audit readiness.

---

## Source Attribution
- **[Document 1]**: Provided detailed StackVision configuration steps for enabling load bin calculations and including parameters in daily sequences; guidance on verifying load bin selection in DataLab.
- **[Document 2]**: Explained the purpose and functions of control charts, outlined CO₂ data analysis methods, baseline calculations, and load bin definitions.
- **[Document 3]**: Detailed Subpart TTTT regulatory guidelines for CO₂ mass emissions, including calculation methods, data validity rules, and compliance requirements.
- **[Document 4]**: Listed TCP/IP port usage for StackVision servers, clients, and controllers, ensuring proper network configuration for data flow and reporting.

---

If you’d like, I can create a **visual workflow diagram** showing the end-to-end process from CO₂ data collection to control chart analysis and regulatory reporting. This would make the consolidated knowledge base entry more actionable for operators and compliance teams. Would you like me to add that?

## Glossary

- **8864**: Data controller platform used by engineering
