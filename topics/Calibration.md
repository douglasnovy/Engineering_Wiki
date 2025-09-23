---
title: Calibration
consolidated: true
sources: 5
conflicts: 0
confidence: 0.90
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_OptimePrecision20050211JLBpdf_2c025a7f.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CalibrationCorrection_EngineeringStandard-CalibrationCorrection-Rev11-01-2021pdf_605a61ca.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPTermsandNotesdocx_cf04b587.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_7-DayCalibrationErrorTestpdf_f17bcd7c.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_StackVision_CHKOOC60Validationdocx_a7cc510e.md']  # This would be a timestamp
---

### Title
**Calibration Precision, Correction, and Out-of-Control (OOC) Management in Continuous Emissions Monitoring Systems (CEMS)**

---

### Overview
Continuous Emissions Monitoring Systems (CEMS) are subject to strict regulatory requirements under **40 CFR Part 60** and **Part 75**. These requirements mandate regular calibration, precision verification, and corrective actions to ensure data accuracy and compliance. This consolidated document integrates procedures for calculating operational precision, applying calibration corrections, validating calibration drift results, and managing Out-of-Control (OOC) periods. It also incorporates Pennsylvania Department of Environmental Protection (PADEP) terminology and testing protocols.

---

### Key Concepts

1. **Calibration Precision**  
   Precision refers to the repeatability of analyzer measurements during calibration checks. It is calculated differently depending on whether the precision value exceeds 60 or is 60 or less.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span calibration results, ensuring compliance with regulatory tolerances.

3. **Out-of-Control (OOC) Periods**  
   OOC periods occur when calibration drift exceeds regulatory limits. These periods must be identified, flagged, and managed according to Part 60 rules.

4. **PADEP Certification and Testing**  
   PADEP requires specific certification tests, including 7-day drift tests, DAHS verification, and QA/QC plans, with defined calculation methods for calibration error.

5. **7-Day Calibration Error Test**  
   This test verifies that analyzer drift remains within acceptable limits over a seven-day period, using zero-level and span-level measurements.

---

### Technical Details

#### 1. Precision Calculation (Document 1)
```c
if (calcprecision > 60)
    calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
else
    calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
```
- **calcprecision**: precision value from calibration  
- **calcminutes**: operational minutes  
- Different formulas are applied depending on whether precision exceeds 60.

---

#### 2. Calibration Correction Configuration (Document 2)
- **Expected Span**: Default = 1  
- **Expected Zero**: Default = 0  
- **Span Result**: Default = 1  
- **Zero Result**: Default = 0  
- **Procedure**:
  - Write expected values and results to math constants during calibration.
  - Do **not** write constants at end of phase (set to NO).
  - Calculate **zero offset** and **gain** from calibration results.
  - Include pseudo digital I/O to disable gain/offset when required.
  - Record all adjustments for compliance.

---

#### 3. PADEP Calibration Error Calculation (Document 3)
- **LMESE**: Lowest Monitored Emissions Standard Equivalent  
  - Default = Full Scale / 2 (except for certain parameters like opacity, CO₂, O₂, VFR, dual range analyzers)
- **Calibration Error (CE)**:
  \[
  CE = \frac{|R - A|}{LMESE} \times 100
  \]
  - **R**: Reference value  
  - **A**: Actual value  
- Certification phases:
  - **Phase I**: Implementation and MP approval
  - **Phase II**: Testing (within 210 days of startup or 60 days after achieving normal capacity)
  - **Phase III**: Certification for DAHS and EDR samples

---

#### 4. 7-Day Calibration Error Test (Document 4)
- Conducted for each monitored parameter (e.g., NOx, O₂).
- Records zero-level and span-level drift values over seven consecutive days.
- Pass/Fail determined by comparing drift percentage to regulatory limits.
- Example:
  - Instrument Span: 20.000  
  - Zero-Level Drift: -0.065% → Pass  
  - Span-Level Drift: -0.571% → Pass

---

#### 5. CHKOOC60 Validation (Document 5)
- **Purpose**: Validates calibration drift for Part 60 parameters and flags OOC periods.
- **Key Switches**:
  - `-n`: No database update
  - `-r`: No OOC flag propagation
  - `-o`: Disable cascading
  - `-m`: Overwrite method code
- **OOC Definitions**:
  - Start: End of previous good calibration
  - End: End of subsequent good calibration (limits apply)
  - Special rules for exceeding 2× or 4× limits
- **Dual Range Analyzer**:
  - Target parameter marked OOC when either low or high range is OOC.

---

### Best Practices

1. **Precision Monitoring**  
   - Apply correct formula based on precision threshold.
   - Regularly review operational minutes and precision values.

2. **Calibration Correction**  
   - Always record adjustments.
   - Configure system to prevent overwriting constants prematurely.
   - Implement alarms for excessive correction levels.

3. **OOC Management**  
   - Use CHKOOC60 with proper parameter group configuration.
   - Ensure TOL parameter values > 0 during operating hours for valid OOC marking.

4. **Testing Compliance**  
   - Schedule and document 7-day drift tests.
   - Follow PADEP certification phases and timelines.

5. **Data Integrity**  
   - Maintain accurate DAHS verification records.
   - Disable correction functions when troubleshooting.

---

### Source Attribution
- **Document 1 (Optime Precision)**: Provided formulas for calculating operational precision based on thresholds.
- **Document 2 (Calibration Correction Standard)**: Detailed configuration steps for automatic calibration correction, including constants and I/O controls.
- **Document 3 (PADEP Terms and Notes)**: Defined PADEP-specific calibration error calculations, LMESE defaults, and certification phases.
- **Document 4 (7-Day Calibration Error Test)**: Supplied example test data and pass/fail criteria for drift testing.
- **Document 5 (CHKOOC60 Validation)**: Explained OOC period definitions, validation process, and tool configuration for Part 60 compliance.

---

If you’d like, I can also create a **flowchart** showing how precision calculation, calibration correction, and OOC validation fit together in the CEMS compliance workflow. Would you like me to prepare that?

## See Also

- [[Environmental]] - It also incorporates Pennsylvania Department of En...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
