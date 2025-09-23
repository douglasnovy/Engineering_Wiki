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
This consolidated guide provides engineering teams with a unified reference for configuring environmental monitoring systems, managing data and reports, performing system reconciliations, and ensuring compliance with key regulatory frameworks such as EPA Regulation 60.48Da(f), Pennsylvania DEP (PaDEP) Continuous Source Monitoring Manual (CSMM) Revision 8, and Subpart TTTT CO₂ Mass Emissions guidelines. It integrates procedures for DAHS (Data Acquisition and Handling System) setup, logger reconciliation, report migration, and regulatory data validation, ensuring operational integrity and adherence to environmental standards.

---

### Key Concepts

1. **Environmental Monitoring Systems (EMS)**
   - Systems such as StackVision and DAHS collect, process, and report emissions data from industrial units.
   - Continuous Emission Monitoring Systems (CEMS) are critical for regulatory compliance.

2. **Regulatory Frameworks**
   - **EPA Regulation 60.48Da(f)**: Specifies particulate matter (PM) averaging and exceedance alarm requirements for certain steam-generating units.
   - **PaDEP CSMM Rev 8**: Defines data validation, reporting formats, QA/QC activities, and process codes for emissions reporting.
   - **Subpart TTTT**: Establishes CO₂ mass emissions calculation and averaging guidelines over a 12-month operating period.

3. **Data Integrity and Reconciliation**
   - Logger reconciliation ensures configuration preservation during updates or upgrades.
   - Proper mapping of process, reason, monitor, and method codes between PaDEP EDR and StackVision is essential for accurate reporting.

4. **Report Management**
   - RSScripter facilitates migration of SQL-based reports between servers or units, ensuring consistent reporting across environments.

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
  - Standard Limit Operator: > or >= (based on rounding preference)  
  - Standard Limit: x.xxxx
- **Condition Manager**:  
  - Marks PM parameter as Missing/Invalid when Time Online = 0.
  - Task applies only to units constructed/reconstructed/modified after Feb 28, 2005.
- **Process Sequence**:  
  - Run Condition Manager before PMDAILYAVG task.
  - Configure DAYROLLAVG tasks to exclude PM parameter or run them prior.
- **Alarm Messages**:  
  - Enable `EXCEALM` for exceedance alarms.

#### 2. Logger Reconciliation Procedure
- **Pre-Reconciliation**:
  - Record network details (IP, subnet, gateway).
  - Access controller via PuTTY/Telnet (8832 via Telnet/PuTTY; 8864 via PuTTY).
  - Log in with integrator-level credentials.
  - Capture system parameters from StackStudio.
- **Purpose**:
  - Preserve configuration before cold starts, firmware updates, or hardware upgrades.

#### 3. PaDEP CSMM Rev 8 Implementation
- **CEMDPS Access**:
  - Use GreenPort web portal for monitoring plan submission and certification.
- **Migration Error Check**:
  - Validate facility emission standards and analyzer information.
- **LMESE (Lowest Monitored Emission Standard Equivalent)**:
  - Default = FS ÷ 2 (except for opacity, CO₂, O₂, VFR).
  - Used for daily zero/upscale calibration drift determination.
- **Process Guide Steps**:
  - Evaluate monitoring plans, petitions, and LMESE.
  - Migrate corrected plans, deploy on DAHS, validate data, and generate EDRs.

#### 4. Process and Code Mapping
- Map PaDEP EDR process codes to StackVision reason codes.
- Map monitor codes to action codes.
- Align method codes between PaDEP EDR and StackVision.

#### 5. CO₂ Mass Emissions (Subpart TTTT)
- **Hourly Calculations**:
  - Use valid hourly fuel flow data; exclude hours with missing/invalid load or substituted data.
  - Include startup/shutdown data.
- **12-Month Average**:
  - Always include 12 operating months; look back for non-operating months.
  - Typical permit limit: 1000 lb/MWh.
- **Configuration Parameters**:
  - `CO2LBS`: CO₂ tons/hour × 2000 × UNITOPHR#100.
  - `LOADMWH`: (UNITLOAD × UNITOPHR#100).
  - `UNITOPHR`: OPTIME parameter for Group 0.

#### 6. Report Migration with RSScripter
- **Requirements**:
  - .NET 3.5 enabled.
  - Run on SQL report server for split-server setups.
- **Procedure**:
  - Launch RSScripter, set report server version, retrieve catalog, select reports.
  - Script reports to output folder, edit `RS Scripter Load All Items.cmd` paths.
  - Locate RS.EXE in SQL Server Tools\Binn folder.
  - Modify `.rss` files for unit-specific report sources.

---

### Best Practices

- **Configuration Management**:
  - Document all DAHS and CEMS settings before changes.
  - Use condition managers to ensure data validity.
- **Data Validation**:
  - Follow PaDEP Rev 8 QA/QC protocols.
  - Exclude invalid/substituted data from regulatory calculations.
- **Regulatory Compliance**:
  - Align averaging periods and limits with applicable regulations.
  - Maintain accurate process/method code mappings.
- **Report Consistency**:
  - Use RSScripter for controlled migration of reports.
  - Verify report functionality post-migration.
- **Operational Continuity**:
  - Perform logger reconciliations before any system upgrade.
  - Validate post-change data against pre-change baselines.

---

### Source Attribution

- **[Document 1: Shaun Ellis]**: Detailed PMDAILYAVG task configuration for Regulation 60.48Da(f), including condition manager setup and alarm configuration.
- **[Document 2: Brian Perlov]**: RSScripter usage for report migration between servers/units.
- **[Document 3: Carl Reid]**: Logger reconciliation procedures to preserve configurations during updates/upgrades.
- **[Document 4: Eric Swisher]**: PaDEP CSMM Rev 8 implementation process, QA/QC activities, and LMESE definitions.
- **[Document 5: Unknown]**: PaDEP process guide steps for monitoring plan evaluation, migration, and EDR generation.
- **[Document 6: Ashley Partington]**: Mapping of process, reason, monitor, and method codes between PaDEP EDR and StackVision.
- **[Document 7: Information Systems Group]**: Subpart TTTT CO₂ mass emissions calculation guidelines and configuration parameters.

---

Would you like me to also create **workflow diagrams** for these procedures so that engineers can visually follow the configuration and compliance steps? This could make the guide more actionable.

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - It integrates procedures for DAHS (Data Acquisitio...
- [[Calibration]] - - Used for daily zero/upscale calibration drift de...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
