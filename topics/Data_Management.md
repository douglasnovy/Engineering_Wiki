---
title: Data_Management
consolidated: true
sources: 6
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_DataRules_DataRulesWhitepaperrev1docx_b06ed322.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_Data_Validation-Rev_8-030712-Cleanpdf_93c395c0.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ProratedFuelFactor_COAL_Boswell_Fuel_Factor_Updates_U4_Hourly_Dataxls_21987164.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_Item_To_Check_In_Migration_Databasesmsg_5a0c6fad.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_ServerMigration_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_0ef1e6a2.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SQL_MappingaNetworkDrivetoSQLforDatabaseBackupsdocx_8eda1cfb.md']  # This would be a timestamp
---

# Consolidated Knowledge Base Entry  
## **Title:** Data Management, Validation, and Server Migration Procedures for StackVision and Related Systems  

---

## **Overview**  
This document consolidates technical guidance on **data rules configuration**, **regulatory data validation**, **fuel factor updates**, and **server migration/database management** for StackVision and related environmental monitoring systems. It integrates operational procedures, regulatory clarifications, and best practices to ensure accurate data handling, compliance with environmental monitoring requirements, and smooth system migrations.

---

## **Key Concepts**  

### **1. Data Rules**  
- **Rule Sets**: Collections of data rules that define how parameters are evaluated.  
- **Parameter Lists**: Lists of parameters to which a Rule Set can be applied.  
- **Execution**: A Rule Set is applied to a Parameter List via a `DATARULES ProcessNow` task.  
- **Flexibility**: Rule Sets are not tied to specific parameters or intervals until execution.  

### **2. Data Validation**  
- **Regulatory Context**: Based on the Pennsylvania DEP Continuous Source Monitoring Manual, Revision No. 8.  
- **Valid Data Reading**: Defined as a valid one-minute average.  
- **Hourly Averages**: Must be calculated from valid one-minute averages per DEP guidance.  

### **3. Fuel Factor Updates**  
- **Purpose**: Adjustments to fuel factor calculations for coal and gas operations to ensure accurate emissions reporting.  
- **Data Tracking**: Includes parameters such as heat input, CO₂, NOx, Hg, SO₂, and flow rates.  

### **4. Server Migration & Database Management**  
- **Network Drive Mapping**: Required when local storage is insufficient for backups.  
- **DataLink Configuration Issue**: Incorrect or blank configuration can cause uncontrolled growth of `dbo.AverageValueLog`.  
- **SQL Integration**: Mapping network drives to SQL Server for direct backup storage.  

---

## **Technical Details**  

### **1. DataRules Operation** (Source: Document 1)  
- **Required Arguments**:  
  - `-rs` = Rule Set name  
  - `-pl` = Parameter List name  
- **Optional Argument**:  
  - `-r` = Real-time alarming  
- **SQL Tables Used**:  
  - `dbo.DataRulesRule` – Stores Rule Sets  
  - `dbo.DataRulesParameterList` – Stores Parameter Lists  
  - `dbo.AlarmNotificationConfig` – Stores alarm settings  
  - `dbo.EmailAddressList` – Stores email notification lists  
- **Editing**: Rule Sets and Parameter Lists are created in the DataRulesEditor spreadsheet and imported into SQL via SSMS.  

### **2. Data Validation Requirements** (Source: Document 2)  
- **Valid One-Minute Average**: The smallest unit of valid data for compliance purposes.  
- **Hourly Average Calculation**: Must be based solely on valid one-minute averages.  
- **DEP Discretion**: The department may deviate from these guidelines if warranted.  

### **3. Fuel Factor Update Process** (Source: Document 3)  
- **Parameters Monitored**:  
  - Unit operational status (gas/coal)  
  - Heat input (GHEATIN, HEATIN)  
  - CO₂ emissions  
  - Flow rates (SCFH)  
  - NOx, Hg, SO₂ emissions (mass and rate)  
- **Before/After Comparisons**: Used to verify accuracy of updated fuel factors.  

### **4. Server Migration Procedures** (Sources: Documents 4, 5, 6)  

#### **A. DataLink Configuration Issue**  
- **Problem**: Blank `dbo.AverageValueLogConfig` causes excessive logging.  
- **Solution**:  
  1. Open `dbo.AverageValueLogConfig` in SSMS.  
  2. If blank, set first box to `1` and second box to `6` (logs one parameter hourly).  
  3. If table is already large, run:  
     ```sql
     TRUNCATE TABLE AverageValueLog
     ```
     *(Ensure StackVision is the active database before running.)*  

#### **B. Mapping a Network Drive to SQL for Backups**  
1. **Share Target Folder** on the destination server.  
2. **Map Network Drive** on the source server (e.g., `S:`).  
3. **Enable XP_CMDSHELL** in SQL Server if not already enabled:  
   ```sql
   EXEC sp_configure 'show advanced options', 1;
   RECONFIGURE;
   EXEC sp_configure 'xp_cmdshell', 1;
   RECONFIGURE;
   ```
4. **Map Drive in SQL**:  
   ```sql
   EXEC XP_CMDSHELL 'net use S: \\RemoteServerName\ShareName /user:USERNAME PASSWORD'
   ```
5. **Verify Mapping**:  
   ```sql
   EXEC XP_CMDSHELL 'dir S:'
   ```
6. **Perform Backup** via SSMS Backup GUI to the mapped drive.  

---

## **Best Practices**  

1. **Data Rules**  
   - Keep Rule Sets modular and reusable.  
   - Maintain clear naming conventions for Rule Sets and Parameter Lists.  
   - Test rules in a non-production environment before deployment.  

2. **Data Validation**  
   - Ensure DAHS programming strictly follows DEP’s valid data definitions.  
   - Maintain audit trails for all hourly average calculations.  

3. **Fuel Factor Updates**  
   - Document all before/after parameter values for traceability.  
   - Validate changes against historical performance data.  

4. **Server Migration**  
   - Always verify `AverageValueLogConfig` settings after installing DataLink.  
   - Use mapped network drives for large backups to avoid local storage issues.  
   - Confirm SQL Server permissions before running XP_CMDSHELL commands.  

---

## **Source Attribution**  

- **Document 1 (DataRules Whitepaper)**: Provided foundational concepts, SQL table structures, and execution parameters for DataRules.  
- **Document 2 (PADEP Data Validation Clarification)**: Clarified regulatory definitions for valid data readings and hourly average calculations.  
- **Document 3 (Fuel Factor Updates)**: Supplied operational data structure and before/after comparison methodology for fuel factor adjustments.  
- **Document 4 (DataLink Configuration Issue)**: Identified and resolved excessive logging caused by blank configuration settings.  
- **Documents 5 & 6 (Mapping a Network Drive to SQL for Backups)**: Detailed step-by-step procedures for mapping network drives to SQL Server for database backups during migrations.  

---

I recommend we **integrate this into the StackVision Operations Manual** as a combined **Data Management & Migration** section, since it covers both compliance-critical data handling and infrastructure maintenance.  

Do you want me to also create a **flowchart** showing the relationship between DataRules, Data Validation, and Fuel Factor updates in the data processing pipeline? That would make this even more actionable.