---
title: Operational_Procedures
consolidated: true
sources: 12
conflicts: 1
confidence: 0.70
generated: ['data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_calibrationsstandardvsdifferencexlsx_4ec97ec2.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_AECI_MatrikonHOSE_Install_Procedure_IC_rev10202017docx_35753998.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_CheatSheetEngineerxlsx_54df7a2a.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_E-DASEMRP60R3UsersGuide050306ID198pdf_639f88c3.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_E-DASEMRP75R3UsersGuide050306ID197pdf_b32b7e9a.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_Linking-Other-Software_D-Fromepdf_1f8ecde0.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_OPCQuestionsdocx_1202a612.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_ProcessNowNewHireTrainingpptx_ee6a8d3e.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_ProcessNowQuestionsdocx_902e3e5d.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_TheInsandOutsofProcessNowdocx_6c95f335.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_ProcessNowpdf_a5fd2f54.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_ProcessNowpdf_ec2b9d26.md']  # This would be a timestamp
---

### Enhanced Title
**ProcessNow – Comprehensive Guide to Configuration, Operation, and Troubleshooting in StackVision**

---

### Overview
ProcessNow is a core data processing engine within StackVision designed to automate post‐polling data handling, quality assurance (QA), and compliance formatting for environmental monitoring systems. Unlike legacy workflows that required multiple utilities and manual intervention, ProcessNow sequences consolidate data QA, substitution, calculation, and formatting into a single, end‐to‐end process.  

Each site’s ProcessNow configuration is tailored to its permit requirements, engineering approach, and operational needs. Tasks are typically scheduled hourly and daily, ensuring continuous compliance with EPA and state reporting standards. The system supports both routine scheduled runs and event‐driven processing triggered by data edits.

---

### Key Concepts

#### ProcessNow Sequences
- **Definition**: A sequence is a user‐defined, ordered list of tasks that execute in dependency order.
- **Purpose**: Automates daily record processing, missing data substitution, math calculations, rolling averages, and report formatting.
- **Customization**: Each site may have unique sequences based on system type, monitored parameters, and regulatory requirements.

#### Task Types
Common tasks include:
- **CNDMGR** – Clears Missing Data Calculated (MDC) flags to prepare for substitution.
- **MDSUB** – Substitutes missing data according to permit rules.
- **ACCEPT** – Marks data as accepted, enabling downstream reporting tasks.
- **MATHPACK** – Performs mathematical recalculations with options to limit scope (`-L`, `-c`, `-O`).
- **PDR/UDR** – Generates preliminary and updated data reports.
- **Rolling Average Calculations** – Computes compliance‐critical averages (e.g., 3‐hour NOx).

#### Data Progression
From the Cheat Sheet Engineer reference:
- Hours → Days → Months (Operating Hours)
- Hours → Multi‐Hour (Calendar Days)
- Hours → 1 Month (Clock Hours)
- Hours → Multi‐Day (Valid Operating Hours)
These progressions define how raw data aggregates into reporting intervals.

---

### Technical Details

#### Initiating ProcessNow
ProcessNow can be initiated in three ways:
1. **Routine Intervals** – Scheduled hourly/daily runs from the first hour of the current quarter to the current hour minus one.
2. **Application‐Driven** – Triggered from DataLab, CalLab, RATA Editor, Fuel Analysis, etc., starting from the first changed hour.
3. **Manual Command Line** – Using task‐specific syntax (e.g., `svmpcalcparm UNIT1:NOXPPM -debug > debug.txt`).

#### Configuring Sequences
- Use the **ProcessNow Editor** in StackStudio.
- Define tasks, parameters, intervals, and execution order.
- Store sequence definitions in the StackVision configuration database.

#### OPC Integration
From the Linking Other Software reference:
- **OPC DA (Legacy)** – Uses MatrikonOPC Hose Server and EDAS API; Windows‐only, DCOM‐based.
- **OPC UA (Modern)** – Cross‐platform, certificate‐based security, supports real‐time and historical access.
- Integration allows importing data from external historians (e.g., OSIsoft PI) into StackVision for processing.

#### Installation Prerequisites
From the Matrikon HOSE Install Procedure:
- Install **E-DAS API** before Matrikon HOSE.
- Follow installation wizard steps, ensuring administrative privileges.
- Confirm E-DAS EMR presence before proceeding.

---

### Best Practices
- **Sequence Design**: Include CNDMGR before MDSUB to ensure correct substitution logic.
- **Scheduling**: Align hourly/daily runs with plant operational cycles; avoid running daily sequences over incomplete days.
- **Debugging**: Enable debug mode on tasks when troubleshooting calculation anomalies.
- **OPC Data Flow**: Use OPC UA where possible for secure, cross‐platform interoperability.
- **Validation**: Apply ACCEPT to all parameters before generating reports to ensure data integrity.

---

### Implementation Examples

#### Example: Full CEMS – NON‐MATS Sequence
1. **CNDMGR** – Clear MDC flags.
2. **MDSUB** – Substitute missing data.
3. **ACCEPT** – Mark all parameters accepted.
4. **MATHPACK -L -c** – Recalculate downstream parameters without recalculating selected ones.
5. **Rolling Average Task** – Compute compliance averages.
6. **PDR/UDR** – Generate reports.

#### Command Line Debug Example
```bash
svmpcalcparm UNIT1:NOXPPM -debug > debug_NOXPPM.txt
```
This recalculates NOXPPM with debug output written to a file.

---

### Troubleshooting

#### Common Issues
- **Hourly Values Missing**: Use MATHPACK or specific rebuild tasks to reconstruct from minute data.
- **Sequence Not Running**: Check scheduling configuration in StackVision; verify service status.
- **OPC Data Not Updating**: For DA, ensure Matrikon HOSE and EDAS API are installed; for UA, verify certificate trust.
- **Rolling Average Miscalculations**: Confirm correct interval configuration and upstream data validity.

#### Debugging Steps
1. Enable task debug mode.
2. Review logs for MDC/MIS/INV flags.
3. Verify data progression settings match permit requirements.
4. Check OPC connectivity and security settings.

---

### Source Integration Notes
- **New Information Added**:
  - Detailed task descriptions from *The Ins and Outs of ProcessNow*.
  - Data progression mappings from *Cheat Sheet Engineer.xlsx*.
  - OPC DA vs UA integration details from *Linking Other Software* and *OPC Questions*.
  - Installation prerequisites from *Matrikon HOSE Install Procedure*.
  - Command line syntax and troubleshooting from *ProcessNow Questions.docx*.
- **Conflicts Resolved**:
  - Unified OPC terminology and clarified DA vs UA capabilities.
  - Standardized task order recommendations across examples.
- **Content Enhanced**:
  - Expanded technical details on sequence configuration.
  - Added best practices for scheduling and debugging.
  - Included real‐world sequence example for Full CEMS systems.

---

If you’d like, I can also create **a visual flow diagram of a typical ProcessNow sequence** integrating OPC data ingestion, QA tasks, and reporting, which would make this guide even more actionable. Would you like me to add that?