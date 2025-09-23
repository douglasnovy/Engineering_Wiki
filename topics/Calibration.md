---
title: Calibration
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_OptimePrecision20050211JLBpdf_2c025a7f.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CalibrationCorrection_EngineeringStandard-CalibrationCorrection-Rev11-01-2021pdf_605a61ca.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPTermsandNotesdocx_cf04b587.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_7-DayCalibrationErrorTestpdf_f17bcd7c.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_StackVision_CHKOOC60Validationdocx_a7cc510e.md']  # This would be a timestamp
---

## Title
**Calibration Precision, Correction, and Out-of-Control (OOC) Management in Continuous Emissions Monitoring Systems (CEMS)**

---

## Overview
Calibration precision and correction are critical components in ensuring the accuracy and regulatory compliance of Continuous Emissions Monitoring Systems (CEMS) under U.S. EPA Part 60 and Part 75 regulations, as well as state-specific requirements such as PADEP Rev 8. Proper calculation of operating precision, implementation of calibration correction algorithms, and management of Out-of-Control (OOC) conditions are essential for maintaining data integrity, passing certification tests, and avoiding regulatory penalties.

This consolidated guide integrates calculation methodologies, calibration correction standards, regulatory testing requirements, and OOC validation procedures into a single reference for engineers and compliance specialists.

---

## Key Concepts

1. **Calibration Precision**  
   - Precision refers to the repeatability of analyzer readings during calibration checks.  
   - Calculations differ depending on whether precision values are above or below 60 units (minutes or equivalent measurement units).

2. **Calibration Correction**  
   - Automatic adjustment of analyzer readings based on daily zero and span calibration results.  
   - Involves calculating both zero offset and gain to correct measurement drift.

3. **Regulatory Testing Requirements**  
   - **7-Day Calibration Error Test**: Verifies analyzer accuracy over a seven-day period.  
   - **PADEP Certification Tests**: Includes drift tests, DAHS verification, and QA/QC plan adherence.

4. **Out-of-Control (OOC) Conditions**  
   - Defined periods when calibration results exceed regulatory limits.  
   - Requires identification, flagging, and corrective action before data can be considered valid.

---

## Technical Details

### 1. Precision Calculation (Document 1)
**Formula for Operating Precision Time (OP_TIME_PPREC):**
```c
if (calcprecision > 60) {
    calcdoptime = (int)((((3600.0/(calcprecision * 60.0) - 1 + (calcminutes * 60.0)) / 3600.0) * (calcprecision * 60.0)) + 0.001) / (calcprecision * 60.0);
} else {
    calcdoptime = (int)((((60.0/calcprecision - 1 + calcminutes) / 60.0) * calcprecision) + 0.001) / calcprecision;
}
```
- **Above 60**: Uses seconds-based calculation.  
- **60 or below**: Uses minutes-based calculation.

---

### 2. Calibration Correction Configuration (Document 2)
- **Inputs Required**:
  - Expected Span (default: 1)
  - Expected Zero (default: 0)
  - Span Result (default: 1)
  - Zero Result (default: 0)
- **Procedure**:
  - Write constants at the end of calibration phase (`Write Constants at End of Phase` = NO).
  - Calculate zero offset and gain based on differences between expected and actual results.
  - Include pseudo digital I/O to disable gain/offset when required.
  - Record all adjustments for compliance documentation.

---

### 3. PADEP Regulatory Requirements (Document 3)
- **Certification Tests**:
  - 7-Day Drift
  - DAHS Accuracy Verification
  - QA/QC Plan adherence
- **LMESE Calculation**:
  - Default = Full Scale (FS) ÷ 2
  - CE = |R – A| / LMESE × 100
- **Opacity Requirements**:
  - 60 one-minute averages and 10-second averages per hour.

---

### 4. 7-Day Calibration Error Test (Document 4)
- **Purpose**: Validate analyzer performance over seven consecutive days.
- **Data Recorded**:
  - Zero-Level and Span-Level values
  - Reference vs. Actual readings
  - Percent calibration error
- **Pass/Fail Criteria**: Based on regulatory limits for each parameter.

---

### 5. CHKOOC60 OOC Validation (Document 5)
- **Function**: Determines validity for Part 60 parameters during calibration drift.
- **Key Switches**:
  - `-n`: No database update
  - `-r`: No OOC flag propagation
  - `-o`: Disable cascading
  - `-m`: Overwrite method code
- **OOC Period Definitions**:
  - Start: End of previous good calibration or after consecutive limit exceedances.
  - End: Next good calibration, within regulatory time limits.
- **Dual Range Analyzer Handling**:
  - Marks merge channel parameter as OOC when either low or high range is OOC.

---

## Best Practices

1. **Precision Monitoring**  
   - Use appropriate formula based on precision threshold (>60 or ≤60).  
   - Regularly review precision calculations to detect anomalies early.

2. **Calibration Correction Implementation**  
   - Maintain accurate expected and actual calibration constants.  
   - Ensure correction can be reset or disabled as needed.  
   - Log all adjustments for audit purposes.

3. **Regulatory Compliance Testing**  
   - Schedule and document all required certification and drift tests.  
   - Use LMESE and CE formulas consistently for error evaluation.

4. **OOC Management**  
   - Configure CHKOOC60 parameters correctly to avoid missed OOC flags.  
   - Understand OOC start/end definitions to ensure timely corrective action.  
   - Avoid altering data during non-operating hours.

5. **Documentation and Traceability**  
   - Keep detailed records of calibration results, corrections applied, and OOC events.  
   - Ensure DAHS and EDR samples are properly certified and archived.

---

## Source Attribution

- **Document 1 (Optime Precision)**: Provided formulas and logic for calculating operating precision time based on precision thresholds.  
- **Document 2 (Calibration Correction Standard)**: Detailed configuration steps, constants, and procedural requirements for implementing calibration correction in compliance with Part 60/75.  
- **Document 3 (PADEP Terms and Notes)**: Defined regulatory testing requirements, LMESE and CE calculations, and certification phases under PADEP Rev 8.  
- **Document 4 (7-Day Calibration Error Test)**: Supplied example test data structure, pass/fail criteria, and reporting format for calibration error testing.  
- **Document 5 (CHKOOC60 Validation)**: Explained OOC detection logic, tool configuration, and regulatory definitions for OOC periods under Part 60.

---

If you’d like, I can create a **visual workflow diagram** showing how precision calculation, calibration correction, and OOC validation fit together in a CEMS compliance cycle. Would you like me to add that?

## Glossary

- **CEMS**: Continuous Emissions Monitoring System
