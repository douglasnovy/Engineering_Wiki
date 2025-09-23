---
title: Data_Management
consolidated: true
sources: 6
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

### Title
**Data Management, Validation, and Migration Procedures for Continuous Source Monitoring Systems**

---

### Overview
This consolidated knowledge base entry provides a comprehensive guide to managing, validating, and migrating data within Continuous Source Monitoring Systems (CSMS), with a focus on StackVision environments. It integrates procedures for defining and applying data rules, clarifying regulatory data validation requirements, handling fuel factor updates, and performing safe server migrations and database backups. The goal is to ensure technical accuracy, regulatory compliance, and operational efficiency during both routine operations and system transitions.

---

### Key Concepts

1. **Data Rules and Rule Sets**  
   - **Rule Sets**: Collections of data rules that can be applied to multiple parameters via parameter lists.  
   - **Parameter Lists**: Groupings of parameters to which a single Rule Set can be applied.  
   - **Independence**: Rule Sets are not inherently tied to specific parameters or intervals; these are defined when creating tasks.

2. **Data Validation**  
   - **Valid Data Reading**: Defined by the Pennsylvania DEP as a valid one-minute average.  
   - **Hourly Averages**: Must be calculated and coded correctly in Data Acquisition and Handling Systems (DAHS) to meet regulatory requirements.  
   - **Supplemental Guidance**: Clarifications provided to assist facility owners/operators in programming DAHS for compliance.

3. **Fuel Factor Updates**  
   - **Prorated Fuel Factor**: Adjustments to fuel factor values based on hourly data for coal and gas usage, heat input, and emissions parameters.  
   - **Data Quality Flags**: Parameters may be marked as missing, invalid, suspect, or under maintenance.

4. **Server Migration and Database Management**  
   - **DataLink Configuration**: Improper configuration can cause uncontrolled growth of the `AverageValueLog` table.  
   - **Network Drive Mapping**: Required when local storage is insufficient for backups during migration.  
   - **SQL Integration**: Mapping network drives directly in SQL Server to facilitate backups.

---

### Technical Details

#### 1. DataRules Operation
- **Execution**: Uses SQL directly for faster rule application compared to CNDMGR.
- **Task Arguments**:
  - Required: `-rs` (Rule Set), `-pl` (Parameter List)
  - Optional: `-r` (Real-time alarming)
- **SQL Tables**:
  - `dbo.DataRulesRule` – Stores Rule Sets
  - `dbo.DataRulesParameterList` – Stores Parameter Lists
  - `dbo.AlarmNotificationConfig` – Stores alarm settings
  - `dbo.EmailAddressList` – Stores email notification lists
- **Creation**: Rule Sets and Parameter Lists are created in DataRulesEditor (Excel) and imported into SQL via SSMS.

#### 2. Data Validation (DEP Clarification)
- **Regulatory Context**: Based on Continuous Source Monitoring Manual Rev. 8.
- **Hourly Average Criteria**: Must be derived from valid one-minute averages.
- **Flexibility**: DEP may allow more stringent criteria upon petition.

#### 3. Fuel Factor Updates
- **Parameters**: Include unit operation status, heat input, CO₂, flow rates, fuel factors for gas and coal, and emissions (NOx, Hg, SO₂).
- **Data Flags**: Missing, invalid, suspect, maintenance, calculated, calculation error, modified.

#### 4. Server Migration Procedures
- **DataLink Issue Resolution**:
  - If `AverageValueLogConfig` is blank, set first box to `1` and second to `6` to limit logging.
  - Use `TRUNCATE TABLE AverageValueLog` in StackVision DB to clear excessive data.
- **Mapping Network Drive to SQL**:
  - Share target folder on network.
  - Map drive in Windows Explorer.
  - Use `XP_CMDSHELL` in SQL to map drive:
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
  - Perform backups via SSMS to mapped drive.

---

### Best Practices

- **DataRules**:
  - Keep Rule Sets modular for reuse across parameter lists.
  - Document all Rule Sets and Parameter Lists for audit purposes.
- **Data Validation**:
  - Align DAHS programming with DEP’s definition of valid data.
  - Regularly review hourly average calculations for compliance.
- **Fuel Factor Management**:
  - Implement automated checks for data flags to maintain data integrity.
  - Maintain historical records of fuel factor changes for traceability.
- **Server Migration**:
  - Pre-check DataLink configuration to prevent uncontrolled table growth.
  - Use network drive mapping for large backups to avoid local storage issues.
  - Test backup and restore procedures before decommissioning old servers.

---

### Source Attribution

- **[Document 1: DataRules Whitepaper]**  
  Key contributions: Detailed explanation of DataRules architecture, SQL table usage, task configuration, and DataRulesEditor workflow.

- **[Document 2: DEP Data Validation Clarification]**  
  Key contributions: Regulatory context and clarification on valid data readings and hourly average calculations.

- **[Document 3: Boswell Fuel Factor Updates]**  
  Key contributions: Hourly fuel factor adjustment data, parameter definitions, and data quality flagging.

- **[Document 4: DataLink Configuration Issue]**  
  Key contributions: Identification and resolution of uncontrolled table growth in `AverageValueLog` during DataLink installation.

- **[Document 5 & 6: Mapping Network Drive to SQL for Backups]**  
  Key contributions: Step-by-step instructions for mapping network drives in Windows and SQL, enabling `XP_CMDSHELL`, and performing backups during server migrations.

---

Would you like me to also create a **visual workflow diagram** showing how DataRules, validation, fuel factor updates, and migration procedures fit together in a CSMS operational lifecycle? That could make this consolidated entry more actionable.