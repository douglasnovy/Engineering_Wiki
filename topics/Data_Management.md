---
title: Data_Management
consolidated: true
sources: 8
conflicts: 0
confidence: 0.90
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPReportingNotesdocx_9a31f1eb.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SampleTests_ECMPSTestHistorypdf_95059768.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

# Consolidated Knowledge Base Entry  
**Title:** Data Management, Validation, and Migration Procedures for Environmental Monitoring Systems  

---

## Overview  
This document consolidates technical guidance on **data rules configuration**, **regulatory data validation**, **reporting requirements**, **fuel factor updates**, **test history tracking**, and **server/database migration procedures** for environmental monitoring systems such as StackVision and DAHS (Data Acquisition and Handling Systems). These processes are critical for ensuring **regulatory compliance**, **data integrity**, and **system performance** in continuous emissions monitoring and reporting environments.  

---

## Key Concepts  

### 1. Data Rules and Rule Sets  
- **Rule Sets**: Collections of data rules applied to parameters for validation, alarming, or processing.  
- **Parameter Lists**: Groupings of parameters to which a Rule Set can be applied.  
- **Execution**: Rule Sets are applied via the `DATARULES ProcessNow` task, specifying the Rule Set (`-rs`), Parameter List (`-pl`), and optionally real-time alarming (`-r`).  
- **Storage**: Rules and parameter lists are stored in SQL tables (`dbo.DataRulesRule`, `dbo.DataRulesParameterList`).  

### 2. Regulatory Data Validation (PADEP Rev. 8)  
- **Valid Data Reading**: Defined as a valid one-minute average.  
- **Hourly Averages**: Must be calculated and validated according to PADEP’s Continuous Source Monitoring Manual, Revision 8.  
- **Clarification Purpose**: To ensure DAHS systems are programmed to calculate hourly averages correctly for compliance.  

### 3. Reporting Requirements (PADEP)  
- **Reason and Action Codes**: Required for each hour; use RC=8 for normal operation.  
- **Missing Values**: Enter `0` for missing PADEP parameter values.  
- **Process Completion**: Ensure PADEP PN process finishes before running the PADEP EDR (Electronic Data Report) to check for errors.  

### 4. Fuel Factor Updates  
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on hourly data for coal and gas usage.  
- **Data Tracking**: Includes before/after values for parameters such as heat input, CO₂, flow, NOx, Hg, and SO₂.  

### 5. Test History Tracking (ECMPS)  
- **Test Records**: Maintain logs of QA, diagnostic, and other test types, including test number, date/time, reason, and result.  
- **Submission Status**: Track whether tests have been submitted to EPA Host System.  

### 6. Server and Database Migration  
- **DataLink Table Growth Issue**: If DataLink is installed but not configured, `dbo.AverageValueLog` can grow uncontrollably.  
- **Mitigation**: Configure `dbo.AverageValueLogConfig` with appropriate values (e.g., `1` and `6`) to limit logging to one parameter at hourly intervals; truncate table if already oversized.  
- **Network Drive Mapping for Backups**:  
  - Share target folder on the network.  
  - Map network drive on old server.  
  - Use SQL `XP_CMDSHELL` to connect to the mapped drive.  
  - Enable `xp_cmdshell` if disabled.  
  - Verify mapping and perform backups via SSMS.  

---

## Technical Details  

### DataRules SQL Tables  
- **dbo.DataRulesRule** – Stores Rule Sets.  
- **dbo.DataRulesParameterList** – Stores Parameter Lists.  
- **dbo.AlarmNotificationConfig** – Stores alarm settings.  
- **dbo.EmailAddressList** – Stores email notification lists.  

### PADEP Validation Criteria  
- **Hourly Average Validity**: Requires valid one-minute averages for inclusion.  
- **Manual Reference**: Page 64, sections 4.a and 4.b of PADEP Manual Rev. 8.  

### Fuel Factor Calculation Parameters  
- **Gas and Coal Heat Input**  
- **CO₂ Emissions**  
- **Flow Rates**  
- **NOx, Hg, SO₂ Emissions**  
- **Fuel Factor (FF Gas, FF Coal)**  

### SQL Commands for Migration  
```sql
-- Map network drive
EXEC XP_CMDSHELL 'net use S: \\RemoteServerName\ShareName /user:USERNAME PASSWORD';

-- Enable xp_cmdshell if needed
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;

-- Verify mapping
EXEC XP_CMDSHELL 'Dir S:';

-- Truncate oversized log table
TRUNCATE TABLE AverageValueLog;
```

---

## Best Practices  

1. **Data Rules Management**  
   - Keep Rule Sets modular and reusable.  
   - Regularly review Parameter Lists for completeness.  
   - Test Rule Sets in a staging environment before production deployment.  

2. **Regulatory Compliance**  
   - Follow PADEP’s definition of valid data strictly.  
   - Maintain complete hourly records with reason/action codes.  
   - Validate DAHS programming against regulatory criteria.  

3. **Database Maintenance**  
   - Monitor `AverageValueLog` table size if DataLink is installed.  
   - Configure logging parameters to prevent uncontrolled growth.  
   - Schedule regular backups to network locations during migrations.  

4. **Fuel Factor Updates**  
   - Document before/after changes for audit purposes.  
   - Verify calculations for each fuel type.  

5. **Test History Management**  
   - Keep detailed records of all QA and diagnostic tests.  
   - Track submission status to EPA systems.  

---

## Source Attribution  

- **[Document 1: DataRules Whitepaper]** – Provided foundational concepts and SQL table structures for DataRules, including Rule Set and Parameter List management.  
- **[Document 2: PADEP Data Validation Clarification]** – Clarified PADEP’s definition of valid data and hourly average validation requirements.  
- **[Document 3: PADEP Reporting Notes]** – Outlined operational reporting requirements, including reason/action codes and missing value handling.  
- **[Document 4: Boswell Fuel Factor Updates]** – Supplied detailed fuel factor adjustment data and parameters.  
- **[Document 5: ECMPS Test History]** – Provided structure and requirements for maintaining test history records.  
- **[Document 6: DataLink Logging Issue]** – Identified potential database growth issue and mitigation steps.  
- **[Document 7 & 8: Mapping Network Drive for Backups]** – Delivered step-by-step instructions for mapping network drives in SQL for database backups during migrations.  

---

If you’d like, I can also create a **process flow diagram** that visually connects **data rules application**, **validation**, **reporting**, and **migration** steps for operational clarity. Would you like me to prepare that?

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

# Consolida...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
