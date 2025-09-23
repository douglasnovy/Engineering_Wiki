---
title: Calibration
consolidated: true
sources: 5
conflicts: 0
confidence: 0.90
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_OptimePrecision20050211JLBpdf_2c025a7f.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CalibrationCorrection_EngineeringStandard-CalibrationCorrection-Rev11-01-2021pdf_605a61ca.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPTermsandNotesdocx_cf04b587.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_7-DayCalibrationErrorTestpdf_f17bcd7c.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_StackVision_CHKOOC60Validationdocx_a7cc510e.md']  # This would be a timestamp
---

### Title
**Calibration Precision, Correction, and Out-of-Control Validation in Continuous Emissions Monitoring Systems (CEMS)**

---

### Overview
Continuous Emissions Monitoring Systems (CEMS) are subject to strict regulatory requirements under **40 CFR Part 60** and **Part 75** to ensure accurate measurement and reporting of emissions data. Key elements of compliance include maintaining calibration precision, applying calibration corrections, performing certification tests, and validating out-of-control (OOC) periods. This consolidated document integrates engineering standards, calculation methods, regulatory definitions, and validation tools to provide a comprehensive guide for managing calibration and precision in CEMS operations.

---

### Key Concepts

1. **Calibration Precision**  
   Precision refers to the repeatability of analyzer readings during calibration checks. It is calculated differently depending on whether the precision exceeds 60 units or is 60 units or less.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span reference values compared to actual calibration results. This ensures compliance with regulatory accuracy requirements.

3. **Certification Tests**  
   Regulatory bodies such as the Pennsylvania Department of Environmental Protection (PADEP) require certification tests, including the 7-Day Calibration Error Test, to verify analyzer performance and data acquisition system accuracy.

4. **Out-of-Control (OOC) Periods**  
   OOC periods occur when calibration results exceed defined limits. Tools like **CHKOOC60** automate the identification and marking of OOC data according to Part 60 rules.

---

### Technical Details

#### 1. Calibration Precision Calculation (Document 1)
Two formulas are used depending on the precision value:

- **Precision > 60**:
  ```c
  calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
  ```

- **Precision ≤ 60**:
  ```c
  calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
  ```

These formulas determine the optimal operating minutes for calibration precision evaluation.

---

#### 2. Calibration Correction Standard (Document 2)
- **Zero Offset** and **Gain** are calculated from:
  - Expected Span (default = 1)
  - Expected Zero (default = 0)
  - Span Result (default = 1)
  - Zero Result (default = 0)
- Corrections are applied at the end of the calibration sequence.
- Functionality includes:
  - Resetting corrections until the next calibration
  - Disabling corrections via pseudo digital I/O
  - Setting alarms based on adjustment thresholds

---

#### 3. PADEP Certification Requirements (Document 3)
- **7-Day Drift Test**: Measures calibration drift over seven consecutive days.
- **DAHS Verification**: Confirms data acquisition and handling system accuracy.
- **Lowest Monitored Emissions Standard Equivalent (LMESE)**:
  - Default: Full Scale (FS) / 2
  - Formula for Calibration Error (CE):
    ```
    CE = |R – A| / LMESE * 100
    ```
    Where:
    - R = Reference value
    - A = Actual value
- Phase-based implementation:
  - Phase I: Implementation and MP approval
  - Phase II: Testing (within 210 days of startup or 60 days of normal capacity)
  - Phase III: Certification

---

#### 4. 7-Day Calibration Error Test (Document 4)
- Conducted for each monitored parameter (e.g., NOx, O₂).
- Compares reference and actual values at zero and span levels.
- Pass/Fail determined by percent calibration error against limits.
- Example parameters:
  - Instrument Span: 20.000 (Low NOx)
  - Instrument Span: 100.000 (High NOx)
  - Instrument Span: 25.000 (O₂ Dry)

---

#### 5. CHKOOC60 Validation Tool (Document 5)
- **Purpose**: Determines validity for Part 60 parameters during calibration drift.
- **Key Switches**:
  - `-n`: No database update
  - `-r`: No OOC flag propagation
  - `-o`: Disable cascading
  - `-m`: Overwrite method code
- **OOC Period Definitions**:
  - Start: End of previous good calibration
  - End: End of subsequent good calibration (limits apply)
  - Special rules for exceeding 2× or 4× limits
- **Dual Range Analyzer Support**: Marks merge channel parameter OOC when either range is OOC.

---

### Best Practices

1. **Maintain Accurate Calibration Records**  
   Record all zero and span reference values, results, and applied corrections for regulatory compliance.

2. **Automate OOC Detection**  
   Use tools like CHKOOC60 to ensure consistent application of Part 60 rules and avoid manual errors.

3. **Perform Regular Certification Tests**  
   Schedule and document 7-Day Drift and Calibration Error Tests to meet PADEP and EPA requirements.

4. **Apply Corrections Judiciously**  
   Enable/disable calibration corrections based on operational needs and regulatory thresholds.

5. **Monitor Precision Trends**  
   Use precision calculation formulas to detect deviations early and adjust maintenance schedules accordingly.

---

### Source Attribution
- **Document 1 (Optime Precision)**: Provided formulas for calculating optimal operating minutes based on calibration precision thresholds.
- **Document 2 (Calibration Correction Standard)**: Defined procedures and configuration for automatic calibration correction, including zero offset and gain calculations.
- **Document 3 (PADEP Terms and Notes)**: Detailed regulatory definitions, certification phases, and calibration error calculation methods.
- **Document 4 (7-Day Calibration Error Test)**: Supplied example test data and pass/fail criteria for calibration error evaluation.
- **Document 5 (CHKOOC60 Validation)**: Explained automated OOC validation logic, tool configuration, and Part 60 compliance rules.

---

If you’d like, I can also create a **flowchart** showing the relationship between calibration precision calculation, correction application, certification testing, and OOC validation for a complete operational workflow. Would you like me to prepare that?

## See Also

- [[Environmental]] - **Certification Tests**  
   Regulatory bodies suc...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
