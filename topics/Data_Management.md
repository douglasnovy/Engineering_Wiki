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
This consolidated knowledge base entry provides a comprehensive guide to managing data rules, validating environmental monitoring data, and performing server migration tasks for Continuous Source Monitoring Systems (CSMS) such as StackVision. It integrates procedures for configuring rule sets, ensuring compliance with Pennsylvania Department of Environmental Protection (PADEP) data validation requirements, managing fuel factor updates, and executing safe and efficient database backups during server migrations. The goal is to ensure accurate data acquisition, regulatory compliance, and system integrity during operational and infrastructure changes.

---

### Key Concepts

#### 1. **Data Rules and Rule Sets**
- **Rule Sets**: Collections of data rules applied to parameters for validation, alarming, or other processing.
- **Parameter Lists**: Groupings of parameters to which a single Rule Set can be applied.
- **Independence**: Rule Sets are not inherently tied to parameters; they are linked during task creation.
- **Execution**: Rule Sets are applied via the `DATARULES ProcessNow` task, specifying Rule Set (`-rs`), Parameter List (`-pl`), and optional real-time alarming (`-r`).

#### 2. **Data Validation**
- **Valid Data Reading**: Defined by PADEP as a valid one-minute average.
- **Hourly Averages**: Must be calculated and coded correctly in Data Acquisition and Handling Systems (DAHS).
- **Reason and Action Codes**: Required for each hour; RC=8 for normal operation.
- **Missing Values**: Must be filled with zero for PADEP parameters.

#### 3. **Fuel Factor Updates**
- **Prorated Fuel Factor**: Adjustments to fuel factor values based on hourly operational data (coal/gas usage, heat input, emissions).
- **Data Integrity**: Requires careful tracking of before/after values for multiple parameters to ensure accuracy.

#### 4. **Server Migration and Database Backup**
- **Network Drive Mapping**: Necessary when local storage is insufficient for backups.
- **SQL Integration**: Mapping drives within SQL Server using `XP_CMDSHELL` commands.
- **DataLink Configuration**: Prevents uncontrolled growth of `AverageValueLog` table by setting appropriate logging parameters.

---

### Technical Details

#### DataRules System
- **SQL Tables**:
  - `dbo.DataRulesRule`: Stores Rule Sets.
  - `dbo.DataRulesParameterList`: Stores Parameter Lists.
  - `dbo.AlarmNotificationConfig`: Stores alarm settings.
  - `dbo.EmailAddressList`: Stores email notification lists.
- **Creation Process**:
  - Rule Sets and Parameter Lists are created in `DataRulesEditor` (Excel).
  - Data is copied into SQL tables via SQL Server Management Studio (SSMS).

#### PADEP Data Validation
- **Manual Reference**: Continuous Source Monitoring Manual Revision No. 8.
- **Coding Requirements**:
  - Reason Code (RC) and Action Code (AC) for each hour.
  - RC=8 for normal operation.
  - Zero-fill missing PADEP parameter values.
- **Validation Logic**:
  - Hourly averages must be based on valid one-minute averages.
  - Facilities may petition for more stringent validation criteria.

#### Fuel Factor Updates
- **Parameters Monitored**:
  - Unit operational status (coal/gas on/off).
  - Heat input, CO₂, flow rates.
  - Emission rates (NOx, Hg, SO₂).
- **Update Process**:
  - Compare "Before" and "After" values.
  - Calculate differences and adjust fuel factor accordingly.

#### Server Migration Procedures
- **Mapping Network Drive**:
  1. Share target folder on new server.
  2. Map network drive on old server via File Explorer.
  3. Use SQL `XP_CMDSHELL` to connect mapped drive.
  4. Enable `xp_cmdshell` if disabled.
  5. Verify mapping with `Dir` command in SQL.
- **DataLink Table Management**:
  - If `AverageValueLogConfig` is blank, set first box to `1` and second to `6` to log changes hourly for one parameter.
  - Truncate `AverageValueLog` if table size is excessive.

---

### Best Practices
1. **DataRules**:
   - Maintain clear documentation of Rule Sets and Parameter Lists.
   - Test rules in a staging environment before production deployment.
2. **Data Validation**:
   - Regularly audit DAHS coding for compliance with PADEP requirements.
   - Ensure zero-filling of missing values to prevent reporting errors.
3. **Fuel Factor Management**:
   - Keep historical records of fuel factor changes for audit purposes.
   - Validate calculations against operational logs.
4. **Server Migration**:
   - Always verify network permissions before mapping drives.
   - Backup databases to secure, accessible network locations.
   - Manage DataLink logging to prevent database bloat.
5. **Regulatory Compliance**:
   - Follow PADEP guidelines strictly; petition for exceptions only with strong justification.
   - Document all deviations from standard procedures.

---

### Source Attribution
- **Document 1 (DataRules Whitepaper)**: Provided foundational concepts, SQL table structures, and operational procedures for DataRules.
- **Document 2 (PADEP Data Validation Clarification)**: Clarified PADEP’s definition of valid data readings and requirements for hourly averages.
- **Document 3 (PADEP Reporting Notes)**: Added specific coding requirements for PADEP reporting, including reason/action codes and zero-filling.
- **Document 4 (Boswell Fuel Factor Updates)**: Detailed fuel factor update process with parameter tracking.
- **Document 6 (Item to Check in Migration Databases)**: Highlighted DataLink configuration issues and solutions to prevent uncontrolled table growth.
- **Document 7 & 8 (Mapping a Network Drive to SQL)**: Provided step-by-step instructions for mapping network drives in SQL for database backups during server migration.

---

Would you like me to also create a **visual workflow diagram** that shows how DataRules, PADEP validation, and server migration tasks interconnect? This could make the consolidated process easier to follow.

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

### Title
*...
- [[Environmental]] - It integrates procedures for configuring rule sets...
