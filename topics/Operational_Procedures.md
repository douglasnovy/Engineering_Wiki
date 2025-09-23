---
title: Operational_Procedures
consolidated: true
sources: 7
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_ConfigurePMDAILYAVGProcessNowTaskforRegulation6048Dafdocx_3992f4be.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CopyReportsrsscripter_RSScripterProceduredocx_b431424a.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_LoggerReconciliation_ProcessforEngineeringLoggerReconciliationsMay2019docx_9734c828.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ExternalDOC-csmm_8_implementation___lesson_learned_standardspdf_2143f765.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PaDEPProcessGuidexlsx_e36a4dcc.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ProcessCodesforPaDEPEDRmaptoReasonCodesinStackVisionasdodocx_117b25f1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md']  # This would be a timestamp
---

### Title
**Configuration, Data Management, and Compliance Procedures for Continuous Emissions Monitoring Systems (CEMS)**

---

### Overview
This consolidated guide provides a comprehensive reference for configuring, managing, and ensuring regulatory compliance of Continuous Emissions Monitoring Systems (CEMS) and associated data handling processes. It integrates procedures for daily average particulate matter calculations, report migration between systems, logger reconciliation prior to upgrades, Pennsylvania Department of Environmental Protection (PaDEP) Revision 8 implementation standards, process code mapping, and Subpart TTTT CO₂ emissions averaging guidelines. The goal is to ensure accurate data collection, proper system configuration, and adherence to federal and state environmental regulations.

---

### Key Concepts

1. **CEMS Configuration and Compliance**  
   Continuous Emissions Monitoring Systems must be configured to meet specific regulatory requirements, such as 40 CFR Part 60 Subpart Da and PaDEP Rev 8 standards. This includes setting up averaging periods, alarm triggers, and data validation rules.

2. **Data Integrity and Logger Reconciliation**  
   Before performing system updates or hardware upgrades, a logger reconciliation captures the current configuration to prevent data loss and ensure post-upgrade functionality.

3. **Report Migration and Redundancy**  
   Tools like RSScripter.exe facilitate the transfer of reports between test and production environments or across units, ensuring consistent reporting formats and data availability.

4. **PaDEP Rev 8 Standards and LMESE**  
   PaDEP Revision 8 introduces specific data validation, reporting formats, and QA/QC requirements, including the calculation of the Lowest Monitored Emission Standard Equivalent (LMESE) for calibration drift checks.

5. **CO₂ Emissions Averaging (Subpart TTTT)**  
   Federal guidelines require calculating 12-month rolling averages for CO₂ mass emissions, with strict rules on data inclusion/exclusion based on validity and operational status.

---

### Technical Details

#### 1. PMDAILYAVG Process Configuration (Regulation 60.48Da(f))
- **System Resources:**  
  `DAY_EXCLUDE_CENTRAL_SITE_PARAMETER = TH`
- **Server Channels:**  
  - Channel Type: 6 – Block Average  
  - Percent Valid Required: 1  
  - Trigger Alarm on Exceedance: True  
  - Time Weight: N  
  - Standard Limit Operator: `>` or `>=` (depending on rounding approach)  
- **Condition Manager:**  
  Create or update a script to mark PM parameters as missing/invalid when `Time Online = 0`.  
  Must run before PMDAILYAVG Task.
- **ProcessNow Sequence:**  
  Run Condition Manager, DAYROLLAVG (excluding PM), then PMDAILYAVG with site and parameter names.
- **Alarm Messages:**  
  Enable `EXCEALM` for exceedance alarms.

#### 2. Logger Reconciliation Procedure
- **Pre-Reconciliation Steps:**  
  - Record network details (IP, subnet, gateway).  
  - Access controller via PuTTY/Telnet with integrator-level credentials.  
  - Navigate to Configuration → System Parameters and capture settings.
- **StackStudio Capture:**  
  Create a snapshot of the configuration for restoration after updates.

#### 3. Report Migration with RSScripter.exe
- **Requirements:**  
  - .NET 3.5 enabled.  
  - Run on SQL report server (for split servers).
- **Procedure:**  
  - Launch RSScripter.exe, set report server version, retrieve catalog.  
  - Select reports, set output folder, script reports.  
  - Edit `RS Scripter Load All Items.cmd` with correct paths for script location and RS.EXE.  
  - Update `.rss` files for unit-specific report sources.

#### 4. PaDEP Rev 8 Implementation
- **CEMDPS Access:**  
  Use GreenPort web portal for monitoring plan submission, testing, and certification.
- **Migration Error Check:**  
  Validate facility emission standards and analyzer information.
- **LMESE Calculation:**  
  Default = Full Scale ÷ 2; exceptions for opacity, CO₂, O₂, and VFR.
- **Process Guide Steps:**  
  - Evaluate monitoring plans, petitions, and LMESE.  
  - Migrate corrected plans to CEMDPS.  
  - Deploy plans on DAHS and validate data.  
  - Generate EDRs with correct process, monitor, method codes.

#### 5. Process Code Mapping
- Map PaDEP EDR process codes to StackVision reason codes, monitor codes to action codes, and method codes directly.

#### 6. Subpart TTTT CO₂ 12-Month Average Guidelines
- **Hourly Calculations:**  
  - Use valid hourly fuel flow data; exclude hours with missing/invalid load or CO₂ data.  
  - Include startup/shutdown data.
- **Rolling Average:**  
  - Always include 12 operating months; look back for non-operating months.  
  - Parameters: CO₂#/MWh, CO₂KGMWH (limit typically 1000 lb/MWh).
- **Configuration:**  
  - CO₂LBS = CO₂T/HR × 2000 × UNITOPHR#100  
  - LOADMWH invalid if CO₂ invalid.  
  - UNITOPHR = OPTIME parameter for Group 0.

---

### Best Practices

- **Run prerequisite tasks** (Condition Manager, DAYROLLAVG) before PMDAILYAVG to ensure valid averages.
- **Perform logger reconciliation** before any firmware or hardware changes to preserve configuration integrity.
- **Maintain consistent report formats** across environments by scripting and editing report sources as needed.
- **Follow PaDEP Rev 8 QA/QC protocols** for data validation and certification to avoid compliance issues.
- **Exclude invalid data** from CO₂ averaging calculations to maintain regulatory accuracy.
- **Document all configurations** and changes for audit readiness.

---

### Source Attribution
- **[Document 1] Shaun Ellis:** Provided PMDAILYAVG ProcessNow task configuration for Regulation 60.48Da(f), including Condition Manager setup and alarm configuration.
- **[Document 2] Brian Perlov:** Detailed RSScripter.exe usage for report migration between servers/units.
- **[Document 3] Carl Reid:** Outlined logger reconciliation procedures to safeguard configurations during updates/upgrades.
- **[Document 4] Eric Swisher:** Explained PaDEP Rev 8 implementation process, data validation requirements, and LMESE standards.
- **[Document 5] Unknown:** Provided PaDEP process guide workflow for transitioning monitoring plans and generating EDRs.
- **[Document 6] Ashley Partington:** Mapped PaDEP EDR process, monitor, and method codes to StackVision equivalents.
- **[Document 7] Information Systems Group:** Supplied Subpart TTTT CO₂ mass emissions 12-month average calculation guidelines and configuration details.

---

Would you like me to also create a **visual workflow diagram** that links these procedures together for easier operational reference? This could help show the sequence from configuration to compliance reporting.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx](../tools/engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx)** (0.02 MB)
- **[engineering_white_papers_WhitePapers_RatioEvaluation_RatioEvaluationxlsx_131ef366.xlsx](../tools/engineering_white_papers_WhitePapers_RatioEvaluation_RatioEvaluationxlsx_131ef366.xlsx)** (0.03 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - It integrates procedures for daily average particu...
- [[Environmental]] - The goal is to ensure accurate data collection, pr...
- [[Calibration]] - **PaDEP Rev 8 Standards and LMESE**  
   PaDEP Rev...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
