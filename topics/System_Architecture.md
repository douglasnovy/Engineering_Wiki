---
title: System_Architecture
consolidated: true
sources: 4
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ControlCharts_CO2controlchartSVConfigurationdocx_47da83fd.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ControlCharts_StackVisionControlChartspptx_cceae59d.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

### Title
**CO₂ Control Charts in StackVision: Configuration, Analysis, and Regulatory Compliance**

---

### Overview
CO₂ control charts are a critical tool within the StackVision emissions monitoring system, used to monitor, control, and improve process performance by tracking CO₂ concentration trends over time. They help detect anomalies such as sampling system in-leakage, which can lead to under-measurement of emissions and potential regulatory penalties. Proper configuration and use of control charts ensure accurate reporting, compliance with environmental regulations (including Subpart TTTT), and optimization of plant operations.

---

### Key Concepts

1. **Control Charts Purpose**  
   - Monitor process variation over time.  
   - Differentiate between common and special causes of variation.  
   - Provide a basis for corrective actions and process improvement.  
   - Serve as a common language for discussing performance.

2. **CO₂ as a Control Parameter**  
   - CO₂ concentration is used due to its relatively low variability within a given load band.  
   - Analysis typically uses daily averages over a baseline period to establish mean and standard deviation.

3. **Load Bins**  
   - Load bins categorize operational load ranges for analysis.  
   - Typically calculated as MW/10 (or MW/20 for common stacks).  
   - Accurate load bin configuration is essential for meaningful control chart reporting.

4. **Regulatory Context (Subpart TTTT)**  
   - Requires calculation of 12-month average CO₂ mass emissions on an output basis (lb/MWh or kg/MWh).  
   - Data validity rules exclude hours with missing or invalid load or CO₂ measurements.  
   - Startup and shutdown data are included; non-operating months are replaced with prior months to maintain a 12-month dataset.

---

### Technical Details

#### Configuration in StackVision
1. **Enable Load Bin Calculations**  
   - Navigate to *Configuration → StackStudio → Plant-Sources-Parameters*.  
   - On the *Part 75 Settings* tab, check **Parameter Daily Record?** and **Load Range Enabled?** for the CO₂ parameter.  

2. **Include Parameter in Daily Sequence**  
   - Go to *ProcessNow → Sequences*.  
   - Select the daily sequence and ensure **Task PDR** is enabled.  
   - Verify the CO₂ parameter is included in the PDR list.

3. **Apply Changes**  
   - Save and apply changes to the StackVision Server.

4. **Verify Load Bin Selection**  
   - Use DataLab to check the Load Range field under *Fields → Part 75*.

#### Data Analysis Workflow
- **Daily CO₂ Averages**:  
  - At least 6 valid hours per day are required.  
  - Baseline: 30 days of daily averages.  
  - Calculate mean and standard deviation for control limits.

- **Load Bin Data**:  
  - Derived from MW readings; bin size depends on configuration.  
  - Used to segment CO₂ data for more precise control charting.

- **Data Sources**:  
  - Hourly CO₂ concentration (primary control parameter).  
  - MODC (Method of Determination Code).  
  - CO₂ RATA (Relative Accuracy Test Audit) results.

#### Regulatory Calculation (Subpart TTTT)
- **Hourly CO₂ lbs**:  
  - Derived from hourly fuel flow data; exclude invalid or substituted data.  
- **Load MWh**:  
  - Calculated from unit load and operating hours; invalid if CO₂ data is invalid.  
- **12-Month Average**:  
  - Rolling average over 12 operating months; replace non-operating months with prior months.  
- **Permit Limits**:  
  - Commonly 1000 lb/MWh; parameters CO2#/MWH and CO2KGMWH configured in StackVision.

---

### Best Practices

1. **Ensure Complete and Valid Data**  
   - Avoid missing or substituted data for both load and CO₂ parameters.  
   - Validate data before running control chart reports.

2. **Maintain Accurate Configuration**  
   - Regularly verify load bin settings and PDR sequence inclusion.  
   - Confirm baseline period data meets validity requirements.

3. **Integrate Regulatory Requirements**  
   - Align control chart analysis with Subpart TTTT data validity rules.  
   - Monitor rolling 12-month averages against permit limits.

4. **Use Control Charts for Proactive Maintenance**  
   - Investigate deviations promptly to prevent compliance issues.  
   - Detect sampling system in-leakage early to avoid under-reporting emissions.

---

### Source Attribution
- **[Document 1]**: Provided detailed StackVision configuration steps for enabling load bins and including CO₂ parameters in daily sequences; guidance on verifying load bin selection in DataLab.  
- **[Document 2]**: Explained the purpose and benefits of control charts; outlined data sources, baseline calculations, and load bin methodology; highlighted CO₂’s suitability as a control parameter.  
- **[Document 3]**: Detailed Subpart TTTT regulatory requirements for CO₂ mass emissions reporting, including data validity rules, calculation methods, and permit limits.  
- **[Document 4]**: Contained TCP/IP port usage for StackVision systems (not directly relevant to CO₂ control charts but important for system connectivity and configuration integrity).

---

If you’d like, I can also integrate **Document 4’s TCP/IP port mapping** into a separate “System Connectivity” section so this consolidated guide covers both **CO₂ control chart usage** and **StackVision network configuration** for a complete operational reference. Would you like me to do that?