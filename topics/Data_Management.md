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
This consolidated knowledge base entry provides a comprehensive guide to managing data rules, validating environmental monitoring data, and performing server migration tasks for Continuous Source Monitoring (CSM) systems such as StackVision. It integrates procedures for rule-based data processing, compliance with Pennsylvania Department of Environmental Protection (PADEP) data validation requirements, fuel factor updates, and best practices for database backup during server migrations. The goal is to ensure accurate data handling, regulatory compliance, and operational efficiency.

---

### Key Concepts

1. **Data Rules and Rule Sets**  
   - Rule Sets define conditions and actions for data processing.  
   - They are applied to Parameter Lists, which group related parameters.  
   - Only one Rule Set can be applied to a Parameter List at a time.  
   - Rule Sets are independent of parameters until applied via a task.

2. **Data Validation for Regulatory Compliance**  
   - PADEP requires validation of hourly averages based on valid one-minute averages.  
   - Reason and action codes must be assigned for each hour of data.  
   - Missing values must be explicitly coded (e.g., “0” for PADEP parameters).  
   - Validation ensures DAHS (Data Acquisition and Handling Systems) calculations meet regulatory criteria.

3. **Fuel Factor Updates**  
   - Fuel factors (e.g., for coal and gas) are calculated and updated hourly.  
   - Parameters include heat input, flow rates, and emissions data (NOx, SO₂, Hg).  
   - Updates require careful handling of missing, invalid, or suspect data flags.

4. **Server Migration and Database Backup**  
   - Backups may need to be stored on network drives due to local storage limitations.  
   - Mapping a network drive to SQL Server allows direct backup to remote storage.  
   - DataLink configuration issues can cause uncontrolled table growth if not properly set.

---

### Technical Details

#### DataRules Implementation
- **SQL Tables Used:**
  - `dbo.DataRulesRule` – Stores Rule Sets.
  - `dbo.DataRulesParameterList` – Stores Parameter Lists.
  - `dbo.AlarmNotificationConfig` – Stores alarm settings.
  - `dbo.EmailAddressList` – Stores email notification lists.
- **Task Arguments:**
  - Required: `-rs` (Rule Set), `-pl` (Parameter List)
  - Optional: `-r` (Real-time alarming)
- **Editor Workflow:**
  - Create Rule Sets and Parameter Lists in DataRulesEditor (Excel).
  - Copy data to SQL via SSMS.

#### PADEP Data Validation
- **Hourly Average Validation:**
  - A valid hourly average requires valid one-minute averages.
- **Coding Requirements:**
  - Reason Code (RC) of 8 for normal operation.
  - Action codes for each hour.
  - Fill missing values with “0” for PADEP parameters.
- **Reporting:**
  - Ensure PADEP PN process completes before running EDR (Electronic Data Report).

#### Fuel Factor Update Process
- **Parameters Monitored:**
  - Unit operation status (coal/gas on/off)
  - Heat input (GHEATIN, HEATIN)
  - CO₂, NOx, SO₂, Hg emissions
  - Flow rates (SCFH)
- **Data Quality Flags:**
  - Missing, Invalid, Suspect, Maintenance
- **Calculation:**
  - Fuel factors computed for coal and gas separately.
  - Differences tracked for QA purposes.

#### Server Migration Procedures
- **Mapping Network Drive to SQL:**
  1. Share target folder on new server.
  2. Map network drive on old server (e.g., S:).
  3. Use `XP_CMDSHELL` in SQL to connect to mapped drive.
  4. Enable `xp_cmdshell` if disabled via `sp_configure`.
  5. Verify mapping with `Dir S:`.
  6. Backup databases via SSMS to mapped location.
- **DataLink Table Growth Issue:**
  - If `dbo.AverageValueLogConfig` is blank, table logs all changes.
  - Fix: Set first box to `1`, second to `6` to limit logging.
  - If table is large, truncate with:
    ```sql
    TRUNCATE TABLE AverageValueLog;
    ```
    *(Ensure correct database selection before running)*

---

### Best Practices

- **DataRules:**
  - Keep Rule Sets modular for reuse across multiple Parameter Lists.
  - Test Rule Sets in a non-production environment before deployment.
  
- **Data Validation:**
  - Automate reason/action code assignment where possible.
  - Regularly audit DAHS calculations against regulatory criteria.
  
- **Fuel Factor Updates:**
  - Implement automated QA checks for missing or suspect data.
  - Maintain historical logs for fuel factor changes for compliance audits.
  
- **Server Migration:**
  - Always verify network permissions before mapping drives.
  - Document all configuration changes during migration.
  - Monitor table sizes post-migration to prevent uncontrolled growth.

---

### Source Attribution

- **[Document 1: DataRules Whitepaper]**  
  Provided foundational concepts and SQL table structures for DataRules, including task arguments and editor workflow.

- **[Document 2: PADEP Data Validation Clarification]**  
  Clarified PADEP’s requirements for hourly average validation and DAHS programming considerations.

- **[Document 3: PADEP Reporting Notes]**  
  Specified coding requirements for reason/action codes and handling missing values in PADEP reporting.

- **[Document 4: Boswell Fuel Factor Updates]**  
  Detailed parameters, data quality flags, and calculation methods for fuel factor updates.

- **[Document 6: Item to Check in Migration Databases]**  
  Identified DataLink configuration issues and provided SQL fixes to prevent uncontrolled table growth.

- **[Documents 7 & 8: Mapping a Network Drive to SQL for Database Backups]**  
  Provided step-by-step instructions for mapping network drives and enabling SQL commands for remote backups during server migration.

---

Would you like me to also create a **visual workflow diagram** that connects DataRules processing, PADEP validation, and server migration steps into a single operational process? This could make the relationships between these procedures clearer.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls](../tools/engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls)** (0.08 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - It integrates procedures for rule-based data proce...
