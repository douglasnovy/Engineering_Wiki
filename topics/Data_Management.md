---
title: Data_Management
consolidated: true
sources: 8
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPReportingNotesdocx_9a31f1eb.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_ECMPSTestHistorypdf_95059768.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

## Title
**Data Management, Validation, and Server Migration Procedures for Continuous Source Monitoring Systems**

---

## Overview
This consolidated knowledge base entry provides a comprehensive guide to managing data rules, validating environmental monitoring data, reporting to regulatory agencies, and performing server migration tasks for Continuous Source Monitoring Systems (CSMS) such as StackVision. It integrates procedures for creating and applying data rules, clarifying Pennsylvania Department of Environmental Protection (PADEP) data validation requirements, handling fuel factor updates, managing ECMPS test histories, and ensuring smooth server migrations with proper database backup and configuration.

These processes are critical for maintaining regulatory compliance, ensuring data integrity, optimizing system performance, and preventing operational issues during infrastructure changes.

---

## Key Concepts

### 1. Data Rules
- **Rule Sets**: Collections of data rules that define how parameters are evaluated.
- **Parameter Lists**: Lists of parameters to which a Rule Set can be applied.
- **Independence**: Rule Sets are not inherently tied to specific parameters or intervals; they are applied dynamically via tasks.
- **SQL Integration**: DataRules uses SQL directly for faster execution compared to legacy tools like CNDMGR.

### 2. Data Validation
- **Valid Data Reading**: Defined by PADEP as a valid one-minute average.
- **Hourly Averages**: Must be calculated and coded correctly in DAHS to meet Revision No. 8 requirements.
- **Supplemental Guidance**: PADEP’s clarification documents provide examples and policies to assist in programming DAHS systems.

### 3. Regulatory Reporting
- **Reason and Action Codes**: Required for each hour; RC=8 for normal operation.
- **Missing Values**: Must be filled with zero for PADEP parameters.
- **Process Completion**: Ensure PADEP PN finishes before running EDR to check for errors.

### 4. Fuel Factor Updates
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on hourly data for coal and gas usage.
- **Parameter Tracking**: Includes heat input, CO₂, flow rates, NOx, Hg, and SO₂ emissions.

### 5. ECMPS Test History
- **Test Records**: Maintain detailed logs of QA, diagnostic, and other test types.
- **Submission Status**: Track whether tests have been submitted to EPA.
- **Facility Metadata**: Include facility name, location, and ORISPL ID.

### 6. Server Migration
- **Database Backups**: Essential during migration to prevent data loss.
- **Network Drive Mapping**: Allows backups to be stored on remote servers when local space is insufficient.
- **DataLink Configuration**: Prevent uncontrolled table growth by properly configuring `AverageValueLogConfig`.

---

## Technical Details

### DataRules Implementation
1. **Creating Rule Sets and Parameter Lists**:
   - Use DataRulesEditor spreadsheet.
   - Copy from Excel to SQL via SSMS into:
     - `dbo.DataRulesRule`
     - `dbo.DataRulesParameterList`
2. **Applying Rules**:
   - Required arguments: `-rs` (Rule Set), `-pl` (Parameter List).
   - Optional: `-r` (Real-time alarming).
3. **Supporting Tables**:
   - `dbo.AlarmNotificationConfig` – Alarm settings.
   - `dbo.EmailAddressList` – Notification recipients.

### PADEP Data Validation
- Ensure DAHS calculates hourly averages from valid one-minute data.
- Petition DEP for more stringent criteria if desired.
- Follow Revision No. 8 supplemental guidance without altering regulatory requirements.

### Reporting Procedures
- Assign reason/action codes for each hour.
- Fill missing PADEP parameter values with zero.
- Complete PN process before running EDR.

### Fuel Factor Update Workflow
- Compare “Before” and “After” values for fuel factors.
- Adjust parameters for coal and gas heat input.
- Validate emission factors for NOx, Hg, and SO₂.

### ECMPS Test History Management
- Record test type, date/time, reason, and result.
- Maintain availability and submission status.
- Verify DAHS data before EPA submission.

### Server Migration Steps
1. **Mapping Network Drive in SQL**:
   - Share target folder on new server.
   - Map drive via File Explorer.
   - Use `XP_CMDSHELL` to connect SQL to mapped drive.
2. **Enabling XP_CMDSHELL**:
   - Configure via `sp_configure` commands.
3. **Backup Process**:
   - Use SSMS backup GUI to store database on mapped drive.
4. **DataLink Configuration**:
   - Edit `AverageValueLogConfig` to limit logging scope.
   - Truncate `AverageValueLog` if table size is excessive.

---

## Best Practices
- **DataRules**: Keep Rule Sets modular and reusable; avoid hardcoding parameters.
- **Validation**: Regularly audit DAHS calculations against PADEP guidelines.
- **Reporting**: Automate reason/action code assignment to reduce human error.
- **Fuel Factors**: Periodically review and adjust based on operational changes.
- **Test History**: Maintain organized, accessible records for audits.
- **Migration**: Test network drive mapping before migration; ensure backups are verified.
- **DataLink**: Configure logging parameters immediately after installation to prevent uncontrolled growth.

---

## Source Attribution
- **Document 1**: Provided detailed DataRules architecture, SQL table usage, and task application procedures.
- **Document 2**: Clarified PADEP data validation requirements and definitions for valid readings.
- **Document 3**: Outlined PADEP reporting requirements, including reason/action codes and missing value handling.
- **Document 4**: Supplied fuel factor update data structure and parameter tracking methodology.
- **Document 5**: Described ECMPS test history report format and metadata requirements.
- **Document 6**: Identified DataLink configuration issues and provided SQL fixes to prevent excessive table growth.
- **Document 7 & 8**: Delivered step-by-step instructions for mapping a network drive to SQL for database backups during server migration.

---

Would you like me to also create a **visual workflow diagram** that links DataRules application, PADEP validation, and server migration steps into a single operational process? This could make the consolidated procedures easier to follow.

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

## Title
**...
- [[Environmental]] - It integrates procedures for creating and applying...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
