---
title: Data_Management
consolidated: true
sources: 6
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

## Title
**Data Management, Validation, and Migration Procedures for StackVision and Related Systems**

---

## Overview
This consolidated guide provides a comprehensive reference for managing data rules, validating continuous source monitoring data, handling fuel factor updates, and performing server migration tasks in StackVision and associated SQL-based systems. It integrates operational procedures, technical specifications, and best practices from multiple engineering white papers to ensure accurate data processing, regulatory compliance, and efficient system transitions.

---

## Key Concepts

### 1. **Data Rules in StackVision**
- **Rule Sets**: Collections of data rules that define conditions or thresholds for parameters.
- **Parameter Lists**: Groups of parameters to which a Rule Set can be applied.
- **Independence of Rules and Parameters**: Rule Sets are not inherently tied to specific parameters; they are linked during task creation.
- **Execution**: Rules are applied via the `DATARULES ProcessNow` task with required arguments for Rule Set (`-rs`) and Parameter List (`-pl`), plus optional real-time alarming (`-r`).

### 2. **Data Validation for Continuous Source Monitoring**
- **Regulatory Context**: Based on Pennsylvania DEP Continuous Source Monitoring Manual Revision No. 8.
- **Valid Data Reading**: Defined as a valid one-minute average.
- **Hourly Average Validation**: Clarifies criteria for coding/calculating hourly averages in DAHS.
- **Supplementary Guidance**: Intended to assist facility owners/operators without altering regulatory requirements.

### 3. **Fuel Factor Updates**
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on hourly operational data.
- **Parameters Tracked**: Includes coal/gas usage, heat input, CO₂ emissions, flow rates, NOx, Hg, SO₂ metrics.
- **Data Quality Flags**: Missing, invalid, suspect, maintenance, calculated, and modified indicators.

### 4. **Server Migration and SQL Management**
- **DataLink Installation Issue**: Unconfigured `dbo.AverageValueLogConfig` can cause uncontrolled growth of `dbo.AverageValueLog`.
- **Network Drive Mapping for Backups**: Enables direct database backup to remote servers during migration.
- **SQL Configuration**: Use of `XP_CMDSHELL` and `sp_configure` to enable network drive mapping.
- **Backup Execution**: Verification of mapped drives and use of SSMS backup GUI.

---

## Technical Details

### DataRules SQL Tables
- **dbo.DataRulesRule**: Stores Rule Sets.
- **dbo.DataRulesParameterList**: Stores Parameter Lists.
- **dbo.AlarmNotificationConfig**: Stores alarm settings.
- **dbo.EmailAddressList**: Stores email lists for notifications.

**Creation Process**:
- Rule Sets and Parameter Lists are created in the DataRulesEditor spreadsheet.
- Data is copied from Excel to SQL using SSMS.

---

### Data Validation Procedures
- **Hourly Average Criteria**:
  - Must be based on valid one-minute averages.
  - Owners/operators may petition for more stringent criteria.
- **DAHS Programming**:
  - Ensure coding/calculation logic aligns with DEP guidance.
  - Apply validation flags appropriately.

---

### Fuel Factor Update Workflow
- **Data Review**:
  - Compare "Before" and "After" values for operational parameters.
  - Adjust fuel factor calculations for coal and gas proportionally.
- **Quality Control**:
  - Apply flags for missing or suspect data.
  - Maintain logs for calculated and modified values.

---

### Server Migration Steps
1. **DataLink Configuration**:
   - If `dbo.AverageValueLogConfig` is blank, set first box to `1` and second to `6` to limit logging.
   - Truncate `dbo.AverageValueLog` if oversized.
2. **Network Drive Mapping**:
   - Share target folder on new server.
   - Map drive on old server via File Explorer.
   - Use SQL commands to map drive (`net use`) and enable `XP_CMDSHELL` if needed.
3. **Backup Execution**:
   - Verify mapped drive with `Dir` command.
   - Perform backup via SSMS GUI.

---

## Best Practices
- **DataRules**:
  - Keep Rule Sets generic for reuse across multiple Parameter Lists.
  - Document Rule Set logic for audit purposes.
- **Validation**:
  - Align DAHS programming with DEP definitions of valid data.
  - Maintain clear records of petitions for more stringent validation.
- **Fuel Factor Management**:
  - Regularly review operational data for accuracy.
  - Apply consistent quality flags to maintain data integrity.
- **Server Migration**:
  - Configure DataLink before enabling logging to prevent uncontrolled table growth.
  - Always verify network permissions before mapping drives.
  - Enable `XP_CMDSHELL` only when necessary and disable afterward for security.

---

## Source Attribution
- **[Document 1: DataRules Whitepaper]**: Provided foundational concepts, SQL table structures, and operational procedures for applying Rule Sets to Parameter Lists in StackVision.
- **[Document 2: Data Validation Clarification]**: Clarified regulatory definitions and procedures for validating hourly averages in continuous source monitoring.
- **[Document 3: Fuel Factor Updates]**: Detailed operational parameters, before/after comparisons, and quality control flags for prorated fuel factor adjustments.
- **[Document 4: DataLink Issue in Migration]**: Identified potential uncontrolled table growth issue and provided SQL-based mitigation steps.
- **[Document 5 & 6: Mapping Network Drive to SQL]**: Delivered step-by-step instructions for mapping network drives in SQL for database backups during server migrations.

---

Would you like me to also include a **visual workflow diagram** showing the relationship between DataRules, validation, fuel factor updates, and migration tasks? This could make the consolidated guide easier to follow.