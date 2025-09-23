---
title: Operational_Procedures
consolidated: true
sources: 7
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_ConfigurePMDAILYAVGProcessNowTaskforRegulation6048Dafdocx_3992f4be.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CopyReportsrsscripter_RSScripterProceduredocx_b431424a.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_LoggerReconciliation_ProcessforEngineeringLoggerReconciliationsMay2019docx_9734c828.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ExternalDOC-csmm_8_implementation___lesson_learned_standardspdf_2143f765.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PaDEPProcessGuidexlsx_e36a4dcc.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ProcessCodesforPaDEPEDRmaptoReasonCodesinStackVisionasdodocx_117b25f1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md']  # This would be a timestamp
---

### Title
**Consolidated Guide to Environmental Monitoring System Configuration, Data Management, and Regulatory Compliance**

---

### Overview
This consolidated guide provides technical procedures, configuration standards, and best practices for managing Continuous Emissions Monitoring Systems (CEMS), Data Acquisition and Handling Systems (DAHS), and related reporting tools in compliance with U.S. EPA and state-specific regulations such as 40 CFR Part 60 Subpart Da and Pennsylvania Department of Environmental Protection (PaDEP) Continuous Source Monitoring Manual (CSMM) Revision 8.  
It integrates operational tasks including logger reconciliation, daily average particulate matter (PM) calculations, CO₂ mass emissions averaging, report migration between systems, and regulatory data mapping, ensuring accurate data capture, validation, and reporting.

---

### Key Concepts

1. **Continuous Emissions Monitoring Systems (CEMS)**  
   Automated systems that measure pollutant emissions from stationary sources continuously, providing data for compliance with environmental regulations.

2. **Data Acquisition and Handling System (DAHS)**  
   Software and hardware that collect, process, and store CEMS data, apply calculations, and generate regulatory reports.

3. **Logger Reconciliation**  
   A process to capture the current configuration of a data logger before updates or upgrades to prevent loss of critical operational settings.

4. **Daily Average Calculations (PMDAILYAVG)**  
   Procedures to compute daily averages for particulate matter emissions, ensuring compliance with specific regulatory limits.

5. **Lowest Monitored Emission Standard Equivalent (LMESE)**  
   A calculated value representing the lowest emission standard in terms of analyzer output, used for calibration drift checks.

6. **CO₂ Mass Emissions 12-Month Average**  
   A rolling average calculation of CO₂ emissions over 12 operating months, used to demonstrate compliance with Subpart TTTT limits.

7. **Report Migration (RSScripter)**  
   The process of transferring report definitions between servers or units, ensuring consistent reporting formats and configurations.

---

### Technical Details

#### 1. PMDAILYAVG ProcessNow Task Configuration (40 CFR 60.48Da(f))
- **System Resources**:  
  `DAY_EXCLUDE_CENTRAL_SITE_PARAMETER = TH`
- **Server Channels**:  
  - Channel Type: 6 – Block Average  
  - Percent Valid Required: 1  
  - Trigger Alarm on Exceedance: True  
  - Time Weight: N  
  - Standard Limit Operator: `>` or `>=` (based on rounding preference)  
  - Standard Limit: *x.xxxx*
- **Condition Manager**:  
  Create or update a Condition Manager to mark PM parameters as *Missing* and *Invalid* when `Time Online` equals 0.
- **Execution Order**:  
  - Run Condition Manager task before PMDAILYAVG task.  
  - Ensure DAYROLLAVG tasks exclude PM parameters or run before PMDAILYAVG.
- **Command Example**:  
  `PMDAILYAVG –s SITE NAME –p PARAMETER NAME –r`
- **Alarm Messages**:  
  Enable `EXCEALM` for exceedance alarms.

#### 2. Logger Reconciliation Procedure
- **Pre-Reconciliation**:  
  - Record network details (IP, subnet mask, gateway).  
  - Access controller via PuTTY/Telnet (8832 via Telnet/PuTTY, 8864 via PuTTY).  
  - Log in with integrator-level credentials.  
  - Navigate to Configuration → System Parameters and record settings.
- **Configuration Capture**:  
  Use StackStudio to snapshot current logger configuration before updates.

#### 3. PaDEP CSMM Rev 8 Implementation
- **CEMDPS Access**:  
  Use GreenPort web portal for monitoring plan submission, testing, and certification.
- **Migration Error Check**:  
  Validate facility emission standards, analyzer details, and measurement basis.
- **LMESE Calculation**:  
  Default = Full Scale ÷ 2; exceptions for opacity, CO₂, O₂, and certain VFR cases.
- **Process Guide Steps**:  
  - Evaluate monitoring plans and petitions.  
  - Migrate corrected plans to CEMDPS.  
  - Deploy plans to DAHS.  
  - Validate data and implement configuration changes per Rev 8 requirements.  
  - Generate and validate PaDEP EDR files with correct process, monitor, method, and reason codes.

#### 4. CO₂ Mass Emissions 12-Month Average (Subpart TTTT)
- **Hourly Data Rules**:  
  - Use valid hourly fuel flow and load data.  
  - Exclude hours with missing/invalid load or substituted fuel flow.  
  - Include startup/shutdown hours with load = 0 and actual CO₂ lbs.
- **Rolling Average**:  
  Always include 12 operating months; look back further if months are non-operating.
- **Configuration Parameters**:  
  - `CO2LBS` = CO₂ tons/hr × 2000 × `UNITOPHR#100`  
  - `LOADMWH` invalid if CO₂ invalid.  
  - `UNITOPHR` from Group 0 OPTIME parameter.
- **Permit Limits**:  
  Typically 1000 lb/MWh.

#### 5. Report Migration via RSScripter
- **Prerequisites**:  
  - Enable .NET 3.5 features.  
  - Run RSScripter.exe on SQL report server.
- **Procedure**:  
  - Launch RSScripter.exe → Options → Report settings.  
  - Select latest Report Server version.  
  - Retrieve catalog, select reports, set output folder.  
  - Edit `RS Scripter Load All Items.cmd` to set script and RS.EXE paths.  
  - Modify `.rss` files for unit name changes if needed.

---

### Best Practices
- **Pre-Change Snapshots**: Always perform logger reconciliation before firmware or hardware changes.
- **Task Sequencing**: Maintain correct execution order for Condition Manager, DAYROLLAVG, and PMDAILYAVG tasks to ensure valid averages.
- **Data Validation**: Apply strict validity checks for load and fuel flow data before inclusion in averages.
- **Regulatory Mapping**: Maintain accurate mapping between PaDEP process/monitor/method codes and StackVision codes.
- **Migration Testing**: Validate migrated monitoring plans in CEMDPS before DAHS deployment.
- **Documentation**: Keep detailed records of configurations, changes, and validation results for audit readiness.

---

### Source Attribution
- **[Document 1: Shaun Ellis]** – Detailed PMDAILYAVG ProcessNow task configuration for 40 CFR 60.48Da(f) compliance.  
- **[Document 2: Brian Perlov]** – RSScripter usage for report migration between servers/units.  
- **[Document 3: Carl Reid]** – Logger reconciliation procedures to preserve configurations during updates/upgrades.  
- **[Document 4: Eric Swisher]** – PaDEP CSMM Rev 8 implementation process, LMESE standards, and QA/QC activities.  
- **[Document 5: Unknown]** – PaDEP process guide outlining transition steps, monitoring plan evaluation, and EDR generation.  
- **[Document 6: Ashley Partington]** – Mapping of PaDEP EDR process/monitor/method codes to StackVision codes.  
- **[Document 7: Information Systems Group]** – Subpart TTTT CO₂ mass emissions 12-month average calculation guidelines and DAHS configuration.

---

Would you like me to also create a **visual workflow diagram** showing the sequence from data capture through validation, calculation, and reporting for these processes? That would make this guide even more actionable.

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - EPA and state-specific regulations such as 40 CFR ...
- [[Environmental]] - **Continuous Emissions Monitoring Systems (CEMS)**...
- [[Calibration]] - **Lowest Monitored Emission Standard Equivalent (L...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
