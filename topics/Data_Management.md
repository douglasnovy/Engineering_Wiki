---
title: Data_Management
consolidated: true
sources: 6
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

## Title
**Data Management, Validation, and Migration Procedures for StackVision and Related Systems**

---

## Overview
This consolidated knowledge base entry provides a comprehensive guide to managing environmental monitoring data within StackVision and related systems. It covers **data rules configuration**, **regulatory data validation requirements**, **fuel factor updates**, and **server migration/database backup procedures**. The goal is to ensure accurate data processing, compliance with environmental regulations, and smooth system transitions during migrations.

---

## Key Concepts

### 1. Data Rules
- **Rule Sets**: Collections of data rules that can be applied to multiple parameters.
- **Parameter Lists**: Groups of parameters to which a single Rule Set can be applied.
- **Independence**: Rule Sets are not inherently tied to specific parameters; they are linked during task creation.
- **Execution**: Rules are applied via SQL for speed and efficiency.

### 2. Data Validation
- **Regulatory Context**: Based on Pennsylvania DEP Continuous Source Monitoring Manual Revision No. 8.
- **Valid Data Reading**: Defined as a valid one-minute average.
- **Hourly Averages**: Must be calculated and coded correctly in DAHS to meet compliance.
- **Supplementary Guidance**: Clarifies but does not override regulatory requirements.

### 3. Fuel Factor Updates
- **Prorated Fuel Factor**: Adjustments to fuel factor values for coal and gas based on operational data.
- **Data Tracking**: Hourly data logs for parameters such as CO₂, NOx, SO₂, and heat input.

### 4. Server Migration and Backups
- **Network Drive Mapping**: Required when local storage is insufficient for backups.
- **DataLink Considerations**: Improper configuration can cause uncontrolled table growth.
- **SQL Integration**: Use of `XP_CMDSHELL` and `sp_configure` for drive mapping and backup execution.

---

## Technical Details

### DataRules Configuration
1. **Tables Used**:
   - `dbo.DataRulesRule`: Stores Rule Sets.
   - `dbo.DataRulesParameterList`: Stores Parameter Lists.
   - `dbo.AlarmNotificationConfig`: Stores alarm settings.
   - `dbo.EmailAddressList`: Stores email notification lists.
2. **Task Arguments**:
   - Required: `-rs` (Rule Set), `-pl` (Parameter List)
   - Optional: `-r` (Real-time alarming)
3. **Creation Process**:
   - Define Rule Sets and Parameter Lists in DataRulesEditor (Excel).
   - Copy data to SQL via SSMS.

### DEP Data Validation Requirements
- **Hourly Average Validation**:
  - Each hourly average must be based on valid one-minute averages.
  - Owners/operators may petition for more stringent criteria.
- **DAHS Programming**:
  - Ensure proper coding for compliance.
  - Follow examples provided in DEP workshops.

### Fuel Factor Update Logging
- **Parameters Monitored**:
  - UNIT4 operational states (ON/OFF for gas/coal).
  - Heat input, fuel factor values, emissions data.
- **Data Quality Flags**:
  - Missing, Invalid, Suspect, Maintenance, Calculated, Calc Error, Modified.

### Server Migration Procedures
1. **Mapping a Network Drive in SQL**:
   - Share target folder on new server.
   - Map drive in Windows Explorer.
   - Use SQL command:
     ```sql
     EXEC XP_CMDSHELL 'net use S: \\RemoteServerName\ShareName /user:USERNAME PASSWORD'
     ```
   - Enable `XP_CMDSHELL` if disabled:
     ```sql
     EXEC sp_configure 'show advanced options', 1;
     RECONFIGURE;
     EXEC sp_configure 'xp_cmdshell', 1;
     RECONFIGURE;
     ```
   - Verify mapping:
     ```sql
     EXEC XP_CMDSHELL 'Dir S:'
     ```
2. **DataLink Table Management**:
   - If `dbo.AverageValueLogConfig` is blank, add:
     - First box: `1` (parameter ID)
     - Second box: `6` (hourly logging)
   - To truncate large tables:
     ```sql
     TRUNCATE TABLE AverageValueLog;
     ```
     *(Ensure correct database selection before running)*

---

## Best Practices
- **DataRules**:
  - Keep Rule Sets modular for reuse across multiple parameters.
  - Use SQL-based execution for efficiency.
- **Validation**:
  - Align DAHS programming with DEP definitions of valid data.
  - Maintain documentation of validation logic for audits.
- **Fuel Factor Updates**:
  - Regularly review and adjust fuel factors based on operational data.
  - Maintain complete logs with quality flags for traceability.
- **Migration**:
  - Always verify network drive mapping before initiating backups.
  - Configure DataLink properly to prevent uncontrolled table growth.
  - Use SSMS GUI for backups after mapping drives.

---

## Source Attribution
- **[Document 1]**: Provided DataRules architecture, SQL table structure, and task configuration details.
- **[Document 2]**: Clarified DEP data validation requirements for hourly averages and DAHS programming.
- **[Document 3]**: Supplied fuel factor update data structure and quality flag definitions.
- **[Document 4]**: Highlighted DataLink configuration issues and SQL table management during migrations.
- **[Document 5] & [Document 6]**: Detailed step-by-step procedures for mapping a network drive to SQL for database backups during server migrations.

---

If you’d like, I can create a **visual workflow diagram** showing how DataRules, validation, fuel factor updates, and migration procedures interact in the overall data management lifecycle. Would you like me to prepare that?