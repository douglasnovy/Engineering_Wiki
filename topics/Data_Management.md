---
title: Data_Management
consolidated: true
sources: 19
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_2_ValidationandFlags_1M_DATA_IMPORTcsv_54727657.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_01-CEMSOverviewandRegulatoryBackgroundpdf_83299e85.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_02-CEMSFundamentalsandEquationspdf_cb4e6665.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_08-CEMSQAQCFollowingMaintenancepdf_70ef1256.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_12-HgCEMSpdf_0a33e322.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_13-PMCEMSpdf_ba784a20.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_14-CEMSDataValidityandAveragingpdf_fc8fc31d.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_9_Regulations_15-ReportingOverviewpdf_452aeda9.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DashboardFlags2021pdf_bf1dbfc3.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DashboardObjects2021pdf_785d580b.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DatacontrollerGeneralNav2021pdf_521667cf.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DatalabDataLabViewer2021pdf_37f0b3e0.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_A_JobAids_DataReviewJobAid2021pdf_244bbcbf.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferenceDocuments_StackStudioDataFlowpdf_1e6047d0.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_CEMS101pptx_2a03d318.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_CEMSblockdiagrampdf_cce6a5bb.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_TBS-Basics-Track-Presentation-M-Astudillopdf_187098c9.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_TBS-Dashboard_A-Lindseypdf_d6b4acb3.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_ReferencePresentations_TBS-Why-is-My-Data-Invalid-M-Johnsonpdf_fd7740e5.md']  # This would be a timestamp
---

## Title
Comprehensive Guide to Continuous Emissions Monitoring Systems (CEMS): Fundamentals, Regulatory Requirements, Data Management, and Best Practices

---

## Overview
Continuous Emissions Monitoring Systems (CEMS) are critical for ensuring compliance with environmental regulations by continuously measuring and recording emissions from industrial stacks. They provide real-time data on pollutants such as SO₂, NOₓ, CO₂, particulate matter (PM), mercury (Hg), and opacity, enabling facilities to meet federal and state regulatory requirements, optimize operations, and maintain environmental stewardship. This guide consolidates technical fundamentals, regulatory frameworks, data validity rules, QA/QC procedures, and operational best practices for CEMS, integrating both regulatory training materials and practical job aids.

---

## Key Concepts

### What is a CEMS?
A CEMS is a system designed to:
- Continuously monitor stack emissions.
- Provide data to regulatory agencies (e.g., EPA) for compliance verification.
- Measure pollutants and diluents to calculate mass emissions and heat input.
- Operate 24/7, sampling, analyzing, and recording data at least every 15 minutes, building hourly averages for reporting.

### Core Components
- **Stack Probe**: Extracts sample gas from the stack.
- **Analyzers**: Measure pollutant concentrations (SO₂, NOₓ, CO₂, O₂, CO, Hg, PM).
- **Flow Monitors**: Measure volumetric stack flow for mass emissions and heat input calculations.
- **Data Controller (e.g., ESC 8864)**: Averages and records data, applies validation rules.
- **Data Acquisition System (DAS)**: StackVision server and client software for storage, processing, and reporting.

### Regulatory Framework
Three primary federal regulations govern CEMS:
1. **Acid Rain Program (ARP)** – 40 CFR Part 75: SO₂ and NOₓ.
2. **New Source Performance Standards (NSPS)** – 40 CFR Part 60: SO₂, NOₓ, PM, CO, Pb, O₃.
3. **Maximum Achievable Control Technology (MACT)** – 40 CFR Part 63: Hazardous Air Pollutants (HAPs), including Hg and PM.

---

## Technical Details

### Measurement Principles
- **Gas Concentrations**: Expressed in ppm or ppb; measured on a wet or dry basis depending on system type.
- **Sampling Methods**:
  - **Extractive**: Cool-dry or hot-wet; requires heated umbilicals and moisture removal.
  - **Dilution Extractive**: In-stack or out-of-stack dilution to prevent condensation.
  - **In-Situ**: Cross-stack or point measurement directly in the stack.

### Specialized CEMS
- **Hg CEMS**: Use atomic absorption or fluorescence; measure in µg/m³ at standard conditions; require specific calibration methods.
- **PM CEMS**: Typically use light scattering or beta attenuation; require site-specific correlation to reference methods; certified under Performance Specification 11.

### Data Validity & Averaging
- **Raw Data**: 1-minute averages for gases/flow; 10-second for opacity.
- **Valid Hourly Average**: Requires data points in each quadrant of the hour; special rules apply during maintenance/calibration.
- **Partial Hours**: Validity rules depend on number of quadrants with operation and timing of calibrations.

### QA/QC Procedures
- **Routine QA Tests**: Calibration error, linearity checks, RATA, cycle/response time.
- **Following Maintenance**: Diagnostic tests with probationary data validity periods (e.g., 168 hours for linearity checks).
- **Certification**: Initial 7-day drift, correlation tests, and response time verification.

### Reporting
- **Quarterly EDRs**: XML format submitted via ECMPS; include monitoring plan, QA data, emissions data.
- **CROMERR Compliance**: Secure account setup, challenge questions, and secure submission protocols.

---

## Best Practices

1. **System Configuration**
   - Use reference configurations and default values when uncertain; consult mentors or customers.
   - Ensure all parameters have correct units of measure, calibration dates, and equations.

2. **Data Review**
   - Perform daily calibration status checks.
   - Use StackVision tools (CalLab, DataLab) to identify invalid or missing data.
   - Investigate flags (e.g., Calibration, Out-of-Control) promptly.

3. **Dashboard Management**
   - Configure gauges and tables with clear flag colors for warnings/alerts.
   - Prioritize high-importance parameters with visible gauges.
   - Group parameters logically for ease of monitoring.

4. **QA/QC Compliance**
   - Follow EPA diagnostic test timelines strictly after maintenance.
   - Maintain documentation of all QA/QC activities for audits.

5. **Reporting Accuracy**
   - Validate data before submission to avoid penalties from substituted data.
   - Ensure ECMPS software is up-to-date and staff are trained in its use.

---

## Source Attribution

- **Document 1**: Provided example raw CEMS data with flags, illustrating minute-by-minute pollutant measurements and flagging conventions.
- **Document 2**: Outlined CEMS regulatory background, pollutant coverage, and training agenda.
- **Document 3**: Detailed CEMS fundamentals, gas measurement principles, and sampling system types.
- **Document 4**: Specified QA/QC requirements following maintenance, diagnostic test procedures, and data validity rules.
- **Document 5**: Explained Hg CEMS measurement techniques, equipment configurations, and calibration methods.
- **Document 6**: Covered PM CEMS background, certification requirements, and correlation testing.
- **Document 7**: Defined data validity and averaging rules for compliance reporting.
- **Document 8**: Summarized quarterly reporting processes, ECMPS usage, and CROMERR compliance.
- **Document 9**: Provided guidance on setting dashboard flags in StackVision for visual alerts.
- **Document 10**: Described dashboard object types and customization options.
- **Document 11**: Explained data controller navigation via GUI and browser access.
- **Document 12**: Outlined DataLab and DataLab Viewer functions for filtering and summarizing data.
- **Document 13**: Offered daily CEMS data review procedures and ProcessNow monitoring.
- **Document 14**: Provided StackStudio configuration workflow for data controllers.
- **Document 15**: Introduced CEMS basics, components, and analyzer types.
- **Document 16**: Illustrated CEMS block diagram showing data flow.
- **Document 17**: Presented CEMS overview, pollutant measurement, and certification testing requirements.
- **Document 18**: Explained dashboard redesign principles for improved usability.
- **Document 19**: Clarified causes of invalid data and methods for investigation and resolution.

---

This consolidated guide integrates regulatory, technical, and operational perspectives to provide a complete reference for CEMS professionals, ensuring both compliance and optimal system performance.

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls](../tools/engineering_white_papers_WhitePapers_SampleTests_NOXCorr_2004xls_1a0b87f6.xls)** (0.08 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

## Title
Co...
- [[Environmental]] - They provide real-time data on pollutants such as ...
- [[Calibration]] - ### Specialized CEMS
- **Hg CEMS**: Use atomic abs...
- [[Calibration]] - ### QA/QC Procedures
- **Routine QA Tests**: Calib...
- [[Calibration]] - - Ensure all parameters have correct units of meas...
- [[Calibration]] - **Data Review**
   - Perform daily calibration sta...
- [[Calibration]] - - **Document 5**: Explained Hg CEMS measurement te...


## Glossary

- **ECMPS**: Emissions Collection and Monitoring Plan System
- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
