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
This consolidated knowledge base entry provides a comprehensive guide to managing, validating, and migrating data within Continuous Source Monitoring (CSM) environments, particularly for systems such as StackVision and related SQL-based data handling tools. It integrates procedures for defining and applying data rules, ensuring compliance with Pennsylvania Department of Environmental Protection (PADEP) Revision 8 data validation requirements, managing fuel factor updates, performing ECMPS test history checks, and executing safe server migrations with SQL database backups.

Effective data management in CSM systems is critical for regulatory compliance, operational efficiency, and maintaining data integrity during system changes or migrations.

---

### Key Concepts

1. **Data Rules and Rule Sets**
   - Rule Sets define conditions and logic for data validation and alarming.
   - Parameter Lists group parameters to which Rule Sets can be applied.
   - Rule Sets are independent of parameters; they are linked during task creation.

2. **PADEP Data Validation**
   - PADEP Rev 8 clarifies hourly average validation requirements.
   - A valid data reading corresponds to a valid one-minute average.
   - Facilities must ensure proper coding/calculation in their DAHS.

3. **Fuel Factor Updates**
   - Fuel factor calculations require accurate hourly data for parameters such as heat input, flow, and emissions.
   - Updates must be validated for missing, invalid, or suspect data.

4. **ECMPS Test History**
   - ECMPS Client Tool tracks QA and diagnostic test history.
   - Test results must be verified before EPA submission.

5. **Server Migration and SQL Backups**
   - Migrations may require mapping network drives for database backups.
   - DataLink configuration must be managed to prevent uncontrolled table growth.

---

### Technical Details

#### 1. DataRules Operation
- **SQL Tables Used:**
  - `dbo.DataRulesRule` – Stores Rule Sets.
  - `dbo.DataRulesParameterList` – Stores Parameter Lists.
  - `dbo.AlarmNotificationConfig` – Stores alarm settings.
  - `dbo.EmailAddressList` – Stores email notification lists.
- **Task Arguments:**
  - Required: `-rs` (Rule Set), `-pl` (Parameter List)
  - Optional: `-r` (Real-time alarming)
- **Example:** Applying `MINVELOCITY` Rule Set to `VELOCITY` Parameter List with real-time alarming enabled.

#### 2. PADEP Validation Requirements
- Hourly averages must be based on valid one-minute averages.
- Reason and action codes must be entered for each hour (RC=8 for normal operation).
- Missing values must be filled with zero for PADEP parameters.
- Run PADEP PN and EDR processes to check for errors before submission.

#### 3. Fuel Factor Update Process
- Maintain accurate hourly data for coal/gas heat input, CO₂, NOx, Hg, SO₂ emissions.
- Validate data for missing, invalid, suspect, or maintenance flags.
- Ensure calculated fuel factors match expected values; investigate discrepancies.

#### 4. ECMPS Test History Verification
- Use ECMPS Client Tool to review test history.
- Confirm QA and diagnostic tests have passed before EPA submission.
- Ensure DAHS verification is complete.

#### 5. Server Migration Procedures
- **Mapping Network Drive in SQL:**
  1. Share target folder on network.
  2. Map network drive in Windows (e.g., S:).
  3. Use SQL `XP_CMDSHELL` to connect:
     ```sql
     EXEC XP_CMDSHELL 'net use S: \\RemoteServerName\ShareName /user:USERNAME PASSWORD'
     ```
  4. Enable `XP_CMDSHELL` if disabled:
     ```sql
     EXEC sp_configure 'show advanced options', 1;
     RECONFIGURE;
     EXEC sp_configure 'xp_cmdshell', 1;
     RECONFIGURE;
     ```
  5. Verify mapping:
     ```sql
     EXEC XP_CMDSHELL 'Dir S:'
     ```
  6. Backup databases via SSMS to mapped drive.
- **DataLink Configuration Fix:**
  - If `dbo.AverageValueLogConfig` is blank, set first box to `1` and second to `6` to limit logging.
  - Truncate `dbo.AverageValueLog` if table size is excessive:
    ```sql
    TRUNCATE TABLE AverageValueLog
    ```

---

### Best Practices

- **DataRules:**
  - Keep Rule Sets modular and reusable.
  - Regularly review Parameter Lists for accuracy.
  - Test Rule Sets in non-production environments before deployment.

- **PADEP Compliance:**
  - Automate reason/action code entry where possible.
  - Validate one-minute averages before hourly aggregation.
  - Maintain documentation of validation logic for audits.

- **Fuel Factor Management:**
  - Implement automated checks for missing or suspect data.
  - Cross-verify fuel factor calculations with historical baselines.

- **ECMPS Testing:**
  - Schedule regular QA tests and maintain logs.
  - Resolve all DAHS verification issues before EPA submission.

- **Server Migration:**
  - Plan migrations during low-load periods.
  - Verify network permissions before mapping drives.
  - Keep backups in multiple secure locations.
  - Monitor DataLink logging to prevent database bloat.

---

### Source Attribution

- **[Document 1: DataRules Whitepaper]**
  - Provided foundational concepts and SQL table structure for DataRules.
  - Detailed task arguments and DataRulesEditor usage.

- **[Document 2: PADEP Data Validation Clarification]**
  - Clarified PADEP Rev 8 hourly average validation requirements.
  - Defined "valid data reading" as a valid one-minute average.

- **[Document 3: PADEP Reporting Notes]**
  - Specified reason/action code requirements and error-checking procedures.

- **[Document 4: Fuel Factor Updates]**
  - Listed parameters and validation flags for fuel factor calculations.

- **[Document 5: ECMPS Test History]**
  - Outlined test history reporting and verification steps.

- **[Document 6: DataLink Configuration Issue]**
  - Identified uncontrolled table growth issue and provided SQL fix.

- **[Document 7 & 8: Mapping Network Drive to SQL for Backups]**
  - Provided step-by-step instructions for mapping drives and backing up databases during migrations.

---

If you’d like, I can also create a **visual workflow diagram** showing the relationship between DataRules, PADEP validation, fuel factor updates, ECMPS testing, and migration procedures to make this guide easier to follow. Would you like me to add that?

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls](../tools/engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls)** (0.08 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - It integrates procedures for defining and applying...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
