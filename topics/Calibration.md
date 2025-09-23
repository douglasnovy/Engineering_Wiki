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
Continuous Emissions Monitoring Systems (CEMS) are subject to strict regulatory requirements under **40 CFR Part 60** and **Part 75**. These requirements ensure accurate measurement of emissions through regular calibration, precision checks, and drift testing. This consolidated guide covers the calculation of operating precision, implementation of calibration correction, Pennsylvania Department of Environmental Protection (PADEP) certification terms, execution of 7-day calibration error tests, and the use of CHKOOC60 validation tools for Out-of-Control (OOC) data handling.

---

### Key Concepts

1. **Operating Precision Calculation**  
   Precision calculations determine the allowable operating time between calibrations based on analyzer performance. Different formulas apply depending on whether the precision exceeds 60 units or not.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span calibration results, ensuring compliance with regulatory accuracy requirements.

3. **PADEP Certification Requirements**  
   PADEP mandates specific certification tests, including 7-day drift tests, DAHS verification, and QA/QC plan adherence, with defined timelines for implementation, testing, and certification.

4. **7-Day Calibration Error Test**  
   This test evaluates analyzer drift over a 7-day period, comparing reference and actual values for zero and span levels against regulatory limits.

5. **Out-of-Control (OOC) Validation**  
   OOC validation tools, such as CHKOOC60, determine when data should be flagged as out-of-control based on calibration drift limits and operational status.

---

### Technical Details

#### 1. Operating Precision Formula (Document 1)
- **For precision > 60:**
  ```c
  calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
  ```
- **For precision ≤ 60:**
  ```c
  calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
  ```

#### 2. Calibration Correction Implementation (Document 2)
- **Inputs:**
  - Expected Span (default = 1)
  - Expected Zero (default = 0)
  - Span Result (default = 1)
  - Zero Result (default = 0)
- **Process:**
  - Calculate zero offset and gain from calibration results.
  - Disable gain/offset via pseudo digital I/O when required.
  - Record all adjustments for regulatory compliance.
  - Configure alarms for excessive correction levels.

#### 3. PADEP Certification Terms (Document 3)
- **Tests Required:**
  - 7-Day Drift
  - DAHS Accuracy Verification
  - QA/QC Plan Review
- **LMESE Calculation:**
  - Default = Full Scale (FS) / 2
  - CE = |R – A| / LMESE × 100
- **Phases:**
  - Phase I: Implementation & MP Approval
  - Phase II: Testing (within 210 days of startup or 60 days of normal capacity)
  - Phase III: Certification

#### 4. 7-Day Calibration Error Test (Document 4)
- **Parameters Tested:** NOx, O₂, etc.
- **Procedure:**
  - Record zero and span reference values.
  - Compare actual readings to limits.
  - Calculate percent calibration error.
  - Pass/Fail determination based on regulatory thresholds.

#### 5. CHKOOC60 Validation Rules (Document 5)
- **OOC Period Definitions (Part 60):**
  - Start: End of previous good calibration.
  - End: End of subsequent good calibration (limits apply).
  - Alternate start/end rules for exceeding 2× or 4× limits.
- **Tool Behavior:**
  - Marks data OOC only when TOL parameter > 0.
  - Ignores non-operating hours.
  - Supports dual-range analyzer configurations.

---

### Best Practices

1. **Maintain Accurate Calibration Records**  
   Always log zero and span calibration results, offsets, and gains for audit readiness.

2. **Use Automated Correction Judiciously**  
   Enable/disable gain/offset adjustments based on operational needs and regulatory limits.

3. **Perform Regular Drift and Precision Checks**  
   Schedule 7-day drift tests and precision calculations to detect performance degradation early.

4. **Configure OOC Validation Properly**  
   Ensure CHKOOC60 parameters and TOL values are correctly set to avoid false OOC flags.

5. **Adhere to Certification Timelines**  
   Follow PADEP and federal timelines for implementation, testing, and certification to avoid compliance issues.

---

### Source Attribution

- **[Document 1: Optime Precision.xls]**  
  Provided formulas for calculating operating precision based on analyzer performance.

- **[Document 2: Calibration Correction Standard]**  
  Detailed procedures for implementing automatic calibration correction, including configuration and compliance considerations.

- **[Document 3: PADEP Terms and Notes]**  
  Defined certification requirements, LMESE calculations, and compliance phases for PADEP-regulated facilities.

- **[Document 4: 7-Day Calibration Error Test]**  
  Supplied example test data and methodology for evaluating calibration drift over a 7-day period.

- **[Document 5: CHKOOC60 Validation]**  
  Explained OOC validation rules, tool configuration, and operational constraints under Part 60.

---

If you’d like, I can create a **flowchart** showing the relationship between calibration correction, precision calculation, drift testing, and OOC validation for easier operational understanding. Would you like me to prepare that?

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

- [[Environmental]] - This consolidated guide covers the calculation of ...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
