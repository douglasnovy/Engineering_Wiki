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
Continuous Emissions Monitoring Systems (CEMS) are critical for ensuring compliance with environmental regulations by continuously measuring and recording emissions data from industrial sources. Two key aspects of CEMS quality assurance are **initial certification events** and **ongoing performance checks**, such as **flow monitor leak checks**.  
This consolidated entry outlines the purpose, process, and best practices for both certification events and leak checks, ensuring accurate and reliable emissions monitoring.

## Key Concepts

### CEMS Certification Events
- **Definition:** Formal testing and documentation to verify that newly installed or relocated CEMS meet regulatory performance specifications before being used for compliance reporting.
- **Types of Certification Events:**
  - **Flow Monitoring System Initial Certification (Event Code 305):** Validates the accuracy of flow measurement devices.
  - **Gas Monitoring System Initial Certification (Event Code 125):** Confirms the accuracy of gas analyzers for pollutants such as SO₂, NOₓ, CO₂, and O₂.

### Flow Monitor Leak Check
- **Definition:** A quality assurance test performed periodically to detect leaks in the flow monitoring system that could compromise measurement accuracy.
- **Purpose:** Ensures the integrity of the flow measurement path and prevents underreporting or overreporting of emissions due to leaks.

## Technical Details

### Certification Event Process
1. **Trigger Conditions:**
   - Installation of a new CEMS.
   - Relocation of an existing CEMS.
2. **Required Tests:**
   - Flow monitoring system certification (Event 305).
   - Gas monitoring system certification (Event 125).
3. **Documentation:**
   - Record system ID, component ID, unit/stack ID.
   - Log event start and end times.
   - Maintain a certification report with version control and operator identification.
4. **Example:**
   - **Plant:** Pine Plant  
     **Report Period:** 07/01/2012 – 10/12/2012  
     Multiple gas monitoring systems (e.g., N02, S02, C02) underwent initial certification.

### Flow Monitor Leak Check Procedure
1. **Test Setup:**
   - Identify system ID, parameter, and component ID.
   - Select the unit to be tested.
2. **Execution:**
   - Perform the leak check according to EPA QA procedures.
   - Record date, hour, status, test number, and reason for test.
   - Note if a grace period applies.
3. **Pass/Fail Criteria:**
   - Pass if leak rate is within allowable limits.
   - Fail if leak rate exceeds limits, requiring corrective action.
4. **Example:**
   - **Plant:** STONEMAN  
     **Report Period:** 04/01/2013 – 05/24/2013  
     Test Number: EPA007-14032, Reason: QA, Status: Pass.

## Best Practices
- **Before Certification:**
  - Ensure all installation and calibration steps are completed.
  - Verify that all sensors and analyzers are functioning within specifications.
- **During Certification:**
  - Follow EPA and local regulatory protocols strictly.
  - Use calibrated reference gases and flow devices.
  - Document all test conditions and results.
- **For Leak Checks:**
  - Schedule leak checks at regular intervals as per QA/QC plan.
  - Investigate and repair any detected leaks immediately.
  - Maintain detailed records for regulatory review.
- **Recordkeeping:**
  - Store all certification and QA test reports with version control.
  - Ensure traceability of test results to specific system components.

## Source Attribution
- **Document 1 (Certification Events):** Provided detailed event codes, system/component/unit IDs, and example certification event records for flow and gas monitoring systems at Pine Plant.
- **Document 2 (Flow Monitor Leak Check):** Supplied procedural details, test parameters, and example leak check records for the STONEMAN plant, including test numbers, reasons, and pass/fail status.

---

If you’d like, I can extend this consolidated entry into a **step-by-step compliance checklist** that operators can use for both certification events and leak checks. This would make it more actionable for field engineers. Would you like me to prepare that?

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_ControlCharts_Lowman_CS4_CO2_Control_Chartxls_4cd21ddb.xls](../tools/engineering_white_papers_WhitePapers_ControlCharts_Lowman_CS4_CO2_Control_Chartxls_4cd21ddb.xls)** (0.15 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - md']  # This would be a timestamp
---

# Continuou...
- [[Calibration]] - ## Best Practices
- **Before Certification:**
  - ...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
