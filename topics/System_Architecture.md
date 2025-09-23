---
title: System_Architecture
consolidated: true
sources: 2
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_CertificationEventspdf_34e4c2dd.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_FlowMonitorLeakCheckpdf_e0e74e0a.md']  # This would be a timestamp
---

# Continuous Emissions Monitoring System (CEMS) Certification and Flow Monitor Leak Checks

## Overview
Continuous Emissions Monitoring Systems (CEMS) are critical for ensuring compliance with environmental regulations by continuously measuring and recording emissions data from industrial sources. Proper installation, certification, and ongoing quality assurance testing are essential to maintain system accuracy and regulatory compliance.  
This consolidated entry covers two key aspects of CEMS quality assurance: **initial certification events** and **flow monitor leak checks**.

## Key Concepts

### CEMS Certification
- **Purpose**: To verify that newly installed or relocated CEMS meet regulatory performance specifications before being used for compliance reporting.
- **Types of Certification Events**:
  - **Flow Monitoring System Initial Certification (Event Code 305)**: Ensures accurate measurement of stack gas flow rates.
  - **Gas Monitoring System Initial Certification (Event Code 125)**: Confirms accuracy of pollutant concentration measurements (e.g., SO₂, NOₓ, CO₂).

### Flow Monitor Leak Check
- **Purpose**: To detect and quantify leaks in the flow monitoring system that could compromise measurement accuracy.
- **Frequency**: Typically performed as part of periodic quality assurance (QA) testing.
- **Pass/Fail Criteria**: Based on regulatory standards (e.g., U.S. EPA Part 75).

## Technical Details

### Certification Events (Example: Pine Plant)
- **Trigger**: Installation or relocation of CEMS equipment.
- **Data Recorded**:
  - **System ID**: Unique identifier for the monitoring system.
  - **Component ID**: Identifies specific hardware components.
  - **Unit/Stack ID**: Links the system to a specific emissions source.
  - **Required Test Code**: Specifies the type of certification test.
  - **Conditional Period Start**: Marks the start of the period during which the system must demonstrate compliance.
- **Example Events**:
  - **F02**: Flow monitoring system initial certification (Event 305).
  - **SL1, N02, S02, C02, SB2, NB2, CB2, SC2**: Gas monitoring system initial certifications (Event 125).

### Flow Monitor Leak Check (Example: Stoneman Plant)
- **Test Parameters**:
  - **System ID**: 107
  - **Parameter**: S1CPFLOW (flow measurement parameter)
  - **Component ID**: 008
  - **Unit ID**: CS12
- **Test Data**:
  - **Date/Hour**: Time of test execution.
  - **Status**: Pass/Fail.
  - **Test Number**: e.g., EPA007-14032.
  - **Test Reason**: QA (Quality Assurance).
  - **Grace Period?**: Indicates if testing occurred within an allowed grace period.
- **Outcome**: Pass indicates no significant leaks detected.

## Best Practices
1. **Document All Certification Events**: Maintain detailed records of system IDs, component IDs, event codes, and test results for regulatory review.
2. **Perform Leak Checks Regularly**: Schedule flow monitor leak checks according to regulatory requirements and manufacturer recommendations.
3. **Use Standardized Test Codes**: Follow EPA or relevant authority codes for consistency and compliance.
4. **Track Conditional Periods**: Ensure all required tests are completed within designated conditional periods to avoid compliance violations.
5. **Maintain Version Control**: Keep track of report versions and generation dates for audit purposes.

## Source Attribution
- **Document 1**: Provided detailed examples of CEMS certification events, including event codes, system/component IDs, and conditional period tracking for the Pine Plant.
- **Document 2**: Supplied specific flow monitor leak check procedures and data fields, including test parameters, reasons, and pass/fail status for the Stoneman Plant.

---

If you’d like, I can also create a **visual workflow diagram** showing the relationship between CEMS installation, certification events, and ongoing QA tests like leak checks. This would make the process easier to follow for both engineers and compliance officers. Would you like me to prepare that?

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_ControlCharts_Lowman_CS4_CO2_Control_Chartxls_4cd21ddb.xls](../tools/engineering_white_papers_WhitePapers_ControlCharts_Lowman_CS4_CO2_Control_Chartxls_4cd21ddb.xls)** (0.15 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

# Continuou...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
