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
This consolidated knowledge base entry provides a comprehensive guide to managing data rules, validating environmental monitoring data, and executing server migration procedures for Continuous Source Monitoring Systems (CSMS) such as StackVision. It integrates operational guidance for rule-based data processing, compliance with Pennsylvania Department of Environmental Protection (PADEP) Revision 8 requirements, fuel factor updates, test history tracking, and best practices for database backup during server migrations. The goal is to ensure accurate data handling, regulatory compliance, and smooth infrastructure transitions.

---

## Key Concepts

### 1. Data Rules
- **Rule Sets**: Collections of data rules that can be applied to multiple parameters.
- **Parameter Lists**: Groups of parameters to which a single Rule Set can be applied.
- **Independence of Rules and Parameters**: Rule Sets are not inherently tied to parameters; association occurs during task creation.
- **SQL Integration**: DataRules uses SQL directly for faster processing compared to legacy systems like CNDMGR.

### 2. Data Validation (PADEP Rev 8)
- **Valid Data Reading**: Defined as a valid one-minute average.
- **Hourly Average Validation**: Criteria clarified by DEP to ensure DAHS systems calculate and code averages correctly.
- **Regulatory Context**: Policies supplement existing requirements but do not replace regulations.

### 3. PADEP Reporting
- **Reason and Action Codes**: Must be coded for each hour (RC=8 for normal operation).
- **Missing Values**: Fill with zero for PADEP parameters.
- **Process Completion**: Ensure PADEP PN process finishes before running EDR error checks.

### 4. Fuel Factor Updates
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on hourly data for coal and gas.
- **Parameter Tracking**: Includes heat input, CO₂ emissions, flow rates, NOx, Hg, and SO₂ metrics.

### 5. Test History Tracking (ECMPS)
- **QA and Diagnostic Tests**: Record and track test results, reasons, and submission status.
- **Regulatory Submission**: Ensure tests are submitted to EPA when required.

### 6. Server Migration and Database Backup
- **DataLink Configuration Issue**: Incorrect or blank configuration can cause uncontrolled table growth.
- **Network Drive Mapping**: Required when local storage is insufficient for backups.
- **SQL Commands for Mapping**: Use `XP_CMDSHELL` and `sp_configure` to enable and map drives.
- **Backup Execution**: Perform backups via SSMS to mapped network locations.

---

## Technical Details

### DataRules Task Creation
**Required Arguments:**
- `-rs` : Rule Set name
- `-pl` : Parameter List name

**Optional Argument:**
- `-r` : Real-time alarming flag

**Example:**
```
DATARULES ProcessNow -rs MINVELOCITY -pl VELOCITY -r
```

**SQL Tables Used:**
- `dbo.DataRulesRule` – Stores Rule Sets
- `dbo.DataRulesParameterList` – Stores Parameter Lists
- `dbo.AlarmNotificationConfig` – Stores alarm settings
- `dbo.EmailAddressList` – Stores email lists

---

### PADEP Data Validation Criteria
- **Hourly Average Validity**: Must be based on valid one-minute averages.
- **Stringency Option**: Facilities may petition DEP for more stringent criteria.
- **DAHS Programming**: Ensure correct coding/calculation of averages per DEP guidance.

---

### PADEP Reporting Workflow
1. Assign reason/action codes for each hour.
2. Use RC=8 for normal operation.
3. Fill missing PADEP parameter values with zero.
4. Complete PADEP PN process.
5. Run PADEP EDR to identify and correct errors.

---

### Fuel Factor Update Procedure
- Review hourly data for coal and gas usage.
- Update fuel factor values (`FF Gas`, `FF Coal`) based on heat input and emissions data.
- Track differences (`DIFF`) and ensure consistency across parameters.

---

### ECMPS Test History Management
- Record unit/stack/pipe IDs, test numbers, types, dates, and reasons.
- Log test results and availability.
- Maintain submission status to EPA.

---

### Server Migration – DataLink Issue Resolution
1. **Identify Tables**: `dbo.AverageValueLog` and `dbo.AverageValueLogConfig`.
2. **Edit Config**: If blank, set first box to `1` and second to `6` to limit logging.
3. **Truncate Large Tables**: Use `TRUNCATE TABLE AverageValueLog` in StackVision DB.

---

### Mapping a Network Drive to SQL
1. Share target folder on network.
2. Map network drive in Windows (e.g., `S:`).
3. In SQL:
   ```
   EXEC XP_CMDSHELL 'net use S: \\RemoteServer\Share /user:USERNAME PASSWORD'
   ```
4. Enable `XP_CMDSHELL` if disabled:
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
6. Backup database via SSMS to mapped drive.

---

## Best Practices
- **DataRules**: Keep Rule Sets and Parameter Lists well-documented; avoid redundant rules.
- **Validation**: Align DAHS programming with DEP guidance; periodically audit averages.
- **Reporting**: Automate reason/action code assignment where possible.
- **Fuel Factors**: Regularly review and update based on operational changes.
- **Test History**: Maintain complete records for compliance audits.
- **Server Migration**: Always check DataLink configuration post-install; map drives securely with proper permissions.
- **Backups**: Test backup and restore procedures before migration.

---

## Source Attribution
- **Document 1 (DataRules Whitepaper)**: Provided foundational concepts, SQL table structures, and task creation procedures for DataRules.
- **Document 2 (PADEP Data Validation Clarification)**: Clarified DEP criteria for valid hourly averages and DAHS programming requirements.
- **Document 3 (PADEP Reporting Notes)**: Detailed reporting workflow, reason/action codes, and error checking.
- **Document 4 (Fuel Factor Updates)**: Supplied structure and parameters for fuel factor adjustments.
- **Document 5 (ECMPS Test History)**: Outlined test tracking and submission requirements.
- **Document 6 (DataLink Issue Email)**: Identified DataLink configuration issue and resolution steps.
- **Documents 7 & 8 (Mapping Network Drive to SQL)**: Provided step-by-step instructions for mapping drives and backing up databases during server migration.

---

Would you like me to also create a **visual workflow diagram** that integrates DataRules processing, PADEP validation, and server migration steps for quick reference? That could make this knowledge base entry more actionable.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls](../tools/engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls)** (0.08 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

## Title
**...
- [[Environmental]] - It integrates operational guidance for rule-based ...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
