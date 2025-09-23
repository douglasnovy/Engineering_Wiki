---
title: Data_Management
consolidated: true
sources: 8
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPReportingNotesdocx_9a31f1eb.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_ECMPSTestHistorypdf_95059768.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

### Title
**Data Management, Validation, and Migration Procedures for Continuous Source Monitoring Systems**

---

### Overview
This consolidated knowledge base entry provides a comprehensive guide to managing, validating, and migrating data within Continuous Source Monitoring (CSM) environments, particularly for systems such as StackVision and related SQL-based data handling tools. It integrates procedures for defining and applying data rules, clarifies regulatory data validation requirements, outlines reporting protocols, addresses fuel factor updates, and details best practices for server migration and database backup.

Effective data management in CSM systems ensures regulatory compliance, operational efficiency, and data integrity. This document is intended for engineers, system administrators, and compliance specialists working with environmental monitoring data.

---

### Key Concepts

1. **Data Rules and Rule Sets**  
   - Rule Sets define conditions and logic for data processing.  
   - Parameters are grouped into Parameter Lists, which can be linked to Rule Sets for batch application.  
   - Rule Sets are independent of parameters until applied via a process task.

2. **Regulatory Data Validation**  
   - Validation ensures hourly averages meet Pennsylvania Department of Environmental Protection (PADEP) criteria.  
   - A valid data reading corresponds to a valid one-minute average.  
   - Policies supplement but do not replace regulatory requirements.

3. **Reporting Requirements**  
   - PADEP reporting requires reason and action codes for each hour.  
   - Missing values must be filled with zero for PADEP parameters.  
   - Specific codes (e.g., RC=8 for normal operation) must be used consistently.

4. **Fuel Factor Updates**  
   - Fuel factor calculations involve multiple parameters (e.g., heat input, flow, NOx, SO₂ emissions).  
   - Data integrity checks (missing, invalid, suspect flags) are essential for accurate fuel factor reporting.

5. **Server Migration and Database Backup**  
   - Migration may require mapping network drives to SQL for direct backups.  
   - DataLink configuration issues can cause uncontrolled table growth if not properly set.

---

### Technical Details

#### 1. DataRules Implementation
- **Tables Used**:  
  - `dbo.DataRulesRule` – Stores Rule Sets.  
  - `dbo.DataRulesParameterList` – Stores Parameter Lists.  
  - `dbo.AlarmNotificationConfig` – Stores alarm settings.  
  - `dbo.EmailAddressList` – Stores email notification lists.
- **ProcessNow Task Arguments**:  
  - Required: `-rs` (Rule Set), `-pl` (Parameter List)  
  - Optional: `-r` (Real-time alarming)
- **Example**: Applying `MINVELOCITY` Rule Set to `VELOCITY` Parameter List with real-time alarming.

#### 2. PADEP Data Validation
- **Criteria**: Hourly averages must be based on valid one-minute averages.  
- **Flexibility**: Facilities may petition for more stringent criteria.  
- **Clarification Purpose**: Assist in DAHS programming to ensure correct coding/calculation.

#### 3. PADEP Reporting Protocol
- **Action Codes**: RC=8 for normal operation.  
- **Missing Values**: Enter zero for missing PADEP parameters.  
- **Process Flow**: Complete PADEP PN → Run PADEP EDR → Check for errors.

#### 4. Fuel Factor Data Management
- **Parameters**: UNIT operation status, heat input, CO₂, flow, NOx, Hg, SO₂ emissions.  
- **Quality Flags**: Missing, invalid, suspect, maintenance indicators.  
- **Calculation Fields**: Fuel factor for gas and coal, differences, emission rates.

#### 5. Server Migration Procedures
- **DataLink Issue**:  
  - Tables: `dbo.AverageValueLog`, `dbo.AverageValueLogConfig`.  
  - If config is blank, logs every change → uncontrolled growth.  
  - Fix: Add `1` (parameter ID) and `6` (hourly level) to config table.  
  - Large table fix: `TRUNCATE TABLE AverageValueLog` (ensure correct database selection).
- **Mapping Network Drive to SQL**:  
  - Share target folder on network.  
  - Map drive in Windows Explorer.  
  - Use `XP_CMDSHELL` to map drive in SQL.  
  - Enable `xp_cmdshell` if disabled.  
  - Verify mapping with `Dir S:` command.  
  - Backup databases via SSMS GUI to mapped drive.

---

### Best Practices

- **DataRules**: Keep Rule Sets modular and parameter-independent for flexibility.  
- **Validation**: Align DAHS programming with regulatory definitions of valid data.  
- **Reporting**: Automate insertion of reason/action codes and zero-fill missing values to reduce human error.  
- **Fuel Factor**: Implement automated quality flag checks before calculations.  
- **Migration**:  
  - Always configure DataLink to limit logging scope.  
  - Map network drives securely with proper permissions.  
  - Verify backups post-migration to ensure data integrity.

---

### Source Attribution

- **Document 1 (DataRules Whitepaper)**: Provided foundational concepts, SQL table structures, and task execution details for DataRules.  
- **Document 2 (PADEP Data Validation Clarification)**: Clarified regulatory definitions and validation criteria for hourly averages.  
- **Document 3 (PADEP Reporting Notes)**: Outlined specific reporting codes and error-checking procedures.  
- **Document 4 (Fuel Factor Updates)**: Detailed fuel factor parameters, quality flags, and calculation fields.  
- **Document 6 (DataLink Issue in Migration)**: Identified potential uncontrolled table growth issue and provided SQL fix.  
- **Documents 7 & 8 (Mapping Network Drive to SQL)**: Provided step-by-step instructions for mapping network drives and backing up databases during migration.

---

If you’d like, I can also create a **visual workflow diagram** that links DataRules application, PADEP validation, reporting, and migration steps into a single operational process map. This would make the consolidated procedures easier to follow for engineers. Would you like me to prepare that?

## See Also

- [[Environmental]] - This document is intended for engineers, system ad...
- [[Environmental]] - **Regulatory Data Validation**  
   - Validation e...
