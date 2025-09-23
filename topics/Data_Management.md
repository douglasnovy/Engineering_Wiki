---
title: Data_Management
consolidated: true
sources: 8
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPReportingNotesdocx_9a31f1eb.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_ECMPSTestHistorypdf_95059768.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

## Title
**Data Management, Validation, and Server Migration Procedures for Continuous Source Monitoring Systems**

---

## Overview
This consolidated knowledge base entry provides a comprehensive guide to managing environmental monitoring data, validating continuous source monitoring results, and performing essential server migration tasks for StackVision and related systems. It integrates procedures for **DataRules configuration**, **Pennsylvania Department of Environmental Protection (PADEP) data validation and reporting**, **fuel factor updates**, **ECMPS test history tracking**, and **SQL-based server migration techniques**. The goal is to ensure accurate data handling, compliance with regulatory requirements, and smooth operational transitions during system upgrades or migrations.

---

## Key Concepts

### 1. DataRules Framework
- **Rule Sets**: Collections of data rules applied to parameters.
- **Parameter Lists**: Groups of parameters to which Rule Sets can be applied.
- **Process Execution**: Rule Sets are applied via the `DATARULES ProcessNow` task, specifying Rule Set (`-rs`), Parameter List (`-pl`), and optional real-time alarming (`-r`).
- **SQL Integration**: DataRules uses SQL directly for faster execution compared to CNDMGR.

### 2. PADEP Data Validation
- **Valid Data Reading**: Defined as a valid one-minute average.
- **Hourly Average Validation**: Criteria outlined in PADEP Continuous Source Monitoring Manual Revision No. 8.
- **Supplemental Guidance**: Clarification documents provide examples for DAHS programming to ensure proper coding/calculation.

### 3. PADEP Reporting Requirements
- **Reason and Action Codes**: Must be coded for each hour; use RC=8 for normal operation.
- **Missing Values**: Fill with `0` for PADEP parameters.
- **Process Completion**: Ensure PADEP PN process finishes before running EDR error checks.

### 4. Fuel Factor Updates
- **Prorated Fuel Factor**: Adjustments to coal and gas fuel factors based on hourly data.
- **Parameter Tracking**: Includes heat input, CO₂, flow rates, NOx, Hg, SO₂, and calculated fuel factors.

### 5. ECMPS Test History
- **Test Tracking**: Records QA, diagnostic, and other test results for units/stacks.
- **Submission Status**: Indicates whether tests have been submitted to EPA.
- **Facility Metadata**: Includes facility name, location, and ORISPL ID.

### 6. Server Migration & SQL Network Drive Mapping
- **Backup Location Constraints**: Limited local disk space may require network-based backups.
- **Network Drive Mapping**: Map a network location to SQL Server for direct backups.
- **DataLink Configuration Issue**: Incorrect or blank configuration can cause uncontrolled table growth in `dbo.AverageValueLog`.

---

## Technical Details

### DataRules SQL Tables
- `dbo.DataRulesRule`: Stores Rule Sets.
- `dbo.DataRulesParameterList`: Stores Parameter Lists.
- `dbo.AlarmNotificationConfig`: Stores alarm settings.
- `dbo.EmailAddressList`: Stores email notification lists.

**Parameter List Creation**:
- Created in DataRulesEditor (Excel).
- Copied into SQL via SSMS.

**Example Command**:
```bash
DATARULES ProcessNow -rs MINVELOCITY -pl VELOCITY -r
```

---

### PADEP Data Validation Criteria
- **Hourly Average Validity**: Must be based on valid one-minute averages.
- **Manual Reference**: Page 64, sections 4.a and 4.b of PADEP Manual Rev. 8.
- **Flexibility**: DEP may allow more stringent criteria upon petition.

---

### PADEP Reporting Workflow
1. Assign reason/action codes for each hour.
2. Enter RC=8 for normal operations.
3. Fill missing PADEP parameter values with `0`.
4. Complete PADEP PN process.
5. Run PADEP EDR to identify and correct errors.

---

### Fuel Factor Update Procedure
- Compare **before** and **after** values for fuel factors.
- Adjust `FF Gas` and `FF Coal` based on updated heat input and flow data.
- Monitor emissions parameters for compliance.

---

### ECMPS Test History Reporting
- Maintain records of all QA and diagnostic tests.
- Verify submission status to EPA.
- Include facility identifiers and test metadata.

---

### SQL Network Drive Mapping for Backups
**Steps**:
1. Share target folder on network.
2. Map network drive on old server.
3. In SQL Server, run:
```sql
EXEC XP_CMDSHELL 'net use S: \\RemoteServer\Share /user:USERNAME PASSWORD'
```
4. Enable `xp_cmdshell` if disabled:
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
6. Perform backup via SSMS GUI.

---

### DataLink Configuration Fix
- **Issue**: Blank `dbo.AverageValueLogConfig` causes excessive logging.
- **Solution**:
  - Edit top 200 records in `dbo.AverageValueLogConfig`.
  - Set first box to `1`, second box to `6` (hourly logging for one parameter).
  - If table is large, truncate:
```sql
TRUNCATE TABLE dbo.AverageValueLog;
```
*(Ensure correct database selection before truncation.)*

---

## Best Practices
- **DataRules**: Keep Rule Sets generic and apply them via Parameter Lists for flexibility.
- **Validation**: Align DAHS programming with PADEP criteria to avoid compliance issues.
- **Reporting**: Automate reason/action code assignment where possible.
- **Fuel Factor**: Regularly review and update based on operational changes.
- **Testing**: Maintain complete ECMPS test records for audits.
- **Migration**: Always verify network drive mapping before initiating backups.
- **DataLink**: Configure logging parameters to prevent uncontrolled table growth.

---

## Source Attribution
- **Document 1**: Provided DataRules architecture, SQL table definitions, and task execution examples.
- **Document 2**: Clarified PADEP hourly average validation criteria and DAHS programming guidance.
- **Document 3**: Detailed PADEP reporting requirements and workflow.
- **Document 4**: Supplied fuel factor update data structure and parameters.
- **Document 5**: Outlined ECMPS test history reporting format and metadata.
- **Document 6**: Identified DataLink configuration issue and SQL fix procedure.
- **Documents 7 & 8**: Delivered step-by-step SQL network drive mapping instructions for server migration backups.

---

Would you like me to also create a **visual workflow diagram** showing the relationship between DataRules, PADEP validation, and server migration tasks? This could help operators see the end-to-end process more clearly.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls](../tools/engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls)** (0.08 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

## Title
**...
- [[Environmental]] - It integrates procedures for **DataRules configura...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
