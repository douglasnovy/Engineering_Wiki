---
title: Operational_Procedures
consolidated: true
sources: 12
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_calibrationsstandardvsdifferencexlsx_4ec97ec2.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_AECI_MatrikonHOSE_Install_Procedure_IC_rev10202017docx_35753998.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_CheatSheetEngineerxlsx_54df7a2a.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_E-DASEMRP60R3UsersGuide050306ID198pdf_639f88c3.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_E-DASEMRP75R3UsersGuide050306ID197pdf_b32b7e9a.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_Linking-Other-Software_D-Fromepdf_1f8ecde0.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_OPCQuestionsdocx_1202a612.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_ProcessNowNewHireTrainingpptx_ee6a8d3e.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_ProcessNowQuestionsdocx_902e3e5d.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_TheInsandOutsofProcessNowdocx_6c95f335.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_ProcessNowpdf_a5fd2f54.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_ProcessNowpdf_ec2b9d26.md']  # This would be a timestamp
---

## Title
**Comprehensive Guide to ProcessNow, OPC Integration, and E-DAS EMR in StackVision Systems**

---

## Overview
ProcessNow is a core data processing engine within the StackVision environmental data management platform. It automates the transformation, validation, and reporting of emissions and operational data to meet regulatory requirements such as EPA Part 60 and Part 75. This guide consolidates training materials, installation procedures, and operational best practices for ProcessNow, OPC integration using Matrikon HOSE and E-DAS API, and related tools such as E-DAS EMR. It is intended for engineers, system administrators, and compliance specialists responsible for configuring, running, and troubleshooting StackVision data workflows.

---

## Key Concepts

### ProcessNow
- **Definition**: A user-defined sequence of tasks that process raw data from controllers into validated, report-ready formats.
- **Purpose**: Streamlines data QA/QC by replacing multiple manual utilities with a single, configurable sequence.
- **Sequence Structure**: Each sequence contains tasks (e.g., missing data substitution, math calculations, rolling averages) that are dependent on one another.
- **Scheduling**: Typically runs hourly and daily; can also be triggered manually after data edits.

### OPC Integration
- **OPC Protocols**:
  - **DA (Data Access)**: Real-time data exchange, legacy COM/DCOM-based.
  - **HDA (Historical Data Access)**: Retrieval of historical datasets.
  - **UA (Unified Architecture)**: Modern, cross-platform protocol with certificate-based security.
- **Matrikon HOSE**: An OPC DA server used to host data tags for StackVision.
- **E-DAS API**: Required for Matrikon HOSE installation and integration.

### E-DAS EMR
- **Function**: Environmental Data Acquisition System for Windows, supporting regulatory data collection and reporting.
- **Regulatory Context**: Supports EPA Part 60 and Part 75 compliance.
- **User Guide Structure**: Includes definitions, conventions, and operational procedures.

---

## Technical Details

### Installing E-DAS API and Matrikon HOSE (Document 2)
1. **E-DAS API Installation**:
   - Copy `1_EDAS_API_R02S5b` from `\\groot\I&C\Matrikon OPC\Matrikon HOSE` to target machine.
   - Run setup executable; approve UAC prompts.
   - Follow wizard steps, confirming E-DAS EMR installation if applicable.
2. **Matrikon HOSE Installation**:
   - Copy executable from `\\groot\I&C\Matrikon OPC\Matrikon HOSE\2_HOSE_v2.0.0.1_011206`.
   - Run as administrator; follow wizard to completion.

### ProcessNow Operation (Documents 8, 10, 11, 12)
- **Initiation Methods**:
  1. **Scheduled**: Hourly/daily runs from the first hour of the current quarter to the current hour minus one.
  2. **Triggered by Edits**: Runs from the first changed hour after data edits.
  3. **Manual**: Initiated from DataLab, CalLab, RATA editor, or Fuel Analysis.
- **Common Tasks**:
  - **CNDMGR**: Clears Missing Data Calculated (MDC) flags to prepare for substitution.
  - **MDSUB**: Substitutes missing data per regulatory rules.
  - **ACCEPT**: Marks data as accepted for downstream processing.
  - **MATHPACK**: Performs calculations; options include:
    - `-L -c`: Recalculate logger channels without recalculating selected parameters.
    - `-O`: Only calculate specified parameters.
- **Command Line Execution**: Tasks can be run via command line with specific syntax (see ProcessNow Questions for examples).

### OPC UA vs OPC DA (Documents 6, 7)
- **OPC DA**:
  - Windows-only, COM/DCOM-based.
  - Requires Matrikon HOSE and E-DAS API.
- **OPC UA**:
  - OS-independent (Windows, Linux, iOS, Android).
  - Secure via x.509 certificates, supports TCP/IP over SSL/HTTP/HTTPS.
  - Handles both real-time and historical data.

---

## Best Practices

1. **Sequence Design**:
   - Tailor tasks to site-specific requirements (system type, permit conditions, engineering approach).
   - Include condition management early to ensure accurate substitutions.
2. **Scheduling**:
   - Maintain consistent hourly and daily runs to ensure timely QA/QC.
   - Avoid running daily sequences over periods with incomplete data to prevent erroneous calculations.
3. **OPC Integration**:
   - Use OPC UA where possible for enhanced security and cross-platform compatibility.
   - Document all tag mappings and maintain updated certificates.
4. **Troubleshooting**:
   - Enable debugging on tasks when diagnosing issues (e.g., `svmpcalcparm` with debug output to file).
   - Verify sequence storage and scheduler configurations if tasks fail to run.
5. **Regulatory Compliance**:
   - Ensure all processed data meets EPA formatting and reporting requirements.
   - Regularly review E-DAS EMR user guides for updates to procedures and definitions.

---

## Source Attribution

- **Document 1**: Placeholder for calibration standards vs difference (Excel extraction failed; no usable content).
- **Document 2**: Provided step-by-step installation procedures for E-DAS API and Matrikon HOSE.
- **Document 3**: Listed parameter limits, averaging periods, and data progression rules for engineering reference.
- **Document 4 & 5**: E-DAS EMR User Guides for EPA Part 60 and Part 75 compliance; definitions, conventions, and operational context.
- **Document 6**: Explained OPC protocols, security, and integration considerations; highlighted Matrikon HOSE and E-DAS API usage.
- **Document 7**: Posed key OPC integration questions; contrasted OPC DA and UA features.
- **Document 8**: ProcessNow New Hire Training slides; overview, configuration, and operational context.
- **Document 9**: ProcessNow troubleshooting and command line execution questions; debugging examples.
- **Document 10**: Detailed description of common ProcessNow tasks and their purposes.
- **Document 11 & 12**: Reference presentations on ProcessNow logic, initiation methods, and sequence behavior.

---

This consolidated guide should serve as a foundational reference for anyone working with ProcessNow, OPC integration, and E-DAS EMR within StackVision systems, ensuring both technical accuracy and operational efficiency.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx](../tools/engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx)** (0.02 MB)
- **[engineering_white_papers_WhitePapers_RatioEvaluation_RatioEvaluationxlsx_131ef366.xlsx](../tools/engineering_white_papers_WhitePapers_RatioEvaluation_RatioEvaluationxlsx_131ef366.xlsx)** (0.03 MB)
- **[Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_Calibration_Specifications_And_References_Rev_6-6-20-18xlsx_1bfbda8e.xlsx](../tools/Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_Calibration_Specifications_And_References_Rev_6-6-20-18xlsx_1bfbda8e.xlsx)** (0.17 MB)
- **[Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationActivityBottlesxlsx_4c681ef1.xlsx](../tools/Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationActivityBottlesxlsx_4c681ef1.xlsx)** (0.02 MB)
- **[Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_calibrationsstandardvsdifferencexlsx_4ec97ec2.xlsx](../tools/Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_calibrationsstandardvsdifferencexlsx_4ec97ec2.xlsx)** (0.03 MB)
- **[Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments-Prism_Calibration_Specifications_And_References_Rev_06-01-2023xlsx_e2aa0ce3.xlsx](../tools/Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments-Prism_Calibration_Specifications_And_References_Rev_06-01-2023xlsx_e2aa0ce3.xlsx)** (0.17 MB)
- **[Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_Calibration_Specifications_And_References_Rev_06-01-2023xlsx_3ca0a2e4.xlsx](../tools/Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_Calibration_Specifications_And_References_Rev_06-01-2023xlsx_3ca0a2e4.xlsx)** (0.17 MB)
- **[Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_Old_Calibration_Specifications_And_References_Rev_6-6-20-18xlsx_d4f71ee8.xlsx](../tools/Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_Old_Calibration_Specifications_And_References_Rev_6-6-20-18xlsx_d4f71ee8.xlsx)** (0.17 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

## Title
**...
- [[Environmental]] - ### E-DAS EMR
- **Function**: Environmental Data A...
- [[Calibration]] - ---

## Source Attribution

- **Document 1**: Plac...
