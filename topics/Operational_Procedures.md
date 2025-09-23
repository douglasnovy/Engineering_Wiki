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
This consolidated guide provides engineering teams with a comprehensive reference for configuring, managing, and reconciling Continuous Emissions Monitoring Systems (CEMS) data in compliance with regulatory requirements such as U.S. EPA 40 CFR Part 60 Subpart Da, Pennsylvania Department of Environmental Protection (PADEP) Continuous Source Monitoring Manual (CSMM) Revision 8, and Subpart TTTT CO₂ mass emissions guidelines.  
It covers procedures for:
- Setting up daily average particulate matter (PM) calculations
- Transferring and replicating reports between systems
- Performing logger reconciliations before upgrades
- Implementing PADEP Rev 8 processes and standards
- Mapping process codes between systems
- Calculating and validating CO₂ emissions over 12-month periods

---

### Key Concepts

1. **Boiler Operating Day Definition**  
   - For units constructed/reconstructed/modified before March 1, 2005: a 24-hour period during which fossil fuel is combusted for the entire day.  
   - For units after February 28, 2005: definitions and averaging requirements per regulation 60.48Da(f).

2. **Daily Average PM Calculation (PMDAILYAVG)**  
   - Uses block average channel type with defined validity and alarm triggers.
   - Requires condition management to flag missing/invalid data before calculation.

3. **Logger Reconciliation**  
   - A “snapshot” of logger configuration prior to updates/upgrades to prevent data/configuration loss.
   - Essential before cold starts, firmware updates, or hardware changes.

4. **PADEP Rev 8 Compliance**  
   - Involves monitoring plan migration, validation, and configuration changes per CSMM standards.
   - Requires mapping of process, reason, monitor, and method codes between StackVision and PADEP EDR.

5. **CO₂ 12-Month Average Calculation (Subpart TTTT)**  
   - Based on hourly fuel flow and load data, excluding invalid/missing/substituted data.
   - Includes startup/shutdown hours and maintains a rolling 12-month operating average.

6. **Report Transfer (RSScripter)**  
   - Facilitates migration of reports between test and production servers or between units.
   - Requires correct server configuration and file path setup.

---

### Technical Details

#### 1. PMDAILYAVG Task Configuration (Regulation 60.48Da(f))
- **System Resources**:  
  `DAY_EXCLUDE_CENTRAL_SITE_PARAMETER = TH`
- **Channel Settings**:  
  - Type: 6 – Block Average  
  - Percent Valid Required: 1%  
  - Trigger Alarm on Exceedance: True  
  - Time Weight: N  
  - Standard Limit Operator: `>` or `>=` (based on rounding preference)  
  - Standard Limit: x.xxxx (site-specific)
- **Condition Manager Script**:  
  - Marks PM parameter as missing/invalid if Time Online = 0.
- **Execution Order**:  
  - Condition Manager → DAYROLLAVG → PMDAILYAVG
- **Alarm Messages**:  
  - Enable `EXCEALM` for exceedance notifications.

#### 2. Logger Reconciliation Procedure
- **Pre-Reconciliation**:
  - Record network details (IP, subnet, gateway).
  - Access controller via PuTTY/Telnet.
  - Capture StackStudio configuration snapshot.
- **Purpose**: Preserve operational configuration during upgrades.

#### 3. PADEP Rev 8 Process Guide
- **Steps**:
  1. File access request for facility.
  2. Evaluate initial monitoring plan and petitions.
  3. Assess LMESE (Lowest Monitored Emission Standard Equivalent).
  4. Migrate corrected monitoring plan to CEMDPS.
  5. Deploy plan to DAHS.
  6. Validate hourly calculations with correct codes and values.
- **Standards**:
  - Compliance with 25 Pa. Code §123.22(c)(4) [SO₂], §123.41 [Opacity], and 40 CFR Part 60 Subpart Da.

#### 4. Process Code Mapping
- Map PADEP EDR process codes to StackVision reason codes.
- Map monitor codes to action codes.
- Map method codes directly between systems.

#### 5. CO₂ 12-Month Average Guidelines
- **Hourly Calculation**:
  - CO₂ lbs = CO₂T/HR × 2000 × UNITOPHR#100
  - Exclude hours with invalid/missing load or CO₂ data.
- **Load MWh**:
  - (UNITLOAD × UNITOPHR#100) + (CO₂LBS × 0)
  - Invalid if CO₂ is invalid.
- **Rolling Average**:
  - Always includes 12 operating months; look back for non-operating months.
- **Limits**:
  - Most permits: ≤ 1000 lb/MWh.

#### 6. RSScripter Report Transfer
- **Requirements**:
  - .NET 3.5 enabled.
  - Run on SQL report server (split server setups).
- **Procedure**:
  1. Launch RSScripter.exe.
  2. Set report server version.
  3. Retrieve catalog and select reports.
  4. Script to output folder.
  5. Edit `RS Scripter Load All Items.cmd` with correct paths.
  6. Adjust `.rss` files for unit name changes.

---

### Best Practices

- **Pre-Task Validation**: Always run condition checks before daily average calculations to ensure data integrity.
- **Configuration Snapshots**: Maintain up-to-date snapshots before any system changes.
- **Code Mapping Consistency**: Keep mappings between systems documented and validated to avoid reporting errors.
- **Data Exclusion Rules**: Strictly enforce exclusion of invalid/missing/substituted data in compliance calculations.
- **Rolling Average Maintenance**: Automate look-back logic for non-operating months to maintain accurate 12-month averages.
- **Report Migration Testing**: Test migrated reports in production before full deployment.

---

### Source Attribution
- **[Document 1] Shaun Ellis**: PMDAILYAVG configuration details for Regulation 60.48Da(f), condition manager setup, execution order, and alarm configuration.
- **[Document 2] Brian Perlov**: RSScripter usage for report migration between servers/units, including configuration and scripting steps.
- **[Document 3] Carl Reid**: Logger reconciliation process, pre-reconciliation steps, and configuration capture methodology.
- **[Document 4] Eric Swisher (All4 Inc.)**: PADEP Rev 8 background, implementation process, standards, and LMESE definition.
- **[Document 5] Unknown**: PADEP transition guide procedural steps from monitoring plan evaluation to EDR generation.
- **[Document 6] Ashley Partington**: Mapping of process, reason, monitor, and method codes between PADEP EDR and StackVision.
- **[Document 7] Information Systems Group**: Subpart TTTT CO₂ mass emissions 12-month average calculation guidelines, configuration parameters, and exclusion rules.

---

Would you like me to also create a **visual workflow diagram** showing the sequence from data collection → validation → calculation → reporting for these processes? That would make this guide even more actionable.

## See Also

- [[Environmental]] - EPA 40 CFR Part 60 Subpart Da, Pennsylvania Depart...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
