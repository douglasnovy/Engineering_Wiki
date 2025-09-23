---
title: Operational_Procedures
consolidated: true
sources: 7
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Calculations_ConfigurePMDAILYAVGProcessNowTaskforRegulation6048Dafdocx_3992f4be.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_CopyReportsrsscripter_RSScripterProceduredocx_b431424a.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_LoggerReconciliation_ProcessforEngineeringLoggerReconciliationsMay2019docx_9734c828.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_ExternalDOC-csmm_8_implementation___lesson_learned_standardspdf_2143f765.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_PaDEPProcessGuidexlsx_e36a4dcc.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_ProcessCodesforPaDEPEDRmaptoReasonCodesinStackVisionasdodocx_117b25f1.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md']  # This would be a timestamp
---

### Title
**Configuration, Data Management, and Compliance Procedures for Continuous Emissions Monitoring Systems (CEMS)**

---

### Overview
This consolidated guide provides a comprehensive reference for configuring, managing, and reconciling Continuous Emissions Monitoring Systems (CEMS) in compliance with U.S. EPA and state-specific regulations, including 40 CFR Part 60 Subpart Da(f), Pennsylvania Department of Environmental Protection (PaDEP) Continuous Source Monitoring Manual (CSMM) Revision 8, and Subpart TTTT CO₂ mass emissions guidelines. It covers calculation task setup, data migration, logger reconciliation, report transfer, process code mapping, and best practices for regulatory compliance.

---

### Key Concepts

1. **CEMS Regulatory Framework**
   - **Federal Regulations**: 40 CFR Part 60 Subpart Da(f) for particulate matter (PM) daily averages; Subpart TTTT for CO₂ mass emissions.
   - **State Regulations**: PaDEP CSMM Rev 8 requirements for data validation, reporting formats, and QA/QC activities.
   
2. **Data Integrity and Validation**
   - Ensuring accurate data capture through pre-update logger reconciliation.
   - Validating hourly, daily, and monthly averages against regulatory standards.
   - Managing missing or invalid data conditions to prevent compliance violations.

3. **System Configuration**
   - StackStudio and DAHS (Data Acquisition and Handling System) parameter setup for averaging, alarm triggers, and exclusion rules.
   - Mapping process, reason, and method codes between PaDEP EDR and StackVision.

4. **Data Transfer and Migration**
   - Use of RSScripter.exe for report migration between servers or units.
   - PaDEP monitoring plan migration and error correction.

---

### Technical Details

#### 1. PMDAILYAVG Task Configuration (Regulation 60.48Da(f))
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
  - Marks PM parameter as missing/invalid when `Time Online = 0`.  
  - Task applies only to units constructed/reconstructed/modified after Feb 28, 2005.
- **Execution Order**:  
  - Condition Manager task runs before PMDAILYAVG.  
  - DAYROLLAVG tasks must exclude PM parameter or run prior to PMDAILYAVG.
- **Alarm Messages**:  
  - Enable `EXCEALM` for exceedance alerts.

#### 2. Logger Reconciliation Procedure
- **Purpose**: Capture ("snapshot") logger configuration before updates/upgrades to prevent data loss.
- **Pre-Reconciliation Steps**:
  - Record network details (IP, subnet, gateway).
  - Access controller via PuTTY/Telnet (8832: Telnet/PuTTY; 8864: PuTTY).
  - Log in with integrator password.
  - Navigate to Configuration → System Parameters.
  - Document all relevant settings.
- **StackStudio Capture**: Export current configuration for archival.

#### 3. PaDEP CSMM Rev 8 Implementation
- **CEMDPS Access**:  
  GreenPort web portal for monitoring plan submission and certification.
- **Migration Error Check**:  
  Validate facility emission standards, analyzer info, and averaging periods.
- **LMESE (Lowest Monitored Emission Standard Equivalent)**:
  - Default = FS ÷ 2 (except for opacity, CO₂, O₂, VFR).
  - Used for daily zero/upscale calibration drift checks.
- **Process Guide Steps**:
  - Evaluate initial monitoring plan and petitions.
  - Correct errors, migrate updated plan to CEMDPS.
  - Deploy plan to DAHS and validate data.
  - Generate EDR with correct process, monitoring, method codes.

#### 4. Process Code Mapping
- Map PaDEP EDR process codes to StackVision reason codes.
- Map monitor codes to action codes.
- Ensure method codes align between systems.

#### 5. CO₂ Mass Emissions (Subpart TTTT)
- **Hourly Calculations**:
  - Use hourly fuel flow to calculate CO₂ lbs.
  - Exclude hours with missing/invalid load or substituted fuel flow data.
- **General Rules**:
  - For no-load hours, use load = 0 with actual CO₂ lbs.
  - Include startup/shutdown data.
  - Maintain rolling 12-month average (look back for non-operating months).
  - Typical permit limit: 1000 lb/MWh.
- **Configuration Parameters**:
  - `CO2LBS`: `CO2T/HR * 2000 * UNITOPHR#100`
  - `LOADMWH`: `(UNITLOAD * UNITOPHR#100)`
  - `UNITOPHR`: OPTIME parameter for Group 0.

#### 6. Report Transfer via RSScripter.exe
- **Requirements**:
  - .NET 3.5 enabled.
  - Run on SQL report server (split server setups).
- **Procedure**:
  - Launch RSScripter.exe → Options → Report.
  - Select latest report server version.
  - Retrieve catalog, select reports, set output folder.
  - Edit `RS Scripter Load All Items.cmd` with correct paths.
  - Update `.rss` files for unit-specific report names if needed.

---

### Best Practices

1. **Pre-Change Documentation**: Always perform logger reconciliation before firmware or hardware changes.
2. **Execution Order Control**: Maintain correct task sequencing to ensure valid averages and alarms.
3. **Data Validation**: Implement automated checks for missing/invalid data before regulatory submission.
4. **Code Mapping Consistency**: Keep process, reason, and method code mappings updated across systems.
5. **Migration Testing**: Validate monitoring plans post-migration to avoid compliance gaps.
6. **CO₂ Data Handling**: Strictly follow exclusion rules for invalid data to maintain accurate rolling averages.
7. **Report Management**: Use RSScripter for consistent report deployment across environments.

---

### Source Attribution
- **[Document 1] Shaun Ellis**: PMDAILYAVG task configuration for Regulation 60.48Da(f), Condition Manager setup, alarm configuration.
- **[Document 2] Brian Perlov**: RSScripter.exe usage for report migration between servers/units.
- **[Document 3] Carl Reid**: Logger reconciliation procedures and pre-update configuration capture.
- **[Document 4] Eric Swisher (All4 Inc.)**: PaDEP CSMM Rev 8 implementation process, LMESE standards, QA/QC activities.
- **[Document 5] Unknown**: PaDEP process guide workflow for monitoring plan migration and validation.
- **[Document 6] Ashley Partington**: Mapping of PaDEP EDR process/monitor/method codes to StackVision codes.
- **[Document 7] Information Systems Group**: Subpart TTTT CO₂ mass emissions calculation guidelines and configuration parameters.

---

Would you like me to also create a **visual workflow diagram** that shows the sequence from logger reconciliation through data validation, task execution, and report submission? This could make the process easier to follow for engineers.

## See Also

- [[Environmental]] - EPA and state-specific regulations, including 40 C...
- [[Calibration]] - - Used for daily zero/upscale calibration drift ch...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
