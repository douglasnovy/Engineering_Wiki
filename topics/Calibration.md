---
title: Calibration
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_OptimePrecision20050211JLBpdf_2c025a7f.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CalibrationCorrection_EngineeringStandard-CalibrationCorrection-Rev11-01-2021pdf_605a61ca.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPTermsandNotesdocx_cf04b587.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_7-DayCalibrationErrorTestpdf_f17bcd7c.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_StackVision_CHKOOC60Validationdocx_a7cc510e.md']  # This would be a timestamp
---

### Title
**Calibration Precision, Correction, and Out-of-Control (OOC) Validation in Continuous Emissions Monitoring Systems (CEMS)**

---

### Overview
Accurate calibration and precision management are critical for Continuous Emissions Monitoring Systems (CEMS) compliance under regulatory frameworks such as **40 CFR Part 60** and **Part 75**. This consolidated guide integrates engineering standards, calculation methods, regulatory definitions, and validation tools to ensure reliable analyzer performance, proper calibration correction, and correct identification of out-of-control periods. It covers precision calculation formulas, calibration correction configuration, Pennsylvania Department of Environmental Protection (PADEP) compliance terms, 7-day calibration error testing, and CHKOOC60 validation procedures.

---

### Key Concepts

1. **Calibration Precision**  
   Precision refers to the repeatability of analyzer measurements during calibration checks. It is calculated differently depending on whether the precision value exceeds 60 or not.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span reference values to maintain compliance and accuracy.

3. **Regulatory Compliance (PADEP & CFR)**  
   Compliance requires adherence to specific test protocols (e.g., 7-day drift tests), data acquisition and handling system (DAHS) verification, and defined limits for calibration drift.

4. **Out-of-Control (OOC) Periods**  
   OOC periods occur when calibration results exceed regulatory limits for consecutive tests. These periods must be correctly identified and flagged in the monitoring system.

5. **7-Day Calibration Error Test**  
   A standardized test to verify analyzer stability over time by comparing reference and actual values for zero and span levels.

---

### Technical Details

#### 1. Precision Calculation (Document 1)
Two formulas are used depending on the precision threshold:

- **Precision > 60**  
  ```
  calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
  ```

- **Precision ≤ 60**  
  ```
  calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
  ```

These formulas determine optimal operating minutes based on calibration precision and elapsed minutes.

---

#### 2. Calibration Correction Configuration (Document 2)
- **Inputs Required:**
  - Expected Span (default = 1)
  - Expected Zero (default = 0)
  - Span Result (default = 1)
  - Zero Result (default = 0)

- **Procedure:**
  - Write expected values and results to math constants during calibration.
  - Ensure "Write Constants at End of Phase" is set to **NO** to evaluate corrections over the full sequence.
  - Calculate **zero offset** and **gain** based on differences between expected and actual calibration results.
  - Include pseudo digital I/O to enable/disable gain/offset adjustments.

- **Regulatory Requirement:**
  - Record all adjustments.
  - Provide reset and disable functionality.
  - Configure alarms for excessive adjustments.

---

#### 3. PADEP Compliance Terms (Document 3)
- **Certification Tests:**  
  - 7-Day drift  
  - DAHS verification  
  - QA/QC plan  
  - Sample reports

- **DAHS Accuracy Verification:**  
  - Opacity requires 60 one-minute averages and 10-second averages for one hour.

- **LMESE (Lowest Monitored Emissions Standard Equivalent):**  
  - Default = Full Scale (FS) / 2  
  - CE (Calibration Error) = |R – A| / LMESE × 100

- **Certification Phases:**  
  - Phase I: Implementation & MP approval  
  - Phase II: Testing (within 210 days of startup or 60 days of normal capacity)  
  - Phase III: Certification for DAHS and EDR sample

---

#### 4. 7-Day Calibration Error Test (Document 4)
- **Purpose:**  
  Verify analyzer drift stability over a 7-day period.

- **Parameters Recorded:**  
  - Zero-Level reference vs actual values  
  - Span-Level reference vs actual values  
  - Percent calibration error  
  - Pass/Fail results

- **Example:**  
  For MC3NOXLO with span = 20.000, errors such as -0.065% and -0.571% were recorded, all within limits.

---

#### 5. CHKOOC60 Validation (Document 5)
- **Function:**  
  Determines validity for Part 60 parameters during calibration drift.

- **Key Switches:**  
  - `-n` No database update  
  - `-r` No OOC flag propagation  
  - `-o` Disable cascading  
  - `-m` Overwrite method code

- **OOC Period Definitions (40 CFR 60):**
  - Start: End of previous good calibration  
  - End: End of subsequent good calibration (limits apply)  
  - Alternate start/end rules for exceeding 2× or 4× limits

- **Dual Range Analyzer Handling:**  
  - Target parameter marked OOC when either low or high range is OOC.

---

### Best Practices

1. **Precision Management:**  
   Use correct formula based on precision threshold to ensure accurate operating time calculations.

2. **Calibration Correction:**  
   Always record adjustments, configure alarms, and allow reset/disable functionality to maintain compliance.

3. **Regulatory Testing:**  
   Perform 7-day drift tests regularly and maintain documentation for certification phases.

4. **OOC Validation:**  
   Configure CHKOOC60 correctly to ensure accurate OOC flagging, especially for dual range analyzers.

5. **Data Integrity:**  
   Ensure DAHS accuracy verification meets regulatory averaging requirements.

---

### Source Attribution
- **Document 1 (Optime Precision)**: Provided formulas for calculating optimal operating minutes based on calibration precision thresholds.
- **Document 2 (Calibration Correction Standard)**: Detailed configuration steps for automatic calibration correction, including regulatory requirements and alarm settings.
- **Document 3 (PADEP Terms and Notes)**: Defined regulatory terms, certification phases, and calculation methods for calibration error under PADEP rules.
- **Document 4 (7-Day Calibration Error Test)**: Supplied example test data and methodology for verifying analyzer drift stability.
- **Document 5 (CHKOOC60 Validation)**: Explained tool usage, OOC period definitions, and configuration for dual range analyzer compliance under Part 60.

---

If you want, I can also create a **flowchart** showing the relationship between precision calculation, calibration correction, regulatory testing, and OOC validation so operators can follow a visual process. Would you like me to do that?

## See Also

- [[Environmental]] - It covers precision calculation formulas, calibrat...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
