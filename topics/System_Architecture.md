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
CO₂ control charts are essential tools for monitoring, controlling, and improving emissions measurement processes in power plants and industrial facilities. They help detect variations in CO₂ concentration, identify potential system issues such as sampling system in-leakage, and ensure compliance with regulatory requirements like Subpart TTTT of the EPA’s NSPS standards. StackVision, a widely used Data Acquisition and Handling System (DAHS), provides integrated tools for generating control charts, calculating load bins, and producing compliance reports. Proper configuration of StackVision is critical to ensure accurate data collection, analysis, and reporting.

---

## Key Concepts

### Control Charts
- **Purpose**: Monitor process variation over time, differentiate between common and special causes of variation, and guide corrective actions.
- **Benefits**: Improved process consistency, reduced costs, higher quality, and enhanced capacity.
- **Application in CO₂ Monitoring**: Detects under-measurement of emissions, which can lead to regulatory penalties.

### Load Bins
- **Definition**: Categorization of plant load into discrete ranges (e.g., MW/10) for analysis.
- **Importance**: CO₂ variability is often analyzed within specific load bins to improve accuracy.

### Subpart TTTT Compliance
- **Scope**: Governs CO₂ mass emissions reporting on a 12-month rolling average basis.
- **Parameters**: CO2#/MWh and CO2KGMWH are standard reporting metrics.
- **Limits**: Typical permit limit is 1000 lb/MWh.

---

## Technical Details

### StackVision Configuration for CO₂ Control Charts
1. **Enable Load Bin Calculations**:
   - Navigate to `Configuration → StackStudio → Plant-Sources-Parameters`.
   - On the *Part 75 Settings* tab, check:
     - **Parameter Daily Record?**
     - **Load Range Enabled?**
2. **Configure Daily ProcessNow Sequence**:
   - Go to `ProcessNow → Sequences`.
   - Select the daily sequence and ensure **Task PDR** is enabled.
   - If the *Parameters* field is blank, all parameters are included; otherwise, ensure the CO₂ parameter is checked.
3. **Apply Changes**:
   - Click the *Apply* icon to update the StackVision Server.
4. **Verify Load Bin Selection**:
   - Use DataLab to check the *Load Range* field under `Fields → Part 75`.

### Data Used for Analysis
- **CO₂ Concentration**:
  - Hourly and daily averages.
  - Baseline mean and standard deviation calculated over 30 days (minimum 6 valid hours/day).
- **Load Bin Data**:
  - Load bin = MW/10 (or MW/20 for common stacks).
  - Max MW typically 750.
- **Additional Parameters**:
  - MODC (Method of Determination Code)
  - CO₂ RATA (Relative Accuracy Test Audit)

### Subpart TTTT 12-Month Average Guidelines
- **Hourly Data Rules**:
  - Use valid hourly fuel flow and load data.
  - Exclude hours with missing/invalid load or CO₂ lbs data.
- **No Load Hours**:
  - Record load as 0 with actual CO₂ lbs.
- **Startup/Shutdown**:
  - Include in calculations.
- **Rolling Average**:
  - Always include 12 operating months; look back further if months are non-operating.
- **Configuration Parameters**:
  - **CO2LBS**: `CO2T/HR × 2000 × UNITOPHR#100`
  - **LOADMWH**: `(UNITLOAD × UNITOPHR#100) + (CO2LBS × 0)`

---

## Best Practices
- **Data Validation**: Ensure all hourly data used in calculations is valid; exclude substituted or missing values.
- **Baseline Period**: Maintain a consistent 30-day baseline for control chart calculations.
- **Load Bin Accuracy**: Regularly verify load bin configurations to ensure correct categorization.
- **Regulatory Compliance**: Align StackVision configuration with Subpart TTTT requirements, including correct parameter naming and limits.
- **System Maintenance**: Periodically review DAHS sequences and parameter settings to prevent data gaps.
- **Network Configuration**: Ensure proper TCP/IP port settings for StackVision server-client communication to avoid data transfer issues.

---

## Source Attribution
- **[Document 1]**: Provided detailed StackVision configuration steps for enabling load bins and parameter daily records, as well as guidance on verifying load bin selection in DataLab.
- **[Document 2]**: Explained the purpose and benefits of control charts, identified key data sources for CO₂ analysis, and described baseline calculation methods.
- **[Document 3]**: Outlined Subpart TTTT regulatory guidelines for 12-month CO₂ mass emissions averages, including data validity rules, calculation methods, and compliance parameters.
- **[Document 4]**: Listed TCP/IP port configurations for StackVision server and client communications, relevant for ensuring uninterrupted data flow between DAHS components.

---

If you’d like, I can also create a **visual workflow diagram** showing how CO₂ data flows from measurement through StackVision configuration to control chart analysis and regulatory reporting. Would you like me to add that?