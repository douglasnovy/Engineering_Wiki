---
title: Data_Management
consolidated: true
sources: 8
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPReportingNotesdocx_9a31f1eb.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_ECMPSTestHistorypdf_95059768.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

### Title
**Data Management, Validation, and Server Migration Procedures for Continuous Source Monitoring Systems**

---

### Overview
This consolidated knowledge base entry provides a comprehensive guide to managing environmental monitoring data, validating continuous source monitoring results, and performing server migration tasks for StackVision and related systems. It integrates procedures for **DataRules configuration**, **Pennsylvania Department of Environmental Protection (PADEP) data validation and reporting**, **fuel factor updates**, **ECMPS test history tracking**, and **SQL-based server migration techniques**. These processes are critical for ensuring regulatory compliance, maintaining data integrity, and enabling efficient system transitions.

---

### Key Concepts

1. **DataRules Framework**  
   - **Rule Sets**: Collections of data rules applied to parameters without being inherently tied to them.  
   - **Parameter Lists**: Groupings of parameters to which a single Rule Set can be applied.  
   - **ProcessNow Tasks**: Execution units specifying Rule Set (`-rs`), Parameter List (`-pl`), and optional real-time alarming (`-r`).  
   - **SQL Integration**: Direct SQL application of rules for speed and simplicity compared to CNDMGR.

2. **Data Validation (PADEP Rev. 8)**  
   - **Valid Data Reading**: Defined as a valid one-minute average.  
   - **Hourly Average Validation**: Clarified procedures for DAHS programming to ensure correct coding/calculation.  
   - **Supplemental Guidance**: Policies supplement existing regulations but do not override them.

3. **PADEP Reporting Requirements**  
   - **Reason and Action Codes**: Must be coded for each hour (RC=8 for normal operation).  
   - **Missing Values**: Fill with zero for PADEP parameters.  
   - **Process Completion**: Ensure PADEP PN finishes before running EDR error checks.

4. **Fuel Factor Updates**  
   - **Prorated Fuel Factor Calculations**: Hourly data adjustments for coal and gas parameters, including heat input, CO₂, NOx, Hg, and SO₂ metrics.  
   - **Data Quality Flags**: Missing, invalid, suspect, maintenance, and calculated error indicators.

5. **ECMPS Test History Tracking**  
   - **Test Metadata**: Includes unit/stack IDs, test numbers, types, reasons, results, and submission status.  
   - **Regulatory Submission**: Tracks whether tests have been submitted to EPA.

6. **Server Migration and SQL Network Drive Mapping**  
   - **DataLink Table Management**: Prevent uncontrolled growth of `dbo.AverageValueLog` by configuring `dbo.AverageValueLogConfig`.  
   - **Network Drive Mapping**: Map drives in SQL using `XP_CMDSHELL` for direct database backups to network locations.  
   - **Backup Procedures**: Use SSMS GUI to back up databases to mapped network drives.

---

### Technical Details

#### DataRules SQL Tables
- `dbo.DataRulesRule`: Stores Rule Sets.
- `dbo.DataRulesParameterList`: Stores Parameter Lists.
- `dbo.AlarmNotificationConfig`: Stores alarm settings.
- `dbo.EmailAddressList`: Stores email notification lists.

#### PADEP Hourly Average Validation
- **Manual Reference**: Page 64, sections 4.a and 4.b of PADEP Continuous Source Monitoring Manual Rev. 8.
- **Validation Logic**: Hourly averages must be based on valid one-minute readings.

#### Fuel Factor Update Workflow
- **Parameters**: UNIT4 GASON, COALON, GHEATIN, CO₂, FLOWSCFH, HEATIN, FUELFACT, NOx, Hg, SO₂.
- **Before/After Comparison**: Track changes in fuel factor calculations.
- **Quality Control**: Use flags to identify data issues.

#### SQL Network Drive Mapping Procedure
1. **Share Target Folder** on network location.
2. **Map Drive** in Windows Explorer on old server.
3. **Run SQL Command**:  
   ```sql
   EXEC XP_CMDSHELL 'net use S: \\RemoteServerName\ShareName /user:USERNAME PASSWORD';
   ```
4. **Enable XP_CMDSHELL** if disabled:
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
6. **Backup Database** via SSMS GUI.

#### DataLink Table Configuration
- **Edit `dbo.AverageValueLogConfig`**: Add `1` to first box and `6` to second box to limit logging to one parameter hourly.
- **Truncate Large Tables**:
   ```sql
   TRUNCATE TABLE AverageValueLog;
   ```

---

### Best Practices

- **DataRules**: Keep Rule Sets generic and reusable; maintain clear documentation of Parameter Lists.
- **Validation**: Align DAHS programming with PADEP guidance; ensure all hourly averages are based on valid minute data.
- **Reporting**: Always code reason/action for each hour; zero-fill missing values before submission.
- **Fuel Factor Updates**: Regularly audit before/after values; investigate discrepancies promptly.
- **Server Migration**: Map network drives securely; verify permissions before backup; disable unnecessary logging to conserve storage.
- **SQL Management**: Enable `XP_CMDSHELL` only when needed; revert configuration after use for security.

---

### Source Attribution

- **[Document 1: DataRules Whitepaper]**: Provided foundational concepts, SQL table structures, and task execution parameters for DataRules.
- **[Document 2: PADEP Data Validation Clarification]**: Clarified hourly average validation requirements and DAHS programming guidance.
- **[Document 3: PADEP Reporting Notes]**: Detailed reason/action code requirements and missing value handling for PADEP reporting.
- **[Document 4: Fuel Factor Updates]**: Supplied data structure and workflow for prorated fuel factor calculations.
- **[Document 5: ECMPS Test History]**: Outlined test tracking and submission status for EPA compliance.
- **[Document 6: Item to Check in Migration Databases]**: Highlighted DataLink table growth issue and SQL fix.
- **[Document 7 & 8: Mapping a Network Drive to SQL for Database Backups]**: Provided step-by-step SQL and Windows procedures for network drive mapping during server migration.

---

If you’d like, I can create a **visual workflow diagram** showing how DataRules, PADEP validation, and server migration tasks interconnect in a typical operational cycle. Would you like me to prepare that?

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - It integrates procedures for **DataRules configura...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
