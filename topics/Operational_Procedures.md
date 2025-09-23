---
title: Operational_Procedures
consolidated: true
sources: 7
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_ConfigurePMDAILYAVGProcessNowTaskforRegulation6048Dafdocx_3992f4be.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CopyReportsrsscripter_RSScripterProceduredocx_b431424a.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_LoggerReconciliation_ProcessforEngineeringLoggerReconciliationsMay2019docx_9734c828.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ExternalDOC-csmm_8_implementation___lesson_learned_standardspdf_2143f765.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PaDEPProcessGuidexlsx_e36a4dcc.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_ProcessCodesforPaDEPEDRmaptoReasonCodesinStackVisionasdodocx_117b25f1.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md']  # This would be a timestamp
---

## Title
Comprehensive Guide to Environmental Monitoring System Configuration, Data Management, and Regulatory Compliance

---

## Overview
This consolidated guide provides technical procedures, configuration standards, and best practices for managing Continuous Emissions Monitoring Systems (CEMS) and associated data handling processes. It integrates operational guidance for configuring monitoring tasks, transferring reports, performing logger reconciliations, implementing Pennsylvania Department of Environmental Protection (PaDEP) Revision 8 requirements, and complying with federal regulations such as 40 CFR Part 60 Subpart Da and Subpart TTTT. The goal is to ensure accurate data collection, regulatory compliance, and reliable system performance across environmental monitoring operations.

---

## Key Concepts

### Continuous Emissions Monitoring Systems (CEMS)
CEMS are used to measure and record emissions data from industrial sources to demonstrate compliance with environmental regulations. Proper configuration and data validation are critical to maintaining accuracy and meeting reporting requirements.

### Logger Reconciliation
A process performed before updates or upgrades to a data controller/logger to capture its current configuration, ensuring no loss of critical operational parameters.

### PaDEP Revision 8
A set of requirements from the Pennsylvania DEP that standardizes data validation, reporting formats, QA/QC activities, and monitoring plan migration processes.

### ProcessNow Tasks
Automated tasks in StackStudio or similar DAHS (Data Acquisition and Handling Systems) used to calculate averages, validate data, and trigger alarms based on regulatory standards.

### LMESE (Lowest Monitored Emission Standard Equivalent)
A calculated value representing the lowest emission standard in terms of analyzer output, used for calibration drift checks.

### Subpart TTTT CO₂ Mass Emissions Guidelines
Federal guidelines for calculating and reporting CO₂ emissions on a 12-month rolling average basis, including data validity rules and configuration parameters.

---

## Technical Details

### 1. Configuring PMDAILYAVG ProcessNow Task (Regulation 60.48Da(f))
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
  Create or update a script to mark PM parameters as missing/invalid when `Time Online` equals 0.
- **Execution Order**:  
  - Run Condition Manager before PMDAILYAVG Task  
  - Ensure DAYROLLAVG tasks exclude PM parameters or run before PMDAILYAVG
- **Alarm Configuration**:  
  Enable `EXCEALM` for exceedance alarms.

### 2. RSScripter Report Transfer Procedure
- **Prerequisites**:  
  - .NET 3.5 enabled  
  - Run on SQL report server (for split server setups)
- **Steps**:  
  1. Launch `RSScripter.exe`  
  2. Set report server version in Options  
  3. Retrieve catalog and select reports  
  4. Script out reports to desired folder  
  5. Edit `RS Scripter Load All Items.cmd` to set correct paths for script location and `RS.EXE`  
  6. Update `.rss` files for unit-specific report names if needed.

### 3. Logger Reconciliation Procedure
- **Pre-Reconciliation**:  
  - Record network details (IP, subnet, gateway)  
  - Access controller via PuTTY/Telnet  
  - Log in with integrator password  
  - Navigate to system parameters and capture configuration
- **StackStudio Capture**:  
  Create a snapshot of current configuration for restoration after updates.

### 4. PaDEP Rev 8 Implementation
- **CEMDPS Access**:  
  Use GreenPort web portal for monitoring plan submission.
- **Migration Error Check**:  
  Validate facility emission standards and analyzer information.
- **Tracking Requirements**:  
  Record analyzer type, measurement basis, manufacturer, model, full scale range, and LMESE.
- **LMESE Defaults**:  
  FS ÷ 2 (except for opacity, CO₂, O₂, VFR).
- **Process Guide Steps**:  
  - Evaluate monitoring plans and petitions  
  - Correct and migrate plans  
  - Deploy updated plans to DAHS  
  - Validate data and generate EDRs with correct process/method codes.

### 5. Subpart TTTT CO₂ Mass Emissions Configuration
- **Hourly Data Rules**:  
  - Use fuel flow data to calculate CO₂ lbs  
  - Exclude hours with missing/invalid load or substituted fuel flow data  
  - Include startup/shutdown data
- **12-Month Average**:  
  - Always include 12 operating months; look back for non-operating months  
  - Configure CO₂#/MWh and CO₂KGMWH parameters per permit limits
- **Parameter Logic**:  
  - `CO2LBS`: `CO2T/HR * 2000 * UNITOPHR#100`  
  - `LOADMWH`: `(UNITLOAD * UNITOPHR#100)`; invalid if CO₂ invalid  
  - `UNITOPHR`: OPTIME parameter for Group 0

---

## Best Practices
- **Pre-Update Snapshots**: Always perform logger reconciliation before firmware or hardware changes.
- **Execution Order Control**: Ensure dependent tasks run in correct sequence to avoid invalid data.
- **Data Validation**: Apply LMESE and validity rules consistently to maintain compliance.
- **Report Management**: Use RSScripter for efficient report migration and maintain version control.
- **Regulatory Alignment**: Regularly review federal and state regulations to update configurations accordingly.
- **Documentation**: Maintain clear records of configurations, changes, and validation results for audits.

---

## Source Attribution
- **[Document 1] Shaun Ellis**: Provided detailed configuration steps for PMDAILYAVG ProcessNow Task under Regulation 60.48Da(f), including Condition Manager scripting and alarm setup.
- **[Document 2] Brian Perlov**: Detailed RSScripter.exe usage for report migration between servers and units.
- **[Document 3] Carl Reid**: Outlined logger reconciliation procedures to preserve configurations during updates/upgrades.
- **[Document 4] Eric Swisher**: Presented PaDEP Rev 8 standards, QA/QC activities, and LMESE definitions.
- **[Document 5] Unknown**: Provided PaDEP process guide for monitoring plan evaluation, migration, and EDR generation.
- **[Document 6] Ashley Partington**: Mapped PaDEP EDR process/method codes to StackVision codes.
- **[Document 7] Information Systems Group**: Supplied Subpart TTTT CO₂ mass emissions calculation and configuration guidelines.

---

Would you like me to also create a **visual workflow diagram** showing the sequence from data collection → validation → reporting for these processes? That could make the relationships between tasks and regulations clearer.

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

## Title
Co...
- [[Environmental]] - It integrates operational guidance for configuring...
- [[Environmental]] - The goal is to ensure accurate data collection, re...
- [[Environmental]] - ---

## Key Concepts

### Continuous Emissions Mon...
- [[Calibration]] - ### LMESE (Lowest Monitored Emission Standard Equi...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
