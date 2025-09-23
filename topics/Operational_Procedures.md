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
This consolidated guide provides technical procedures, configuration standards, and best practices for managing Continuous Emissions Monitoring Systems (CEMS), Data Acquisition and Handling Systems (DAHS), and associated reporting tools. It integrates regulatory requirements (e.g., 40 CFR Part 60 Subpart Da, Subpart TTTT, and PADEP Revision 8), operational tasks such as logger reconciliation, daily average calculations, and report migration, ensuring compliance, data integrity, and operational efficiency.

---

### Key Concepts

1. **Continuous Emissions Monitoring Systems (CEMS)**  
   CEMS are used to measure pollutant emissions from stationary sources. Data is processed through DAHS and reported to regulatory agencies.

2. **Data Acquisition and Handling System (DAHS)**  
   DAHS collects, processes, and stores emissions data, performs calculations (e.g., daily averages), and generates regulatory reports.

3. **Regulatory Frameworks**  
   - **40 CFR Part 60 Subpart Da**: Standards for PM daily averages for certain steam-generating units.  
   - **PADEP Revision 8 (CSMM)**: Pennsylvania-specific monitoring, validation, and reporting requirements.  
   - **40 CFR Part 60 Subpart TTTT**: CO₂ mass emissions 12-month average guidelines.

4. **Logger Reconciliation**  
   Capturing a snapshot of logger configuration before updates/upgrades to prevent data loss.

5. **Report Migration**  
   Using tools like RSScripter.exe to transfer reports between servers or units.

---

### Technical Details

#### 1. PMDAILYAVG ProcessNow Task Configuration (Regulation 60.48Da(f))
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
  Create a script to mark PM parameter as Missing/Invalid when Time Online = 0.
- **Execution Order**:  
  Condition Manager → DAYROLLAVG Task(s) → PMDAILYAVG Task.
- **Alarm Messages**:  
  Enable `EXCEALM` for exceedance alarms.

#### 2. Logger Reconciliation Procedure
- **Pre-Reconciliation**:  
  - Record network details (IP, subnet, gateway).  
  - Access controller via PuTTY/Telnet.  
  - Capture StackStudio configuration snapshot.
- **Situations Requiring Reconciliation**:  
  Cold-starts, firmware updates, hardware upgrades.

#### 3. PADEP Revision 8 Implementation
- **CEMDPS Access**:  
  GreenPort portal for monitoring plan submission and certification.
- **Migration Error Check**:  
  Validate facility emission standards, analyzer info, and measurement basis.
- **LMESE (Lowest Monitored Emission Standard Equivalent)**:  
  - Default: FS ÷ 2  
  - Used for calibration drift determination.  
  - Not applicable for opacity, CO₂, O₂, and certain VFR cases.
- **Process Guide Steps**:  
  - Evaluate monitoring plans and petitions.  
  - Migrate corrected plans.  
  - Deploy on DAHS.  
  - Generate and validate EDR data with correct process/method codes.

#### 4. Mapping Codes for PADEP EDR
- Process Codes → Reason Codes (StackVision)  
- Monitor Codes → Action Codes (StackVision)  
- Method Codes → Method Codes (StackVision)

#### 5. CO₂ Mass Emissions 12-Month Average (Subpart TTTT)
- **Hourly Calculations**:  
  - Use hourly fuel flow data; exclude missing/invalid load or CO₂ data.  
  - Include startup/shutdown data.  
- **Annual Average**:  
  - Always include 12 operating months; look back for non-operating months.  
  - Limit: typically 1000 lb/MWh.
- **Configuration Parameters**:  
  - `CO2LBS`: `(CO2T/HR * 2000 * UNITOPHR#100)`  
  - `LOADMWH`: `(UNITLOAD * UNITOPHR#100)`  
  - `UNITOPHR`: OPTIME parameter for Group 0.

#### 6. Report Migration with RSScripter.exe
- **Requirements**:  
  - .NET 3.5 enabled.  
  - Run on SQL report server for split-server setups.
- **Procedure**:  
  - Launch RSScripter.exe → Options → Report settings.  
  - Get Catalog → Select reports → Script to output folder.  
  - Edit `RS Scripter Load All Items.cmd` with correct paths.  
  - Update `.rss` files for unit-specific report names.

---

### Best Practices

1. **Maintain Execution Order**  
   Ensure prerequisite tasks (Condition Manager, DAYROLLAVG) run before PMDAILYAVG.

2. **Validate Data Before Reporting**  
   Use PADEP migration error checks and LMESE evaluations to ensure accuracy.

3. **Perform Logger Reconciliation Before Changes**  
   Always capture configurations before updates to prevent downtime or data loss.

4. **Follow Regulatory Averaging Rules**  
   For CO₂ and PM, adhere strictly to inclusion/exclusion criteria for valid data.

5. **Document All Changes**  
   Maintain clear records of configuration changes, report migrations, and reconciliations.

6. **Use Correct Code Mapping**  
   Ensure process, monitor, and method codes are correctly mapped between DAHS and regulatory EDR formats.

---

### Source Attribution
- **[Document 1] Shaun Ellis**: PMDAILYAVG ProcessNow Task configuration for Regulation 60.48Da(f), Condition Manager setup, execution order, and alarm configuration.  
- **[Document 2] Brian Perlov**: RSScripter.exe usage for report migration between servers/units.  
- **[Document 3] Carl Reid**: Logger reconciliation procedures, pre-reconciliation steps, and configuration snapshot methods.  
- **[Document 4] Eric Swisher (All4 Inc.)**: PADEP Revision 8 implementation process, CEMDPS access, migration error checks, LMESE definitions.  
- **[Document 5] Unknown**: PADEP process guide workflow from monitoring plan evaluation to EDR generation.  
- **[Document 6] Ashley Partington**: Mapping of PADEP EDR process, monitor, and method codes to StackVision equivalents.  
- **[Document 7] Information Systems Group**: Subpart TTTT CO₂ mass emissions 12-month average calculation guidelines, configuration parameters, and data validity rules.

---

If you’d like, I can create **a visual workflow diagram** that integrates these procedures from configuration through reporting to help engineers follow the process end-to-end. Would you like me to do that?

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
- [[Calibration]] - - **LMESE (Lowest Monitored Emission Standard Equi...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
