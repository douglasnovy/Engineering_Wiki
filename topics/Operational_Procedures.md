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
This consolidated guide provides engineering and technical personnel with a unified reference for configuring environmental monitoring systems, managing data and reports, performing system reconciliations, and ensuring compliance with key regulatory requirements. It integrates procedures for particulate matter (PM) daily average calculations, report transfer between systems, logger reconciliation, Pennsylvania Department of Environmental Protection (PaDEP) Continuous Source Monitoring Manual (CSMM) Revision 8 processes, and CO₂ mass emissions averaging under Subpart TTTT.

---

### Key Concepts

1. **Environmental Monitoring Systems (EMS)**
   - Systems such as StackVision and DAHS (Data Acquisition and Handling Systems) collect, process, and report emissions data from industrial units.
   - Continuous Emission Monitoring Systems (CEMS) are critical for regulatory compliance.

2. **Regulatory Framework**
   - **40 CFR Part 60, Subpart Da**: Standards for PM emissions from certain boilers.
   - **PaDEP CSMM Rev 8**: State-specific requirements for data validation, reporting, and QA/QC.
   - **Subpart TTTT**: Federal guidelines for CO₂ mass emissions and 12-month rolling averages.

3. **Data Integrity and Transfer**
   - Maintaining accurate configurations during upgrades or migrations.
   - Transferring reports between test and production environments.

4. **Averaging and Validation**
   - Daily and multi-month averaging for compliance.
   - Excluding invalid or substituted data from calculations.

---

### Technical Details

#### 1. PM Daily Average Configuration (Regulation 60.48Da(f))
- **System Resources**:  
  `DAY_EXCLUDE_CENTRAL_SITE_PARAMETER = TH`
- **Server Channels**:  
  - Channel Type: 6 – Block Average  
  - Percent Valid Required: 1  
  - Trigger Alarm on Exceedance: True  
  - Time Weight: N  
  - Standard Limit Operator: `>` or `>=` (based on rounding preference)  
  - Standard Limit: x.xxxx
- **Condition Manager**:  
  - Marks PM parameter as Missing/Invalid if Time Online = 0.
- **Execution Order**:  
  - Condition Manager task runs before PMDAILYAVG task.  
  - DAYROLLAVG tasks must exclude PM parameter or run prior.
- **Alarm Messages**:  
  - Enable `EXCEALM` for exceedance alarms.

#### 2. Report Transfer via RSScripter
- **Prerequisites**:  
  - .NET 3.5 enabled on server.  
  - Run on SQL report server for split server setups.
- **Procedure**:  
  - Launch `RSScripter.exe` → Configure options → Get Catalog → Select reports → Script to output folder.  
  - Edit `RS Scripter Load All Items.cmd` to set paths for script location and `RS.EXE`.  
  - Modify `.rss` files for unit-specific report sources.

#### 3. Logger Reconciliation
- **Purpose**:  
  - Capture ("snapshot") logger configuration before updates/upgrades to prevent data loss.
- **Steps**:  
  - Record network details (IP, subnet, gateway).  
  - Access controller via PuTTY/Telnet.  
  - Navigate to Configuration → System Parameters → Record settings.  
  - Capture StackStudio configuration.

#### 4. PaDEP CSMM Rev 8 Implementation
- **CEMDPS Access**:  
  - Web-based portal for CEMS data submission (GreenPort).
- **Process Steps**:  
  - Evaluate monitoring plans, petitions, and LMESE.  
  - Perform migration error checks.  
  - Deploy updated monitoring plans to DAHS.  
  - Validate data and generate EDRs with proper codes.
- **LMESE**:  
  - Lowest Monitored Emission Standard Equivalent = FS ÷ 2 (default).  
  - Not applicable for opacity, CO₂, O₂, VFR.

#### 5. CO₂ Mass Emissions – Subpart TTTT
- **Hourly Calculations**:  
  - Use fuel flow data; exclude hours with missing/invalid load or CO₂ data.  
  - Include startup/shutdown data.
- **12-Month Average**:  
  - Rolling average over 12 operating months; look back for non-operating months.
- **Parameters**:  
  - `CO2#/MWH` and `CO2KGMWH` (limit typically 1000 lb/MWh).
- **Configuration**:  
  - `CO2LBS` = CO₂ tons/hour × 2000 × `UNITOPHR#100`.  
  - `LOADMWH` invalid if CO₂ invalid.

---

### Best Practices

1. **Maintain Execution Order**  
   - Ensure prerequisite tasks (Condition Manager, DAYROLLAVG) run before PMDAILYAVG.

2. **Validate Before Migration**  
   - Perform thorough error checks before deploying new monitoring plans.

3. **Snapshot Configurations**  
   - Always capture current logger and system settings before upgrades.

4. **Exclude Invalid Data**  
   - Configure calculations to omit substituted or invalid readings.

5. **Document Paths and Versions**  
   - For report transfers, record exact paths to executables and scripts.

6. **Regulatory Awareness**  
   - Stay updated on federal and state-specific emission standards and reporting formats.

---

### Source Attribution

- **[Document 1] Shaun Ellis**: PMDAILYAVG task configuration for Regulation 60.48Da(f), Condition Manager setup, alarm configuration.
- **[Document 2] Brian Perlov**: RSScripter procedure for report transfer between systems, prerequisites, and file path configurations.
- **[Document 3] Carl Reid**: Logger reconciliation process, pre-reconciliation steps, configuration capture.
- **[Document 4] Eric Swisher (All4 Inc.)**: PaDEP CSMM Rev 8 background, implementation process, LMESE definition.
- **[Document 5] Unknown**: PaDEP transition guide workflow from plan evaluation to EDR generation.
- **[Document 6] Ashley Partington**: Mapping of PaDEP EDR process/method codes to StackVision codes.
- **[Document 7] Information Systems Group**: Subpart TTTT CO₂ mass emissions calculation guidelines, configuration details.

---

Would you like me to also **integrate a visual workflow diagram** showing the sequence from data collection → validation → averaging → reporting for both PM and CO₂ compliance? This could make the guide more actionable for engineers.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx](../tools/engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx)** (0.02 MB)
- **[engineering_white_papers_WhitePapers_RatioEvaluation_RatioEvaluationxlsx_131ef366.xlsx](../tools/engineering_white_papers_WhitePapers_RatioEvaluation_RatioEvaluationxlsx_131ef366.xlsx)** (0.03 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - It integrates procedures for particulate matter (P...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System


## Glossary

- **CEMS**: Continuous Emissions Monitoring System


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
