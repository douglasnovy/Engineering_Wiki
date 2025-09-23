---
title: Data_Management
consolidated: true
sources: 4
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

## Title
**Data Management, Validation, and Backup Procedures for Continuous Source Monitoring Systems**

---

## Overview
This consolidated guide provides a comprehensive reference for managing environmental monitoring data, validating continuous source monitoring results, and ensuring secure database backup during server migrations. It integrates procedures for **DataRules** configuration, **Pennsylvania DEP data validation criteria**, and **SQL-based network drive mapping for database backups**. These processes are critical for maintaining regulatory compliance, operational efficiency, and data integrity in Continuous Source Monitoring (CSM) environments.

---

## Key Concepts

### 1. DataRules Framework
- **Rule Sets**: Collections of data rules applied to monitoring parameters.
- **Parameter Lists**: Groups of parameters to which a Rule Set can be applied.
- **Independence of Rules and Parameters**: Rule Sets are not inherently tied to specific parameters; they are linked during task creation.
- **Execution via SQL**: DataRules uses SQL directly for faster processing compared to legacy systems like CNDMGR.

### 2. Data Validation (PADEP Manual Rev. 8)
- **Valid Data Reading**: Defined as a valid one-minute average.
- **Hourly Average Validation**: Clarified criteria for determining valid hourly averages in DAHS systems.
- **Regulatory Context**: Policies supplement existing requirements but do not replace regulations; DEP may deviate from guidelines if warranted.

### 3. SQL Network Drive Mapping for Backups
- **Purpose**: Enables direct database backup to a network location when local storage is insufficient.
- **Network Drive Mapping**: Assigning a drive letter to a shared network folder for SQL Server access.
- **XP_CMDSHELL Utility**: Used to execute OS-level commands from SQL Server for mapping and verification.

---

## Technical Details

### 1. Configuring DataRules
- **Required Arguments for DATARULES ProcessNow Task**:
  - `-rs`: Rule Set name
  - `-pl`: Parameter List name
- **Optional Argument**:
  - `-r`: Real-time alarming
- **Example**: Applying `MINVELOCITY` Rule Set to `VELOCITY` Parameter List with real-time alarming.
- **SQL Tables**:
  - `dbo.DataRulesRule`: Stores Rule Sets
  - `dbo.DataRulesParameterList`: Stores Parameter Lists
  - `dbo.AlarmNotificationConfig`: Stores alarm settings
  - `dbo.EmailAddressList`: Stores email notification lists
- **Creation Workflow**:
  - Define Rule Sets and Parameter Lists in **DataRulesEditor** (Excel).
  - Import into SQL via SSMS.

### 2. PADEP Hourly Average Validation
- **Criteria**:
  - Hourly averages must be based on valid one-minute averages.
  - Owners/operators may petition DEP for more stringent criteria.
- **Implementation in DAHS**:
  - Ensure coding/calculation aligns with DEP clarification.
  - Reference Manual Rev. 8, page 64 (sections 4.a and 4.b).

### 3. Mapping a Network Drive to SQL for Backups
- **Step-by-Step**:
  1. **Share Folder**:
     - Right-click folder → Properties → Sharing tab → Share.
     - Use Advanced Sharing to set user permissions.
  2. **Map Network Drive**:
     - File Explorer → Right-click Computer → Map Network Drive.
     - Assign preferred letter (e.g., `S:`) and set folder path.
  3. **Connect in SQL**:
     ```sql
     EXEC XP_CMDSHELL 'net use S: \\RemoteServerName\ShareName /user:USERNAME PASSWORD';
     ```
  4. **Enable XP_CMDSHELL** (if disabled):
     ```sql
     EXEC sp_configure 'show advanced options', 1;
     RECONFIGURE;
     EXEC sp_configure 'xp_cmdshell', 1;
     RECONFIGURE;
     ```
  5. **Verify Mapping**:
     ```sql
     EXEC XP_CMDSHELL 'Dir S:';
     ```
  6. **Backup Database**:
     - Use SSMS backup GUI to save to mapped drive.

---

## Best Practices

1. **DataRules**:
   - Keep Rule Sets modular for reuse across multiple Parameter Lists.
   - Document Rule Set logic for audit and troubleshooting.
   - Test in a staging environment before applying to production.

2. **Data Validation**:
   - Align DAHS programming with DEP’s clarified criteria.
   - Maintain logs of one-minute averages for traceability.
   - Periodically review validation logic against regulatory updates.

3. **Database Backups**:
   - Ensure network permissions are correctly configured before mapping.
   - Disable XP_CMDSHELL after use to reduce security risks.
   - Verify backup integrity by restoring to a test environment.

---

## Source Attribution
- **[Document 1]:** Provided detailed explanation of DataRules architecture, required/optional task arguments, SQL table structures, and DataRulesEditor workflow.
- **[Document 2]:** Clarified PADEP Manual Rev. 8 hourly average validation criteria, regulatory context, and DAHS programming guidance.
- **[Document 3 & 4]:** Delivered identical step-by-step instructions for mapping a network drive to SQL Server for database backups, including XP_CMDSHELL configuration and verification commands.

---

Would you like me to also **integrate a visual workflow diagram** showing the relationship between DataRules configuration, data validation, and backup processes? That could make this guide more operationally intuitive.