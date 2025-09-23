---
title: Data_Management
consolidated: true
sources: 19
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_2_ValidationandFlags_1M_DATA_IMPORTcsv_54727657.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_01-CEMSOverviewandRegulatoryBackgroundpdf_83299e85.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_02-CEMSFundamentalsandEquationspdf_cb4e6665.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_08-CEMSQAQCFollowingMaintenancepdf_70ef1256.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_12-HgCEMSpdf_0a33e322.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_13-PMCEMSpdf_ba784a20.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_14-CEMSDataValidityandAveragingpdf_fc8fc31d.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_15-ReportingOverviewpdf_452aeda9.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DashboardFlags2021pdf_bf1dbfc3.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DashboardObjects2021pdf_785d580b.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DatacontrollerGeneralNav2021pdf_521667cf.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DatalabDataLabViewer2021pdf_37f0b3e0.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DataReviewJobAid2021pdf_244bbcbf.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_StackStudioDataFlowpdf_1e6047d0.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_CEMS101pptx_2a03d318.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_CEMSblockdiagrampdf_cce6a5bb.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_TBS-Basics-Track-Presentation-M-Astudillopdf_187098c9.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_TBS-Dashboard_A-Lindseypdf_d6b4acb3.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_TBS-Why-is-My-Data-Invalid-M-Johnsonpdf_fd7740e5.md']  # This would be a timestamp
---

## Title
**Comprehensive Guide to Continuous Emissions Monitoring Systems (CEMS): Fundamentals, Regulatory Requirements, Data Management, and Best Practices**

---

## Overview
Continuous Emissions Monitoring Systems (CEMS) are critical for ensuring compliance with environmental regulations by continuously measuring and recording emissions from industrial stacks. They provide real-time data on pollutants such as SO₂, NOₓ, CO₂, particulate matter (PM), mercury (Hg), and opacity, enabling facilities to meet federal and state reporting requirements, optimize operations, and maintain environmental stewardship.

This guide consolidates technical fundamentals, regulatory frameworks, data acquisition and validation processes, dashboard and data visualization tools, and best practices for maintenance, QA/QC, and reporting.

---

## Key Concepts

### What is a CEMS?
- **Definition:** A system that continuously monitors emissions from a smokestack.
- **Purpose:** To provide accurate, timely data to regulatory agencies (e.g., EPA) for compliance with mandated pollutant limits.
- **Core Components:**
  - **Stack Probe:** Extracts gas sample from the stack.
  - **Analyzers:** Measure pollutant concentrations.
  - **Data Controller (e.g., ESC 8832/8864):** Aggregates, validates, and transmits data.
  - **StackVision Server:** Stores and processes data for reporting.
  - **PC/DAHS:** Runs StackVision software for data acquisition and handling.

### Pollutants and Diluents Monitored
- **Pollutants:** SO₂, NOₓ, CO, CO₂, Hg, PM, HCl.
- **Diluents:** CO₂ or O₂ (used for heat input calculations).
- **Flow:** Measured to calculate mass emissions and heat input.
- **Opacity:** Measures light blockage by particulates.

### Regulatory Framework
- **Acid Rain Program (ARP):** SO₂ and NOₓ.
- **40 CFR Part 60 (NSPS):** SO₂, NOₓ, PM, CO, Pb, O₃.
- **40 CFR Part 63 (MACT):** 187 Hazardous Air Pollutants.
- **MATS (Mercury and Air Toxics Standards):** Hg and PM CEMS requirements.

---

## Technical Details

### Sampling System Types
- **Extractive:**
  - *Dilution Extractive:* In-stack or out-of-stack dilution.
  - *Straight Extractive:* Cool-dry or hot-wet sampling.
- **In-Situ:**
  - *Cross-stack* or *point* measurement.

### Measurement Units
- **Gas Concentrations:** ppm, ppb.
- **Hg CEMS:** µg/m³ or µg/scm at standard conditions (68°F, 29.92 in Hg), hot-wet basis.
- **Flow:** scfh (standard cubic feet per hour).

### QA/QC Requirements
- **Initial Certification Tests:**
  - 7-day calibration error (drift) test.
  - Linearity checks.
  - Relative Accuracy Test Audit (RATA).
  - Cycle/Response time tests.
- **Following Maintenance:**
  - Diagnostic tests (probationary calibration error, linearity, leak check, cycle time, RATA).
  - Conditional data validity periods (e.g., 168 operating hours for linearity checks).
  - EPA R&DT policy applies to Part 75 CEMS only.

### Data Validity and Averaging
- **Raw Data:** 1-minute averages for gases/flow; 10-second for opacity.
- **Averaging Rules:**
  - 6-minute opacity averages (§60.13(h)(1)).
  - 1-hour gaseous averages (§60.13(h)(2), §75.10(d)(1)).
- **Valid Hourly Average:** ≥4 data points, one in each quadrant of the hour; special rules for maintenance/calibration periods.
- **Partial Hours:** Rules vary based on number of quadrants with operation.

### Reporting
- **Quarterly EDRs:** XML format via ECMPS for ARP, CSAPR, MATS.
- **Record Groups:** Monitoring plan, QA data, emissions data.
- **CROMERR Compliance:** Secure submission with challenge questions.

### Dashboard and Data Visualization (StackVision)
- **Objects:** Number, analog, vertical gauges; parameter tables; text boxes.
- **Flags:** Warning, alert, out-of-control, maintenance, calibration.
- **DataLab:** Filtering, summaries, flag color display.
- **ProcessNow:** Automated background tasks for data processing.

---

## Best Practices

1. **Maintain Continuous Operation:**
   - Ensure CEMS operates 24/7 with minimal downtime.
   - Monitor calibration status daily.

2. **Follow QA/QC Protocols:**
   - Perform required certification and diagnostic tests.
   - Document all maintenance and test results.

3. **Validate Data Rigorously:**
   - Apply EPA-defined validation rules before reporting.
   - Investigate and resolve invalid data flags promptly.

4. **Optimize Dashboard Use:**
   - Configure flags and gauges for quick identification of issues.
   - Use parameter tables for grouped data monitoring.

5. **Leverage DataLab Tools:**
   - Apply filters and summaries to detect trends and anomalies.
   - Maintain clear records of data edits and validations.

6. **Ensure Accurate Reporting:**
   - Use ECMPS software for EDR preparation and submission.
   - Maintain CROMERR compliance for secure data transfer.

7. **Training and Documentation:**
   - Train staff on CEMS fundamentals, regulatory requirements, and StackVision tools.
   - Keep configuration and operational documentation up to date.

---

## Source Attribution

- **[Document 1]:** Provided example raw data import format for NOx measurements with flags.
- **[Document 2]:** Outlined CEMS regulatory background and pollutant coverage.
- **[Document 3]:** Detailed CEMS fundamentals, sampling types, and gas measurement principles.
- **[Document 4]:** Specified QA/QC requirements following maintenance, diagnostic test limits, and EPA policy applicability.
- **[Document 5]:** Explained Hg CEMS measurement techniques, units, equipment, and calibration options.
- **[Document 6]:** Provided PM CEMS background, certification procedures, and correlation testing requirements.
- **[Document 7]:** Defined data validity rules, averaging periods, and conditions for valid hourly averages.
- **[Document 8]:** Described quarterly reporting structure, ECMPS usage, and CROMERR compliance.
- **[Document 9]:** Explained dashboard flag configuration in StackVision.
- **[Document 10]:** Described dashboard object types and customization options.
- **[Document 11]:** Covered general navigation of ESC data controllers via GUI and browser.
- **[Document 12]:** Detailed DataLab and DataLab Viewer functions for filtering and summarizing data.
- **[Document 13]:** Provided daily CEMS data review procedures, calibration checks, and ProcessNow monitoring.
- **[Document 14]:** Outlined StackStudio configuration data flow from controllers to parameters and channels.
- **[Document 15]:** Introduced CEMS basics, components, and analyzer types.
- **[Document 16]:** Illustrated CEMS block diagram linking components and data flow.
- **[Document 17]:** Summarized CEMS operational requirements and initial certification testing.
- **[Document 18]:** Presented dashboard redesign principles for improved usability.
- **[Document 19]:** Explained causes of invalid data and procedures for investigation and resolution.

---

This consolidated guide serves as a comprehensive reference for CEMS operators, technicians, and compliance managers, integrating regulatory knowledge, technical operation, data management, and visualization best practices.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls](../tools/engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls)** (0.08 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

## Title
**...
- [[Environmental]] - They provide real-time data on pollutants such as ...
- [[Calibration]] - ### QA/QC Requirements
- **Initial Certification T...
- [[Calibration]] - - **Following Maintenance:**
  - Diagnostic tests ...
- [[Calibration]] - - **Flags:** Warning, alert, out-of-control, maint...
- [[Calibration]] - - Monitor calibration status daily...
- [[Calibration]] - - **[Document 5]:** Explained Hg CEMS measurement ...
- [[Calibration]] - - **[Document 13]:** Provided daily CEMS data revi...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
