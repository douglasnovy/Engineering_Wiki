---
title: Calibration
consolidated: true
sources: 5
conflicts: 0
confidence: 0.90
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_OptimePrecision20050211JLBpdf_2c025a7f.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CalibrationCorrection_EngineeringStandard-CalibrationCorrection-Rev11-01-2021pdf_605a61ca.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPTermsandNotesdocx_cf04b587.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_7-DayCalibrationErrorTestpdf_f17bcd7c.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_StackVision_CHKOOC60Validationdocx_a7cc510e.md']  # This would be a timestamp
---

### Title
**Calibration Precision, Correction, and Out-of-Control (OOC) Validation in Continuous Emissions Monitoring Systems (CEMS)**

---

### Overview
Continuous Emissions Monitoring Systems (CEMS) are subject to strict regulatory requirements under **40 CFR Part 60** and **Part 75**. These requirements include maintaining calibration precision, applying calibration corrections, and validating out-of-control (OOC) periods. Proper implementation ensures data integrity, regulatory compliance, and operational efficiency. This consolidated entry integrates calculation methods, calibration correction standards, regulatory definitions, and validation tools used in CEMS operations.

---

### Key Concepts

1. **Calibration Precision**  
   Precision refers to the closeness of agreement between repeated measurements under unchanged conditions. In CEMS, calibration precision is calculated differently depending on whether the precision exceeds 60 units or is 60 or less.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span calibration results. This ensures that reported emissions data reflect accurate measurements.

3. **Regulatory Testing Requirements**  
   Agencies such as the Pennsylvania Department of Environmental Protection (PADEP) require specific certification tests, including the 7-Day Calibration Error Test, to verify system accuracy and compliance.

4. **Out-of-Control (OOC) Periods**  
   OOC periods occur when calibration results exceed regulatory limits. These periods must be identified, documented, and resolved according to Part 60 rules.

---

### Technical Details

#### 1. Calibration Precision Calculation (Document 1)
The **Optime Precision** function calculates operating minutes based on calibration precision:

- **For precision > 60:**
```c
calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
```

- **For precision ≤ 60:**
```c
calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
```

These formulas determine optimal operating time based on calibration precision and minutes of operation.

---

#### 2. Calibration Correction Standards (Document 2)
Key configuration elements for calibration correction:

- **Math Constants:**
  - Expected Span: Default = 1
  - Expected Zero: Default = 0
  - Span Result: Default = 1
  - Zero Result: Default = 0

- **Procedure:**
  - Write expected values and results to math constants during calibration.
  - Do **not** write constants at the end of phase to ensure daily evaluation.
  - Calculate both zero offset and gain adjustments.
  - Include pseudo digital I/O to disable gain/offset when necessary.
  - Implement alarms for excessive adjustments.

---

#### 3. Regulatory Definitions and Testing (Document 3 & 4)
- **LMESE (Lowest Monitored Emissions Standard Equivalent):**  
  Used to determine daily zero/upscale calibration drift.  
  Formula:  
  \[
  CE = \frac{|R - A|}{LMESE} \times 100
  \]
  Where:
  - \( R \) = Reference value
  - \( A \) = Actual value

- **PADEP Defaults:**  
  LMESE = Full Scale (FS) / 2 (except for certain parameters like opacity, CO₂, O₂, VFR, dual range).

- **7-Day Calibration Error Test:**  
  Conducted to verify calibration stability over a week.  
  Parameters include zero-level and span-level measurements, percent calibration error, and pass/fail results.

---

#### 4. Out-of-Control (OOC) Validation (Document 5)
**CHKOOC60 Tool** validates Part 60 parameters during calibration drift:

- **Key Switches:**
  - `-n` No database update
  - `-r` No OOC flag propagation
  - `-o` Disable cascading
  - `-m` Overwrite method code

- **OOC Period Definitions:**
  - Start: End of previous good calibration
  - End: End of subsequent good calibration (limits apply)
  - Special rules for exceeding 2× or 4× limits
  - Non-operating hours are excluded from OOC marking

- **Dual Range Analyzer Handling:**
  - Target parameter marked OOC when either low or high range channel is OOC.

---

### Best Practices

1. **Maintain Accurate Calibration Records**  
   Record all zero and span calibration results, offsets, and gains for audit purposes.

2. **Implement Automated Correction with Manual Override**  
   Allow operators to disable or reset calibration corrections when necessary.

3. **Regularly Perform Regulatory Tests**  
   Schedule and document 7-Day Calibration Error Tests and other certification tests per regulatory timelines.

4. **Use OOC Validation Tools Consistently**  
   Configure CHKOOC60 or equivalent tools to correctly identify and mark OOC periods, ensuring compliance.

5. **Monitor Precision Trends**  
   Use precision calculations to anticipate and address potential calibration drift before it leads to OOC conditions.

---

### Source Attribution

- **Document 1 (Optime Precision.xls)**: Provided formulas for calculating operating minutes based on calibration precision thresholds.
- **Document 2 (Calibration Correction Standard)**: Defined procedures and configuration for automatic calibration correction, including constants, offsets, and gain adjustments.
- **Document 3 (PADEP Terms and Notes)**: Clarified regulatory definitions, LMESE calculation, and certification phases.
- **Document 4 (7-Day Calibration Error Test)**: Supplied example test data and structure for calibration error reporting.
- **Document 5 (CHKOOC60 Validation)**: Detailed OOC validation process, tool configuration, and regulatory definitions for OOC periods.

---

If you’d like, I can **create a visual workflow diagram** showing how calibration precision calculation, correction application, regulatory testing, and OOC validation fit together in a CEMS compliance cycle. Would you like me to prepare that?

## See Also

- [[Environmental]] - **Regulatory Testing Requirements**  
   Agencies ...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
