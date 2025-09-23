---
title: Operational_Procedures
consolidated: true
sources: 7
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_ConfigurePMDAILYAVGProcessNowTaskforRegulation6048Dafdocx_3992f4be.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CopyReportsrsscripter_RSScripterProceduredocx_b431424a.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_LoggerReconciliation_ProcessforEngineeringLoggerReconciliationsMay2019docx_9734c828.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ExternalDOC-csmm_8_implementation___lesson_learned_standardspdf_2143f765.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PaDEPProcessGuidexlsx_e36a4dcc.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ProcessCodesforPaDEPEDRmaptoReasonCodesinStackVisionasdodocx_117b25f1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md']  # This would be a timestamp
---

### Title
**Consolidated Guide to Emissions Monitoring Configuration, Data Management, and Regulatory Compliance Procedures**

---

### Overview
This consolidated guide provides a comprehensive reference for configuring emissions monitoring systems, managing data across platforms, and ensuring compliance with key regulatory requirements such as EPA 40 CFR Part 60 Subpart Da, Pennsylvania Department of Environmental Protection (PaDEP) Continuous Source Monitoring Manual (CSMM) Revision 8, and Subpart TTTT CO₂ mass emissions guidelines.  
It integrates procedures for:
- Setting up daily average particulate matter (PM) calculations
- Reconciling logger configurations before system updates
- Transferring and replicating reports across systems
- Implementing PaDEP Rev 8 processes and mapping codes
- Configuring CO₂ 12-month average calculations

---

### Key Concepts

**1. Continuous Emissions Monitoring Systems (CEMS)**  
CEMS are used to measure pollutants emitted from industrial sources. Proper configuration ensures accurate data collection, compliance with environmental regulations, and reliable reporting.

**2. Data Acquisition and Handling Systems (DAHS)**  
DAHS collect, process, and store emissions data from CEMS. They must be configured to meet specific regulatory averaging periods, validity criteria, and reporting formats.

**3. Logger Reconciliation**  
A process to capture ("snapshot") the configuration of a data logger before updates or upgrades, ensuring no loss of critical operational settings.

**4. PaDEP CSMM Rev 8 Requirements**  
Includes data validation, reporting formats, QA/QC activities, and mapping of process/method codes between PaDEP EDR and StackVision.

**5. Subpart TTTT CO₂ Mass Emissions**  
Defines calculation and averaging methods for CO₂ emissions over a 12-month operating period, including data validity rules and configuration parameters.

---

### Technical Details

#### **A. PMDAILYAVG ProcessNow Task Configuration (Regulation 60.48Da(f))**
- **System Resources:**  
  `DAY_EXCLUDE_CENTRAL_SITE_PARAMETER = TH`
- **Server Channels:**  
  - Channel Type: 6 – Block Average  
  - Percent Valid Required: 1%  
  - Trigger Alarm on Exceedance: True  
  - Time Weight: N  
  - Standard Limit Operator: `>` or `>=` (based on rounding preference)  
  - Standard Limit: x.xxxx
- **Condition Manager:**  
  Create a script to mark PM parameter as MISSING and INVALID when Time Online equals 0.  
  Example:  
  ```
  If UNIT1:MATSON EQ 0
    SET UNIT1:PM_RT = MISSING
    SET UNIT1:PM_RT = INVALID
  END
  ```
- **Execution Order:**  
  Condition Manager task must run before PMDAILYAVG task.  
  DAYROLLAVG tasks must exclude PM parameter or run prior to PMDAILYAVG.
- **Alarm Messages:**  
  Enable `EXCEALM` to receive exceedance alarms.

#### **B. Logger Reconciliation Procedure**
- **Pre-Reconciliation Steps:**  
  - Record network details (IP, subnet mask, gateway)  
  - Access controller via PuTTY/Telnet  
  - Log in with integrator password  
  - Navigate to Configuration → System Parameters  
  - Capture StackStudio configuration snapshot
- **Applicable Scenarios:**  
  Cold-starts, firmware updates, hardware upgrades (e.g., 8832 to 8864).

#### **C. Report Transfer via RSScripter**
- **Requirements:**  
  - .NET 3.5 enabled  
  - Run on SQL report server (for split server setups)
- **Procedure:**  
  - Launch RSScripter.exe  
  - Set report server version  
  - Retrieve catalog and select reports  
  - Script out to desired folder  
  - Edit `RS Scripter Load All Items.cmd` to set paths for script location and RS.EXE  
  - Modify `.rss` files for unit-specific report sources

#### **D. PaDEP Rev 8 Implementation**
- **Process Steps:**  
  - File access request for facility  
  - Evaluate initial monitoring plan and petitions  
  - Assess LMESE values  
  - Correct and migrate monitoring plan to CEMDPS  
  - Deploy plan to DAHS  
  - Validate data and recommend configuration changes  
  - Generate EDR and validate hourly calculations with process, monitoring, and method codes
- **Code Mapping:**  
  - Process Codes in PaDEP EDR → Reason Codes in StackVision  
  - Monitor Codes in PaDEP EDR → Action Codes in StackVision  
  - Method Codes map directly

#### **E. Subpart TTTT CO₂ 12-Month Average Guidelines**
- **Hourly Calculations:**  
  - Use hourly fuel flow to calculate CO₂ lbs  
  - Exclude hours with missing/invalid load or substituted fuel flow data  
  - Include startup/shutdown data
- **Averaging:**  
  - Maintain rolling 12 operating months (look back for non-operating months)  
  - Operating month = any month with fuel combustion
- **Parameters:**  
  - `CO2#/MWH` and `CO2KGMWH` configured; typical limit = 1000 lb/MWh  
  - Annual Energy Sold and Potential Electric Output entered manually in EDR XML
- **Configuration:**  
  - `CO2LBS` = `CO2T/HR * 2000 * UNITOPHR#100`  
  - `LOADMWH` invalid if CO₂ invalid  
  - `UNITOPHR` = OPTIME parameter for Group 0

---

### Best Practices
- **Sequence Control:** Always run prerequisite tasks (Condition Manager, DAYROLLAVG) before dependent calculations (PMDAILYAVG).
- **Data Integrity:** Perform logger reconciliation before any system changes to preserve configuration.
- **Report Management:** Use RSScripter for consistent report replication, ensuring paths and executable references are correct.
- **Regulatory Compliance:**  
  - Follow PaDEP Rev 8 process steps meticulously to avoid migration errors.  
  - Validate LMESE values and ensure proper code mapping between systems.
- **CO₂ Data Validity:** Strictly apply exclusion rules for invalid/missing data to maintain compliance with Subpart TTTT.

---

### Source Attribution
- **[Document 1] Shaun Ellis:** Detailed PMDAILYAVG ProcessNow Task configuration for Regulation 60.48Da(f), including Condition Manager setup and alarm configuration.
- **[Document 2] Brian Perlov:** RSScripter.exe usage for report transfer between servers/units.
- **[Document 3] Carl Reid:** Logger reconciliation process and pre-reconciliation steps for preserving configurations.
- **[Document 4] Eric Swisher:** PaDEP CSMM Rev 8 background, implementation process, QA/QC activities, and LMESE definition.
- **[Document 5] Unknown:** PaDEP Rev 8 transition process guide from initial plan evaluation to EDR generation.
- **[Document 6] Ashley Partington:** Mapping of process, monitor, and method codes between PaDEP EDR and StackVision.
- **[Document 7] Information Systems Group:** Subpart TTTT CO₂ mass emissions 12-month average calculation guidelines and configuration parameters.

---

Would you like me to also create a **visual workflow diagram** showing the sequence from data collection → validation → calculation → reporting for these regulatory processes? That would make this guide even more actionable.

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
- [[Environmental]] - Proper configuration ensures accurate data collect...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
