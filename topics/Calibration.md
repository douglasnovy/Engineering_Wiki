---
title: Calibration
consolidated: true
sources: 5
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Calculations_OptimePrecision20050211JLBpdf_2c025a7f.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_CalibrationCorrection_EngineeringStandard-CalibrationCorrection-Rev11-01-2021pdf_605a61ca.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_PADEPRev8_PADEPTermsandNotesdocx_cf04b587.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_SampleTests_7-DayCalibrationErrorTestpdf_f17bcd7c.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_StackVision_CHKOOC60Validationdocx_a7cc510e.md']  # This would be a timestamp
---

### Title
**Calibration Precision, Correction, and Out-of-Control (OOC) Management in Continuous Emissions Monitoring Systems (CEMS)**

---

### Overview
Accurate calibration and precision management are critical for Continuous Emissions Monitoring Systems (CEMS) to comply with regulatory requirements under **40 CFR Part 60** and **Part 75**. This consolidated guide integrates procedures for calculating operational precision, applying calibration corrections, conducting certification and drift tests, and managing Out-of-Control (OOC) conditions. It draws from engineering standards, regulatory definitions, and practical test data to provide a comprehensive reference for operators, engineers, and compliance managers.

---

### Key Concepts

1. **Calibration Precision**  
   Precision refers to the repeatability of analyzer readings during calibration. It is calculated differently depending on whether the precision value is above or below 60 units.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span reference values to maintain compliance and accuracy.

3. **Certification and Drift Testing**  
   Regulatory agencies such as the Pennsylvania Department of Environmental Protection (PADEP) require specific certification tests, including 7-Day Calibration Error Tests, to verify analyzer performance over time.

4. **Out-of-Control (OOC) Conditions**  
   OOC conditions occur when calibration results exceed regulatory limits for consecutive tests. Tools like **CHKOOC60** automate detection and flagging of OOC periods.

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
These formulas determine optimal operating minutes based on calibration precision and elapsed time.

---

#### 2. Calibration Correction Procedure (Document 2)
- **Inputs:** Expected Span (default 1), Expected Zero (default 0), Span Result (default 1), Zero Result (default 0).
- **Process:**  
  - Calculate **zero offset** and **gain** from differences between expected and actual calibration values.  
  - Apply corrections at the end of the calibration sequence.  
  - Maintain previous correction values until the next calibration.
- **Control Features:**  
  - Ability to disable gain/offset adjustments.  
  - Alarm triggers when adjustments exceed agreed thresholds.  
  - Reset functionality between calibrations.

---

#### 3. Certification and Drift Testing (Document 3 & 4)
- **PADEP Requirements:**  
  - **7-Day Drift Test**: Measures calibration error over seven consecutive days.  
  - **LMESE** (Lowest Monitored Emissions Standard Equivalent) defines the baseline for drift calculations:  
    \[
    CE = \frac{|R - A|}{LMESE} \times 100
    \]
    where \( R \) = reference value, \( A \) = actual value.
  - Default LMESE = Full Scale / 2 (except for certain parameters like opacity, CO₂, O₂).
- **Sample Test Data:**  
  - Reports include zero-level and span-level values, limits, percent calibration error, and pass/fail results for each component.

---

#### 4. Out-of-Control (OOC) Management (Document 5)
- **CHKOOC60 Tool:**  
  - Validates Part 60 parameters during calibration drift.  
  - Flags OOC periods based on regulatory definitions:
    - **Start OOC:** End of previous good calibration or after consecutive limit exceedances.
    - **End OOC:** End of subsequent good calibration, within regulatory time limits.
  - Only marks hours where the corresponding TOL parameter > 0 (operating hours).
- **Dual Range Analyzer Support:**  
  - Can mark merged parameters as OOC when either low or high range is OOC.

---

### Best Practices

1. **Maintain Consistent Calibration Records**  
   - Log all zero and span reference values, results, and applied corrections.
   - Ensure calibration corrections are traceable and reversible.

2. **Automate OOC Detection**  
   - Use tools like CHKOOC60 to reduce manual review errors.
   - Configure alarms for early detection of drift trends.

3. **Follow Regulatory Test Schedules**  
   - Conduct 7-Day Drift Tests and other certification tests within required timeframes.
   - Adhere to PADEP and EPA guidelines for test execution and reporting.

4. **Validate Precision Calculations**  
   - Apply correct formula based on precision threshold.
   - Regularly review calculation logic for software implementations.

5. **Disable Corrections When Necessary**  
   - Implement pseudo digital I/O controls to disable gain/offset adjustments during troubleshooting or maintenance.

---

### Source Attribution

- **[Document 1: Optime Precision]**  
  Provided formulas and logic for calculating operational minutes based on calibration precision thresholds.

- **[Document 2: Calibration Correction Standard]**  
  Detailed procedure for automatic calibration correction, including configuration constants, control features, and compliance considerations.

- **[Document 3: PADEP Terms and Notes]**  
  Defined certification test requirements, LMESE calculation, and regulatory timelines for implementation and testing.

- **[Document 4: 7-Day Calibration Error Test]**  
  Supplied example test data structure, pass/fail criteria, and reporting format for drift tests.

- **[Document 5: CHKOOC60 Validation]**  
  Explained automated OOC detection logic, tool configuration, and regulatory definitions for OOC periods.

---

If you’d like, I can create a **visual workflow diagram** showing how precision calculation, calibration correction, drift testing, and OOC management fit together in a CEMS compliance cycle. Would you like me to prepare that?

## Related Tools and Spreadsheets

The following tools and spreadsheets are available for this topic:

- **[engineering_white_papers_WhitePapers_AmmoniaSlip_AmmoniaSlipCalculationxlsx_7514d17d.xlsx](../tools/engineering_white_papers_WhitePapers_AmmoniaSlip_AmmoniaSlipCalculationxlsx_7514d17d.xlsx)** (0.02 MB)
- **[engineering_white_papers_WhitePapers_AmmoniaSlip_ESCAmmoniaSlipCalculationxls_cbc4be89.xls](../tools/engineering_white_papers_WhitePapers_AmmoniaSlip_ESCAmmoniaSlipCalculationxls_cbc4be89.xls)** (0.04 MB)
- **[engineering_white_papers_WhitePapers_AmmoniaSlip_NH3slipcalculationsxls_692ae2a3.xls](../tools/engineering_white_papers_WhitePapers_AmmoniaSlip_NH3slipcalculationsxls_692ae2a3.xls)** (0.10 MB)
- **[engineering_white_papers_WhitePapers_Moisture_MoistureCalculationsxlsx_b389940b.xlsx](../tools/engineering_white_papers_WhitePapers_Moisture_MoistureCalculationsxlsx_b389940b.xlsx)** (0.19 MB)
- **[engineering_white_papers_WhitePapers_Moisture_RMBMoistureCalculationxls_107f6bfc.xls](../tools/engineering_white_papers_WhitePapers_Moisture_RMBMoistureCalculationxls_107f6bfc.xls)** (0.04 MB)
- **[engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx](../tools/engineering_white_papers_WhitePapers_Moisture_SaturationMoistureCalculationxlsx_374381ed.xlsx)** (0.02 MB)

*For additional tools, see the [Engineering Tools Index](../tools/README.md)*

## See Also

- [[Environmental]] - **Certification and Drift Testing**  
   Regulator...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
