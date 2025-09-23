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
Accurate calibration and precision management are critical for Continuous Emissions Monitoring Systems (CEMS) compliance under regulatory frameworks such as **40 CFR Part 60** and **Part 75**, as well as state-specific requirements like **PADEP Rev 8**. This consolidated guide integrates procedures for calculating operational precision, implementing calibration correction, conducting certification and drift tests, and managing Out-of-Control (OOC) conditions. Proper application ensures data integrity, regulatory compliance, and optimal system performance.

---

## Key Concepts

1. **Calibration Precision**  
   Precision refers to the repeatability of analyzer measurements over time. It is calculated differently depending on whether the precision value exceeds 60 or not, influencing operational time calculations.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span reference values versus actual results, ensuring compliance with regulatory drift limits.

3. **Certification and Drift Testing**  
   Certification tests (e.g., 7-Day Drift Test) verify analyzer accuracy and DAHS (Data Acquisition and Handling System) performance. Drift limits are defined by regulatory bodies and must be adhered to.

4. **Out-of-Control (OOC) Conditions**  
   OOC conditions occur when calibration results exceed regulatory limits for consecutive tests. Tools like **CHKOOC60** automate detection and flagging of OOC periods.

5. **Regulatory Frameworks**  
   - **40 CFR Part 60 & Part 75**: Federal requirements for calibration, drift limits, and OOC handling.  
   - **PADEP Rev 8**: State-specific definitions, limits, and certification phases.

---

## Technical Details

### 1. Precision Calculation (Document 1)
Two formulas are used depending on the precision threshold:

- **For precision > 60**:
```c
calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
```

- **For precision ≤ 60**:
```c
calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
```

These calculations determine operational minutes based on precision and elapsed time.

---

### 2. Calibration Correction Implementation (Document 2)
- **Inputs**:
  - Expected Span (default 1)
  - Expected Zero (default 0)
  - Span Result (default 1)
  - Zero Result (default 0)
- **Procedure**:
  - Calculate zero offset and gain from daily calibration results.
  - Ensure *Write Constants at End of Phase* is set to **NO** to evaluate corrections over the full sequence.
  - Include functionality to:
    - Reset corrections until next calibration
    - Disable corrections
    - Trigger alarms when adjustments exceed agreed thresholds
- **Control**:
  - Use pseudo digital I/O to disable gain/offset adjustments when needed.

---

### 3. Certification & Drift Testing (Documents 3 & 4)
- **PADEP Rev 8 Requirements**:
  - **7-Day Drift Test**: Measures deviation from calibration reference values over seven consecutive days.
  - **LMESE**: Lowest Monitored Emissions Standard Equivalent, used in drift calculations:
    ```
    CE = |R – A| / LMESE * 100
    ```
    Where R = Reference, A = Actual.
  - Default LMESE = FS / 2 (Full Scale divided by 2), except for certain parameters (Opacity, CO₂, O₂, VFR, some dual range).
- **Certification Phases**:
  - Phase I: Implementation & MP approval
  - Phase II: Testing (within 210 days of startup or 60 days of achieving normal capacity)
  - Phase III: Certification for DAHS and EDR samples

---

### 4. Out-of-Control (OOC) Management (Document 5)
**CHKOOC60 Tool**:
- Validates Part 60 parameters during calibration drift.
- Flags OOC periods based on:
  - Maintenance limit exceedances
  - Consecutive calibration failures
  - Defined time-based rules (e.g., 24 hours after previous calibration)
- **OOC Period Definitions**:
  - Start: End of previous good calibration
  - End: End of subsequent good calibration (limits apply)
- **Dual Range Analyzer Handling**:
  - Marks target merge channel parameter OOC when either low or high range is OOC.

---

## Best Practices

1. **Precision Management**  
   - Use correct formula based on precision threshold.
   - Regularly verify calculation logic in software implementations.

2. **Calibration Correction**  
   - Maintain accurate expected and result constants.
   - Implement alarms for excessive corrections.
   - Document all adjustments for compliance audits.

3. **Drift Testing**  
   - Schedule and document 7-Day Drift Tests.
   - Use LMESE values correctly for each parameter type.
   - Ensure DAHS verification includes all operating conditions.

4. **OOC Handling**  
   - Configure CHKOOC60 parameters accurately.
   - Review OOC flags regularly to avoid prolonged non-compliance.
   - Integrate OOC detection with maintenance workflows.

5. **Regulatory Compliance**  
   - Align procedures with both federal and state-specific requirements.
   - Keep calibration and drift test records readily available for inspections.

---

## Source Attribution

- **Document 1 (Optime Precision)**: Provided formulas and logic for calculating operational minutes based on precision thresholds.
- **Document 2 (Calibration Correction Standard)**: Detailed procedure for implementing automatic calibration correction, including configuration and control mechanisms.
- **Document 3 (PADEP Terms and Notes)**: Defined certification phases, drift test requirements, and LMESE calculation methodology.
- **Document 4 (7-Day Calibration Error Test)**: Supplied example drift test data and structure for reporting calibration errors.
- **Document 5 (CHKOOC60 Validation)**: Explained automated OOC detection logic, tool configuration, and regulatory definitions for OOC periods.

---

If you’d like, I can create a **visual workflow diagram** showing how precision calculation, calibration correction, drift testing, and OOC management fit together in a CEMS compliance cycle. Would you like me to add that?

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_AmmoniaSlip_AmmoniaSlipCalculationxlsx_7514d17d.xlsx](../tools/engineering_white_papers_WhitePapers_AmmoniaSlip_AmmoniaSlipCalculationxlsx_7514d17d.xlsx)** (0.02 MB)
- **[engineering_white_papers_WhitePapers_AmmoniaSlip_ESCAmmoniaSlipCalculationxls_cbc4be89.xls](../tools/engineering_white_papers_WhitePapers_AmmoniaSlip_ESCAmmoniaSlipCalculationxls_cbc4be89.xls)** (0.04 MB)
- **[engineering_white_papers_WhitePapers_AmmoniaSlip_NH3slipcalculationsxls_692ae2a3.xls](../tools/engineering_white_papers_WhitePapers_AmmoniaSlip_NH3slipcalculationsxls_692ae2a3.xls)** (0.10 MB)
- **[engineering_white_papers_WhitePapers_Moisture_MoistureCalculationsxlsx_b389940b.xlsx](../tools/engineering_white_papers_WhitePapers_Moisture_MoistureCalculationsxlsx_b389940b.xlsx)** (0.19 MB)
- **[engineering_white_papers_WhitePapers_Moisture_RMBMoistureCalculationxls_107f6bfc.xls](../tools/engineering_white_papers_WhitePapers_Moisture_RMBMoistureCalculationxls_107f6bfc.xls)** (0.04 MB)
- **[engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx](../tools/engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx)** (0.02 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## Glossary

- **CEMS**: Continuous Emissions Monitoring System
