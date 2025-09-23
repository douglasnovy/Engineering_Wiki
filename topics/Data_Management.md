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
This consolidated knowledge base entry provides a comprehensive guide to managing, validating, and migrating data within Continuous Source Monitoring (CSM) systems, with a focus on **DataRules configuration**, **data validation criteria**, **fuel factor updates**, and **server/database migration procedures**.  
It integrates operational guidance for SQL-based rule application, Pennsylvania DEP data validation standards, fuel factor adjustment workflows, and best practices for database backup and migration.

---

## Key Concepts

### 1. DataRules Framework
- **Rule Sets**: Collections of data rules stored in SQL (`dbo.DataRulesRule`) that define how parameters are evaluated.
- **Parameter Lists**: Groupings of parameters stored in SQL (`dbo.DataRulesParameterList`) to which Rule Sets are applied.
- **Execution Model**: Rule Sets are applied via the `DATARULES ProcessNow` task, specifying:
  - `-rs` (Rule Set) – Required
  - `-pl` (Parameter List) – Required
  - `-r` (Real-time alarming) – Optional
- **Performance**: Uses direct SQL queries for faster execution compared to legacy systems like CNDMGR.

### 2. Data Validation Standards (PADEP Rev. 8)
- **Valid Data Reading**: Defined as a valid one-minute average.
- **Hourly Averages**: Must be calculated and coded correctly in DAHS to meet DEP criteria.
- **Regulatory Context**: Guidelines supplement existing requirements but do not replace regulations; DEP may deviate from these policies if warranted.

### 3. Fuel Factor Updates
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on operational data (e.g., coal/gas usage, heat input, emissions).
- **Data Tracking**: Hourly logs track parameters such as CO₂, NOx, Hg, SO₂, and fuel factors for accuracy and compliance.
- **Quality Flags**: Data entries may be marked as Missing, Invalid, Suspect, Maintenance, Calculated, or Modified.

### 4. Server and Database Migration
- **DataLink Table Growth Issue**: Installing DataLink without configuration causes uncontrolled growth in `dbo.AverageValueLog`.
- **Mapping Network Drives for Backups**: Enables direct backup to remote servers during migration when local storage is insufficient.
- **SQL Configuration**: Requires enabling `xp_cmdshell` for network drive mapping.

---

## Technical Details

### DataRules SQL Tables
- `dbo.DataRulesRule`: Stores Rule Sets.
- `dbo.DataRulesParameterList`: Stores Parameter Lists.
- `dbo.AlarmNotificationConfig`: Stores alarm settings.
- `dbo.EmailAddressList`: Stores email notification lists.

**Creating Rule Sets and Parameter Lists**:
1. Use **DataRulesEditor** (Excel-based).
2. Copy configurations into SQL via SSMS.

**Example Command**:
```
DATARULES ProcessNow -rs MINVELOCITY -pl VELOCITY -r
```

---

### PADEP Data Validation Implementation
- Ensure DAHS calculates hourly averages from valid one-minute averages.
- Petition DEP for more stringent criteria if desired.
- Maintain compliance with Revision No. 8 guidelines.

---

### Fuel Factor Update Workflow
- Maintain hourly logs for operational parameters.
- Compare BEFORE/AFTER values for fuel factor adjustments.
- Apply quality flags to identify data integrity issues.

---

### Server Migration Procedures

#### DataLink Table Management
1. Check `dbo.AverageValueLogConfig`.
2. If blank, set:
   - First box = `1` (parameter ID)
   - Second box = `6` (hourly logging)
3. Truncate large tables if necessary:
```
TRUNCATE TABLE AverageValueLog
```
*(Ensure correct database selection)*

#### Mapping Network Drive in SQL
1. Share target folder on new server.
2. Map drive in Windows (e.g., `S:`).
3. In SQL:
```
EXEC XP_CMDSHELL 'net use S: \\RemoteServer\Share /user:USERNAME PASSWORD'
```
4. Enable `xp_cmdshell` if disabled:
```
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
```
5. Verify mapping:
```
EXEC XP_CMDSHELL 'Dir S:'
```
6. Perform backup via SSMS GUI.

---

## Best Practices
- **DataRules**: Keep Rule Sets modular and parameter lists well-defined; avoid hard-coding parameters into rules.
- **Validation**: Implement automated checks for one-minute averages before hourly aggregation.
- **Fuel Factor**: Regularly audit fuel factor calculations against operational logs.
- **Migration**: Always configure DataLink tables before enabling logging; map network drives securely with least-privilege credentials.
- **SQL Operations**: Use SSMS for controlled data entry; document all changes for audit compliance.

---

## Source Attribution
- **[Document 1]**: Provided DataRules architecture, SQL table structure, and task execution parameters.
- **[Document 2]**: Clarified PADEP Rev. 8 data validation criteria and regulatory context.
- **[Document 3]**: Detailed fuel factor update process and parameter tracking methodology.
- **[Document 4]**: Identified DataLink table growth issue and mitigation steps.
- **[Document 5] & [Document 6]**: Provided step-by-step instructions for mapping network drives to SQL for database backups during migration.

---

I can also create a **visual workflow diagram** showing how DataRules, validation, fuel factor updates, and migration procedures interconnect if you’d like.  
Do you want me to add that diagram for easier reference?