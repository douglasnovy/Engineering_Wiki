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
This consolidated knowledge base entry provides a comprehensive guide to managing, validating, and migrating data within Continuous Source Monitoring (CSM) environments, specifically focusing on **DataRules configuration**, **Pennsylvania Department of Environmental Protection (PADEP) data validation and reporting requirements**, **fuel factor updates**, **ECMPS test history tracking**, and **SQL-based server migration procedures**.  
The goal is to ensure accurate environmental compliance reporting, maintain database integrity, and optimize operational efficiency during both routine and transitional phases.

---

### Key Concepts

#### 1. **DataRules Framework**
- **Rule Sets**: Collections of data rules that define validation or processing logic.
- **Parameter Lists**: Groups of parameters to which a Rule Set can be applied.
- **Independence of Rules and Parameters**: Rule Sets are not inherently tied to parameters; linkage occurs during task creation.
- **SQL Integration**: DataRules uses SQL directly for faster execution compared to legacy tools like CNDMGR.

#### 2. **PADEP Data Validation**
- **Valid Data Reading**: Defined as a valid one-minute average.
- **Hourly Average Validation**: Criteria outlined in PADEP Continuous Source Monitoring Manual, Revision No. 8.
- **Supplemental Guidance**: Clarification documents provide examples and programming guidance for DAHS configuration.

#### 3. **PADEP Reporting Requirements**
- **Reason and Action Codes**: Must be coded for each hour (RC=8 for normal operation).
- **Missing Values**: Enter “0” for missing PADEP parameter values.
- **Process Completion**: Ensure PADEP PN process finishes before running EDR error checks.

#### 4. **Fuel Factor Updates**
- **Prorated Fuel Factor Calculations**: Adjustments to fuel factor values for coal and gas based on hourly operational data.
- **Data Integrity Checks**: Identify missing, invalid, or suspect values before applying updates.

#### 5. **ECMPS Test History**
- **QA and Diagnostic Tests**: Track test results, reasons, and submission status.
- **EPA Submission**: Ensure tests are submitted to EPA host systems when required.

#### 6. **Server Migration and SQL Backup**
- **DataLink Table Management**: Prevent uncontrolled growth of `dbo.AverageValueLog` by configuring `dbo.AverageValueLogConfig`.
- **Network Drive Mapping for Backups**: Map a network drive to SQL Server for direct database backup to remote storage.
- **XP_CMDSHELL Usage**: Enable and use for network drive mapping commands.

---

### Technical Details

#### **DataRules Configuration**
1. **SQL Tables Used**:
   - `dbo.DataRulesRule` – Stores Rule Sets.
   - `dbo.DataRulesParameterList` – Stores Parameter Lists.
   - `dbo.AlarmNotificationConfig` – Stores alarm settings.
   - `dbo.EmailAddressList` – Stores email notification lists.
2. **Task Arguments**:
   - Required: `-rs` (Rule Set), `-pl` (Parameter List)
   - Optional: `-r` (Real-time alarming)
3. **DataRulesEditor**:
   - Create Rule Sets and Parameter Lists in Excel.
   - Copy directly to SQL via SSMS.

#### **PADEP Validation Procedures**
- Program DAHS to calculate hourly averages from valid one-minute averages.
- Petition DEP for more stringent criteria if desired.
- Follow Manual Rev. 8 guidelines for data reduction and validation.

#### **Fuel Factor Update Process**
- Review hourly operational data for coal/gas usage.
- Calculate prorated fuel factors (`FF Gas`, `FF Coal`) based on heat input and flow data.
- Correct missing or invalid entries before applying updates.

#### **ECMPS Test History Management**
- Maintain records of QA and diagnostic tests.
- Verify submission status to EPA.
- Include facility identifiers and test reasons in documentation.

#### **Server Migration Steps**
1. **DataLink Configuration**:
   - Edit `dbo.AverageValueLogConfig` to limit logging scope.
   - Truncate `dbo.AverageValueLog` if oversized.
2. **Network Drive Mapping**:
   - Share target folder on new server.
   - Map drive via File Explorer.
   - Use SQL `XP_CMDSHELL` to connect mapped drive.
   - Backup databases via SSMS to mapped location.

---

### Best Practices
- **DataRules**: Keep Rule Sets modular and reusable across Parameter Lists.
- **Validation**: Always confirm one-minute averages before calculating hourly averages.
- **Reporting**: Automate reason/action code entry to reduce manual errors.
- **Fuel Factor Updates**: Implement automated integrity checks before recalculating fuel factors.
- **Test History**: Maintain a centralized repository for QA/diagnostic test records.
- **Migration**: Configure DataLink before migration to prevent excessive logging; ensure XP_CMDSHELL is enabled only when necessary for security reasons.

---

### Source Attribution
- **[Document 1: DataRules Whitepaper]**: Provided foundational concepts, SQL table structures, and task configuration for DataRules.
- **[Document 2: PADEP Data Validation Clarification]**: Clarified PADEP hourly average validation criteria and DAHS programming guidance.
- **[Document 3: PADEP Reporting Notes]**: Detailed reporting requirements, reason/action codes, and error checking procedures.
- **[Document 4: Boswell Fuel Factor Updates]**: Supplied data structure and process for prorated fuel factor calculations.
- **[Document 5: ECMPS Test History]**: Outlined test tracking, QA/diagnostic procedures, and submission requirements.
- **[Document 6: Item to Check in Migration Databases]**: Highlighted DataLink configuration issues and mitigation steps.
- **[Document 7 & 8: Mapping a Network Drive to SQL for Database Backups]**: Provided step-by-step instructions for mapping network drives and backing up databases during migration.

---

I can also create a **visual workflow diagram** showing the relationship between DataRules configuration, PADEP validation, fuel factor updates, and migration procedures if you’d like.  
Do you want me to add that?

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - The goal is to ensure accurate environmental compl...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
