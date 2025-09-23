---
title: Data_Management
consolidated: true
sources: 6
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

## Title
**Data Management, Validation, and Migration Procedures for Continuous Source Monitoring Systems**

---

## Overview
This consolidated knowledge base entry provides a comprehensive guide to managing, validating, and migrating data in Continuous Source Monitoring (CSM) environments, particularly for systems such as StackVision. It integrates procedures for defining and applying data rules, clarifying regulatory data validation requirements, managing fuel factor updates, and executing safe and efficient server migrations. The goal is to ensure technical accuracy, regulatory compliance, and operational efficiency during both routine operations and system transitions.

---

## Key Concepts

### 1. **Data Rules**
- **Rule Sets**: Collections of data rules that can be applied to multiple parameters via parameter lists.
- **Parameter Lists**: Groupings of parameters to which a single Rule Set can be applied.
- **Independence from Parameters**: Rule Sets are not inherently tied to specific parameters or intervals; they are applied dynamically during task execution.
- **Execution via SQL**: DataRules uses SQL directly for faster processing compared to legacy tools like CNDMGR.

### 2. **Data Validation**
- **Regulatory Context**: Based on Pennsylvania DEP Continuous Source Monitoring Manual Revision No. 8.
- **Valid Data Reading**: Defined as a valid one-minute average; hourly averages must be calculated from valid one-minute data points.
- **Supplemental Guidance**: Clarification documents provide examples and programming guidance for DAHS to ensure proper coding and calculation.

### 3. **Fuel Factor Updates**
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on hourly operational data.
- **Data Integrity**: Tracking changes in parameters such as coal/gas usage, heat input, CO₂ emissions, and pollutant outputs.

### 4. **Server Migration**
- **DataLink Considerations**: Installation of DataLink can create logging tables that may grow excessively if not configured.
- **Database Backups**: Mapping network drives to SQL Server for direct backups to remote or new servers when local storage is insufficient.

---

## Technical Details

### DataRules Implementation
1. **Required Arguments for DATARULES ProcessNow Task**:
   - `-rs` = Rule Set
   - `-pl` = Parameter List
2. **Optional Argument**:
   - `-r` = Real-time alarming
3. **SQL Tables Used**:
   - `dbo.DataRulesRule` – Stores Rule Sets
   - `dbo.DataRulesParameterList` – Stores Parameter Lists
   - `dbo.AlarmNotificationConfig` – Stores alarm settings
   - `dbo.EmailAddressList` – Stores email notification lists
4. **Creation Workflow**:
   - Define Rule Sets and Parameter Lists in DataRulesEditor (Excel).
   - Copy directly into SQL tables using SSMS.

### Data Validation Procedures
- Ensure DAHS calculates hourly averages only from valid one-minute averages.
- Petition DEP for more stringent validation criteria if desired.
- Follow DEP’s clarification examples to avoid misinterpretation of regulatory requirements.

### Fuel Factor Data Management
- Maintain accurate before/after values for operational parameters.
- Track and flag missing, invalid, suspect, or maintenance data.
- Ensure calculated values are error-free before applying fuel factor updates.

### Server Migration and Backup Mapping
1. **Network Folder Sharing**:
   - Share target backup folder on new server.
   - Verify permissions via Advanced Sharing.
2. **Map Network Drive on Old Server**:
   - Assign preferred drive letter (e.g., S:).
   - Link to network path of shared folder.
3. **Map Drive in SQL Server**:
   - Use `XP_CMDSHELL` to execute `net use` command.
   - Enable `XP_CMDSHELL` if disabled via `sp_configure`.
4. **Verify Mapping**:
   - Run `EXEC XP_CMDSHELL 'Dir S:'` to confirm.
5. **Backup Execution**:
   - Use SSMS backup GUI to save databases to mapped drive.

### DataLink Table Management
- **Issue**: Blank `AverageValueLogConfig` causes excessive logging in `AverageValueLog`.
- **Solution**:
  - Edit `AverageValueLogConfig` to set first box to `1` and second to `6` (logs one parameter hourly).
  - Truncate `AverageValueLog` if already oversized, ensuring StackVision is the active database.

---

## Best Practices
- **DataRules**: Keep Rule Sets modular and parameter lists well-defined to simplify application and maintenance.
- **Validation**: Align DAHS programming with DEP’s clarified definitions to ensure compliance.
- **Fuel Factor Updates**: Implement robust data quality checks before applying updates.
- **Server Migration**:
  - Plan for storage limitations early.
  - Map network drives securely with proper permissions.
  - Disable unnecessary logging to prevent database bloat.
- **SQL Management**: Regularly monitor table sizes and truncate logs when necessary, following proper backup protocols.

---

## Source Attribution
- **[Document 1: DataRules Whitepaper]**: Provided foundational concepts, SQL table structures, and execution parameters for DataRules.
- **[Document 2: Data Validation Clarification Document]**: Clarified regulatory definitions and procedures for valid data readings and hourly averages.
- **[Document 3: Boswell Fuel Factor Updates]**: Illustrated fuel factor adjustment processes and data integrity tracking.
- **[Document 4: Item to Check in Migration Databases]**: Highlighted DataLink-related logging issues and SQL table management solutions.
- **[Document 5 & 6: Mapping a Network Drive to SQL for Database Backups]**: Detailed step-by-step procedures for mapping network drives and executing backups during server migrations.

---

I have consolidated the documents into a single structured guide.  
Do you want me to also create **a visual workflow diagram** showing how DataRules, validation, fuel factor updates, and migration steps fit together? That could help operational teams see the process end-to-end.