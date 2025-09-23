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
This consolidated guide provides a comprehensive reference for managing data rules, validating environmental monitoring data, handling fuel factor updates, and performing database-related server migration tasks in StackVision and associated systems. It integrates procedural details from multiple engineering white papers to ensure consistent, efficient, and accurate data handling across operational, compliance, and IT migration contexts.

---

## Key Concepts

### Data Rules
- **Rule Sets**: Collections of data validation or transformation rules that can be applied to multiple parameters.
- **Parameter Lists**: Groupings of parameters to which a Rule Set can be applied.
- **Execution**: Rule Sets are applied via the `DATARULES ProcessNow` task, specifying the Rule Set, Parameter List, and optional real-time alarming.

### Data Validation
- **Valid Data Reading**: Defined by the Pennsylvania DEP (PADEP) as a valid one-minute average.
- **Hourly Averages**: Must be calculated and coded correctly in the Data Acquisition and Handling System (DAHS) to meet regulatory requirements.
- **Regulatory Context**: Clarifications supplement but do not replace regulatory obligations.

### Fuel Factor Updates
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on operational data (e.g., coal/gas usage, heat input, emissions).
- **Data Tracking**: Hourly data includes operational parameters, emissions rates, and calculated fuel factors.

### Server Migration & Database Management
- **DataLink Configuration**: Misconfiguration can lead to uncontrolled growth of `dbo.AverageValueLog`. Proper configuration limits logging to essential parameters and intervals.
- **Network Drive Mapping for Backups**: Enables direct backup to a new server or network location when local storage is insufficient.

---

## Technical Details

### 1. DataRules Implementation
- **SQL Tables**:
  - `dbo.DataRulesRule`: Stores Rule Sets.
  - `dbo.DataRulesParameterList`: Stores Parameter Lists.
  - `dbo.AlarmNotificationConfig`: Stores alarm settings.
  - `dbo.EmailAddressList`: Stores email notification lists.
- **Execution Parameters**:
  - Required: `-rs` (Rule Set), `-pl` (Parameter List)
  - Optional: `-r` (Real-time alarming)
- **Example**: Applying `MINVELOCITY` Rule Set to `VELOCITY` Parameter List with real-time alarming enabled.

### 2. Data Validation per PADEP Rev. 8
- **Clarification Purpose**: Ensure DAHS systems calculate hourly averages correctly.
- **Valid One-Minute Average**: The fundamental unit for determining valid hourly data.
- **Flexibility**: Facilities may petition DEP for more stringent validation criteria.

### 3. Fuel Factor Data Handling
- **Data Fields**: Include operational status, fuel type usage, heat input, CO₂, flow rates, emissions (NOx, Hg, SO₂), and calculated fuel factors.
- **Quality Flags**: Missing, invalid, suspect, maintenance, calculated, calculation error, modified.

### 4. DataLink Configuration Issue
- **Problem**: Blank `AverageValueLogConfig` causes excessive logging.
- **Solution**:
  1. Open `dbo.AverageValueLogConfig` in SQL Server Management Studio (SSMS).
  2. If blank, set first box to `1` and second to `6` (logs one parameter at hourly level).
  3. If table is large, truncate with:
     ```sql
     TRUNCATE TABLE AverageValueLog;
     ```
     *(Ensure StackVision database is selected before running.)*

### 5. Mapping a Network Drive to SQL for Backups
- **Folder Sharing**:
  1. Share target folder on network.
  2. Verify permissions via Advanced Sharing.
- **Mapping Drive**:
  - In File Explorer: Map to a letter (e.g., `S:`) pointing to network path.
- **SQL Mapping Command**:
  ```sql
  EXEC XP_CMDSHELL 'net use S: \\RemoteServerName\ShareName /user:USERNAME PASSWORD';
  ```
- **Enable `xp_cmdshell` if Disabled**:
  ```sql
  EXEC sp_configure 'show advanced options', 1;
  RECONFIGURE;
  EXEC sp_configure 'xp_cmdshell', 1;
  RECONFIGURE;
  ```
- **Verification**:
  ```sql
  EXEC XP_CMDSHELL 'dir S:';
  ```
- **Backup**: Use SSMS backup GUI to save database to mapped drive.

---

## Best Practices
1. **Data Rules**:
   - Keep Rule Sets modular and reusable.
   - Regularly review Parameter Lists for relevance.
2. **Data Validation**:
   - Align DAHS programming with DEP definitions.
   - Maintain documentation of validation logic for audits.
3. **Fuel Factor Management**:
   - Monitor quality flags to ensure data integrity.
   - Automate checks for missing or suspect data.
4. **Database Management**:
   - Configure DataLink logging parameters immediately after installation.
   - Periodically purge or archive large log tables.
5. **Server Migration**:
   - Test network drive mapping before initiating backups.
   - Ensure `xp_cmdshell` is disabled after use for security.

---

## Source Attribution
- **[Document 1: DataRules Whitepaper rev1]**: Provided foundational concepts, SQL table structures, and execution parameters for DataRules.
- **[Document 2: PADEP Data Validation Rev. 8]**: Clarified regulatory definitions and requirements for valid data readings and hourly averages.
- **[Document 3: Boswell Fuel Factor Updates]**: Supplied operational data structure for prorated fuel factor calculations.
- **[Document 4: Item to Check in Migration Databases]**: Identified DataLink configuration issue and provided corrective SQL procedure.
- **[Document 5 & 6: Mapping a Network Drive to SQL for Database Backups]**: Delivered step-by-step instructions for mapping a network drive and performing backups during server migration.

---

Would you like me to also create a **visual workflow diagram** that integrates DataRules processing, data validation, and migration steps for easier operational reference? This could help bridge the gap between compliance and IT procedures.