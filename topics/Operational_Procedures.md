---
title: Operational_Procedures
consolidated: true
sources: 7
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_ConfigurePMDAILYAVGProcessNowTaskforRegulation6048Dafdocx_3992f4be.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CopyReportsrsscripter_RSScripterProceduredocx_b431424a.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_LoggerReconciliation_ProcessforEngineeringLoggerReconciliationsMay2019docx_9734c828.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ExternalDOC-csmm_8_implementation___lesson_learned_standardspdf_2143f765.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PaDEPProcessGuidexlsx_e36a4dcc.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ProcessCodesforPaDEPEDRmaptoReasonCodesinStackVisionasdodocx_117b25f1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md']  # This would be a timestamp
---

### Title
**Comprehensive Guide to Environmental Monitoring System Configuration, Data Management, and Regulatory Compliance**

---

### Overview
This consolidated guide provides technical procedures, configuration standards, and best practices for managing Continuous Emission Monitoring Systems (CEMS) and associated data workflows. It integrates processes for logger reconciliation, report transfer, regulatory-specific task configuration, and compliance with Pennsylvania Department of Environmental Protection (PaDEP) Revision 8 and federal regulations such as 40 CFR Part 60 Subpart Da and Subpart TTTT. The goal is to ensure accurate data capture, seamless system updates, and adherence to environmental reporting requirements.

---

### Key Concepts

1. **Logger Reconciliation**  
   Capturing a complete snapshot of a logger’s configuration before updates or upgrades to prevent data loss and maintain operational integrity.

2. **Report Transfer via RSScripter**  
   Using RSScripter.exe to migrate or duplicate SQL-based reports between servers or units, ensuring consistent reporting across environments.

3. **Regulatory-Specific Task Configuration**  
   Setting up calculation tasks (e.g., PMDAILYAVG) to comply with specific environmental regulations, including data validity checks and alarm triggers.

4. **PaDEP Revision 8 Compliance**  
   Implementing monitoring plans, validating data, and mapping process/method codes between PaDEP EDR and StackVision for accurate reporting.

5. **CO2 Mass Emissions 12-Month Average (Subpart TTTT)**  
   Configuring parameters and calculations to meet CO2 emission limits and reporting requirements based on continuous operational data.

---

### Technical Details

#### 1. Logger Reconciliation Procedure
- **Pre-Reconciliation Steps**:
  - Record network details (IP, subnet mask, gateway).
  - Access controller via PuTTY/Telnet (8832: Telnet/PuTTY, 8864: PuTTY).
  - Log in with integrator-level credentials.
  - Navigate to *Configuration → System Parameters* and document settings.
- **Configuration Capture**:
  - Use StackStudio to snapshot current settings.
  - Ensure all critical parameters are backed up before firmware or hardware changes.

#### 2. RSScripter Report Transfer
- **Requirements**:
  - .NET 3.5 enabled on the server.
  - Run RSScripter.exe on the SQL report server (especially for split-server setups).
- **Procedure**:
  - Launch RSScripter.exe, set report server version, retrieve catalog.
  - Select and script desired reports to an output folder.
  - Edit `RS Scripter Load All Items.cmd` to set correct paths for script location and RS.EXE.
  - Update `.rss` files for unit-specific report sources if needed.

#### 3. PMDAILYAVG Task Configuration (Regulation 60.48Da(f))
- **System Resources**:
  - `DAY_EXCLUDE_CENTRAL_SITE_PARAMETER = TH`
- **Channel Settings**:
  - Type: 6 – Block Average
  - Percent Valid Required: 1%
  - Alarm on exceedance: Enabled
  - Standard Limit Operator: `>` or `>=` (based on rounding preference)
- **Condition Manager**:
  - Mark PM parameter as missing/invalid if `Time Online` equals 0.
- **Execution Order**:
  - Condition Manager task → DAYROLLAVG task → PMDAILYAVG task.
- **Alarm Messages**:
  - Enable `EXCEALM` for exceedance alerts.

#### 4. PaDEP Revision 8 Implementation
- **Process Flow**:
  - Request facility file access.
  - Evaluate and migrate monitoring plans via CEMDPS.
  - Perform error checks and implement configuration changes per PaDEP Rev8.
  - Generate and validate EDR data with correct process, monitoring, and method codes.
- **Code Mapping**:
  - Map PaDEP EDR process codes to StackVision reason codes.
  - Map monitor codes to action codes and method codes consistently.

#### 5. Subpart TTTT CO2 Emissions Guidelines
- **Hourly Data Rules**:
  - Use valid hourly fuel flow and load data.
  - Exclude hours with missing/invalid load or substituted fuel flow.
- **12-Month Average Calculation**:
  - Include startup/shutdown data.
  - Always maintain 12 operating months in the average (look back for non-operating months).
- **Parameter Configuration**:
  - `CO2LBS`: `(CO2T/HR * 2000 * UNITOPHR#100)`
  - `LOADMWH`: `(UNITLOAD * UNITOPHR#100)`
  - Ensure invalid CO2 invalidates load for daily/monthly totals.
- **Permit Limits**:
  - Typical limit: 1000 lb/MWh.

---

### Best Practices

- **Pre-Change Documentation**: Always perform logger reconciliation before any update or upgrade.
- **Validation First**: Run data validity checks before executing regulatory calculation tasks.
- **Execution Order Discipline**: Maintain strict task execution sequences to ensure accurate averages and compliance.
- **Consistent Code Mapping**: Use standardized mappings between PaDEP and StackVision to avoid reporting errors.
- **Data Integrity in Transfers**: When using RSScripter, verify paths and report sources to prevent broken links or incorrect data.
- **Regulatory Awareness**: Stay updated on both state (PaDEP) and federal (EPA) requirements to ensure configurations meet current standards.

---

### Source Attribution

- **[Document 1] Shaun Ellis**: Detailed PMDAILYAVG task configuration for Regulation 60.48Da(f), including Condition Manager setup and execution order.
- **[Document 2] Brian Perlov**: Step-by-step procedure for using RSScripter.exe to transfer reports between servers/units.
- **[Document 3] Carl Reid**: Logger reconciliation process, pre-reconciliation steps, and configuration capture methods.
- **[Document 4] Eric Swisher (All4 Inc.)**: PaDEP Rev8 background, implementation process, and LMESE standards.
- **[Document 5] Unknown**: PaDEP transition guide workflow from monitoring plan evaluation to EDR generation.
- **[Document 6] Ashley Partington**: Mapping of PaDEP EDR process/method codes to StackVision codes.
- **[Document 7] Information Systems Group**: Subpart TTTT CO2 mass emissions 12-month average calculation guidelines and configuration parameters.

---

Would you like me to also create a **visual workflow diagram** that shows the relationship between logger reconciliation, report transfer, regulatory task execution, and compliance validation? This could make the process easier to follow for engineers.

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - It integrates processes for logger reconciliation,...
- [[Environmental]] - The goal is to ensure accurate data capture, seaml...
- [[Environmental]] - , PMDAILYAVG) to comply with specific environmenta...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
