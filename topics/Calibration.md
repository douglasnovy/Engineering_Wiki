---
title: Calibration
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_Calculations_OptimePrecision20050211JLBpdf_2c025a7f.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_CalibrationCorrection_EngineeringStandard-CalibrationCorrection-Rev11-01-2021pdf_605a61ca.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPTermsandNotesdocx_cf04b587.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_SampleTests_7-DayCalibrationErrorTestpdf_f17bcd7c.md', 'data\\extracted\\set_scaling_test\\engineering_white_papers_WhitePapers_StackVision_CHKOOC60Validationdocx_a7cc510e.md']  # This would be a timestamp
---

### Title
**Calibration Precision, Correction, and Out-of-Control (OOC) Management in Emissions Monitoring Systems**

---

### Overview
Accurate calibration and precision management are critical for continuous emissions monitoring systems (CEMS) to comply with regulatory requirements such as **40 CFR Part 60** and **Part 75**. This consolidated guide integrates engineering standards, calculation methodologies, regulatory definitions, and validation tools to ensure reliable data acquisition, proper calibration correction, and systematic handling of out-of-control conditions.

---

### Key Concepts

1. **Calibration Precision**  
   Precision refers to the repeatability of measurement results during calibration. It is quantified using specific formulas that vary depending on whether the precision exceeds or is less than 60 units.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span reference values compared to calibration results. This ensures compliance with regulatory drift limits.

3. **Regulatory Testing Requirements**  
   Agencies such as PADEP require certification tests (e.g., 7-Day Drift, DAHS verification) to validate system accuracy and compliance.

4. **Out-of-Control (OOC) Conditions**  
   OOC conditions occur when calibration results exceed regulatory limits for consecutive tests. Tools like **CHKOOC60** automate detection and flagging of OOC periods.

5. **Data Acquisition and Handling System (DAHS)**  
   DAHS accuracy verification ensures correct data processing, averaging, and reporting, including handling of invalid or substituted data.

---

### Technical Details

#### 1. Precision Calculation (Document 1)
Two formulas are used depending on the precision threshold:

- **For precision > 60:**
```c
calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
```

- **For precision ≤ 60:**
```c
calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
```

These calculations determine optimal operating minutes for calibration precision assessment.

---

#### 2. Calibration Correction Implementation (Document 2)
- **Inputs:** Expected Span (default 1), Expected Zero (default 0), Span Result, Zero Result.
- **Process:**  
  - Calculate **zero offset** and **gain** from calibration differences.  
  - Write constants at the end of calibration phase (set "Write Constants at End of Phase" to NO).
  - Include pseudo digital I/O to enable/disable gain/offset adjustments.
  - Record all adjustments for compliance documentation.
  - Configure alarms for excessive correction levels.

---

#### 3. Regulatory Definitions & Testing (Document 3)
- **LMESE (Lowest Monitored Emissions Standard Equivalent):**  
  Used to calculate calibration error:  
  \[
  CE = \frac{|R - A|}{LMESE} \times 100
  \]
  where \( R \) = Reference, \( A \) = Actual.
- **PADEP Defaults:** LMESE = FS / 2 (except for certain parameters like Opacity, CO₂, O₂).
- **Certification Phases:**  
  - Phase I: Implementation & MP approval  
  - Phase II: Testing (within 210 days of startup or 60 days of achieving capacity)  
  - Phase III: DAHS & EDR certification

---

#### 4. 7-Day Calibration Error Test (Document 4)
- **Purpose:** Verify calibration stability over a 7-day period.
- **Parameters:** Zero-Level and Span-Level readings compared to limits.
- **Pass/Fail Criteria:** Based on percent calibration error relative to limits.
- **Example:**  
  - Instrument Span: 20.000  
  - Error: -0.065% → Pass

---

#### 5. Out-of-Control Management (Document 5)
- **CHKOOC60 Tool:**  
  - Validates Part 60 parameters during calibration drift.
  - Flags OOC periods based on TOL parameter values and operational hours.
- **OOC Period Definitions (40 CFR 60):**
  - Start: End of previous good calibration  
  - End: End of subsequent good calibration (limits vary: 2× or 4× thresholds)
  - Special case: Start 24 hours after previous calibration, end at next calibration.
- **Dual Range Analyzer Handling:**  
  - Marks merge channel parameter OOC if either range is OOC.

---

### Best Practices

1. **Maintain Accurate Calibration Records**  
   Document all zero/span results, offsets, and gains for compliance audits.

2. **Automate OOC Detection**  
   Use tools like CHKOOC60 to ensure timely identification and resolution of OOC conditions.

3. **Configure Alarms for Drift**  
   Set alarms for calibration corrections exceeding agreed thresholds to prevent unnoticed drift.

4. **Follow Regulatory Testing Schedules**  
   Adhere to PADEP and EPA timelines for certification and drift testing.

5. **Separate Operational and Non-Operational Data**  
   Ensure OOC tools do not alter non-operating hour data to maintain integrity.

---

### Source Attribution

- **Document 1 (Optime Precision.xls)**: Provided precision calculation formulas for different thresholds.
- **Document 2 (Calibration Correction Standard)**: Detailed engineering practices for implementing automatic calibration correction, including configuration parameters and compliance considerations.
- **Document 3 (PADEP Terms and Notes)**: Defined regulatory terms, testing phases, and calibration error calculation methods.
- **Document 4 (7-Day Calibration Error Test)**: Supplied example test data and pass/fail criteria for drift verification.
- **Document 5 (CHKOOC60 Validation)**: Explained automated OOC detection logic, tool configuration, and regulatory definitions for OOC periods.

---

If you’d like, I can **create a visual workflow diagram** showing how precision calculation, calibration correction, and OOC detection integrate into daily CEMS operations. This would make the process easier to follow for operators and compliance engineers. Would you like me to do that?

## Glossary

- **CEMS**: Continuous Emissions Monitoring System
