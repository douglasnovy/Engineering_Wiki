---
title: Operational_Procedures
consolidated: true
sources: 12
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_calibrationsstandardvsdifferencexlsx_4ec97ec2.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_AECI_MatrikonHOSE_Install_Procedure_IC_rev10202017docx_35753998.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_CheatSheetEngineerxlsx_54df7a2a.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_E-DASEMRP60R3UsersGuide050306ID198pdf_639f88c3.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_E-DASEMRP75R3UsersGuide050306ID197pdf_b32b7e9a.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_Linking-Other-Software_D-Fromepdf_1f8ecde0.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_OPCQuestionsdocx_1202a612.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_ProcessNowNewHireTrainingpptx_ee6a8d3e.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_ProcessNowQuestionsdocx_902e3e5d.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_7_Processnow_TheInsandOutsofProcessNowdocx_6c95f335.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_ProcessNowpdf_a5fd2f54.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_ProcessNowpdf_ec2b9d26.md']  # This would be a timestamp
---

## Title
**Comprehensive Guide to ProcessNow, OPC Integration, and E-DAS EMR in StackVision Systems**

---

## Overview
ProcessNow is a core data processing and quality assurance (QA) automation tool within the StackVision environmental data management platform. It streamlines the transformation of raw data from Continuous Emissions Monitoring Systems (CEMS) into validated, compliant records for regulatory reporting. This guide consolidates training materials, installation procedures, operational notes, and best practices for using ProcessNow in conjunction with OPC data interfaces (Matrikon HOSE, E-DAS API) and E-DAS EMR software.

The document covers:
- ProcessNow logic, configuration, and task sequencing
- OPC DA and OPC UA integration for external data sources
- Installation of Matrikon HOSE and E-DAS API
- E-DAS EMR usage fundamentals
- Best practices for calibration, data progression, and troubleshooting

---

## Key Concepts

### ProcessNow
- **Purpose**: Automates post-processing of polled data, ensuring it meets EPA/state reporting requirements.
- **Sequences**: User-defined lists of dependent tasks (e.g., daily record processing, missing data substitution, math calculations, rolling averages).
- **Scheduling**: Typically runs hourly and daily; can be triggered manually or via other StackVision modules (DataLab, CalLab, RATA editor, Fuel Analysis).
- **Compliance**: Ensures data is correctly formatted for Electronic Data Reports (EDR) and other permit reports.

### OPC Integration
- **OPC DA (Legacy)**: Uses DCOM/COM, Windows-only, more complex configuration.
- **OPC UA (Unified Architecture)**: OS-independent, certificate-based security, supports real-time and historical data access.
- **Matrikon HOSE**: OPC DA server used with E-DAS API to host and map data tags from external systems (e.g., OSIsoft PI historian).

### E-DAS EMR
- **Function**: Environmental Data Acquisition System for Windows; manages data collection, storage, and preliminary processing.
- **Release R3**: Includes user guides for Part 60 and Part 75 compliance contexts.
- **Integration**: Works with Matrikon HOSE and ProcessNow for end-to-end data handling.

### Data Progression & Parameters
- **Progression Types**: Hours → Days, Hours → Multi-Hour, Hours → Months, etc.
- **Validation & Conditions**: Parameters have limits, averaging periods, and online conditions; startup periods may be excluded.
- **Final Parameters**: Calculated values used in compliance reporting.

---

## Technical Details

### Installing E-DAS API (Prerequisite for Matrikon HOSE)
1. Copy `1_EDAS_API_R02S5b` from `\\groot\I&C\Matrikon OPC\Matrikon HOSE` to target machine.
2. Run `setup.exe` as administrator.
3. Accept prompts (User Account Control, installation wizard).
4. Confirm E-DAS EMR is installed if prompted.
5. Complete installation (Next → Finish).

### Installing Matrikon HOSE
1. Copy executable from `\\groot\I&C\Matrikon OPC\Matrikon HOSE\2_HOSE_v2.0.0.1_011206`.
2. Run as administrator.
3. Follow installation wizard, accept license, and finish setup.

### ProcessNow Task Examples
- **CNDMGR**: Clears Missing Data Calculated (MDC) flags before substitution.
- **MDSUB**: Substitutes missing data based on rules and MDC status.
- **ACCEPT**: Marks data as accepted for downstream processing.
- **MATHPACK**: Performs math calculations with options:
  - `-L -c`: Recalculate logger channels, skip selected parameters, calculate downstream.
  - `-O`: Only calculate specified parameters.

### OPC Data Flow
- **Getting Data Out**: Requires running condition manager to clear MIS/INV flags.
- **Getting Data In**: Monthly data may be browsable but not auto-updated in some OPC DA setups.
- **Security**: OPC UA supports TCP/IP over SSL, HTTP/HTTPS with x.509 certificates.

---

## Best Practices

1. **Sequence Design**: Tailor ProcessNow sequences to site-specific systems, permits, and operational needs.
2. **Scheduling**: Ensure hourly and daily runs are configured and monitored; troubleshoot missed runs by checking stored schedules.
3. **Debugging**: Enable debug mode on tasks when diagnosing issues (e.g., `svmpcalcparm UNIT1:NOXPPM -debug > debugfile.txt`).
4. **Data Recovery**: Use appropriate tasks to rebuild hourly values from minute data when needed.
5. **OPC Configuration**: Prefer OPC UA for new integrations due to enhanced security and cross-platform support.
6. **Installation Order**: Install E-DAS API before Matrikon HOSE to ensure proper OPC DA functionality.
7. **Calibration Management**: Maintain clear distinction between standard and difference calibration methods (requires review of Document 1 once available).
8. **Security Certificates**: Manage OPC UA certificates carefully to maintain secure client-server communication.

---

## Source Attribution

- **Document 1**: Placeholder for calibration standard vs. difference methodology (Excel extraction failed; requires manual review).
- **Document 2**: Detailed installation steps for E-DAS API and Matrikon HOSE.
- **Document 3**: Parameter definitions, limits, data progression types, and validation rules.
- **Document 4 & 5**: E-DAS EMR User’s Guides for Part 60 and Part 75 compliance contexts.
- **Document 6**: OPC UA vs. OPC DA comparison, security considerations, and integration notes.
- **Document 7**: OPC-related customer Q&A, setup requirements for PI-to-StackVision data push.
- **Document 8**: ProcessNow overview, objectives, and operational context from new hire training.
- **Document 9**: ProcessNow troubleshooting and command-line usage examples.
- **Document 10**: Detailed description of common ProcessNow tasks and their purposes.
- **Document 11 & 12**: ProcessNow logic, sequence behavior, and initiation methods from reference documents/presentations.

---

This consolidated guide provides a unified reference for technical staff working with StackVision’s ProcessNow, OPC integration, and E-DAS EMR systems, ensuring consistent understanding and application across installations and operational contexts.

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
- [[Calibration]] - **Calibration Management**: Maintain clear distinc...
- [[Calibration]] - ---

## Source Attribution

- **Document 1**: Plac...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
