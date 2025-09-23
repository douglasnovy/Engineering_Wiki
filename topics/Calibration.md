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
Continuous Emissions Monitoring Systems (CEMS) are subject to strict regulatory requirements under **40 CFR Part 60** and **Part 75**. These requirements mandate regular calibration, drift testing, and corrective actions to ensure data accuracy and compliance. This consolidated document outlines the key concepts, technical procedures, and best practices for:

- Calculating optimal calibration precision and operating time
- Implementing automatic calibration correction
- Understanding Pennsylvania Department of Environmental Protection (PADEP) certification terms
- Conducting 7-day calibration error tests
- Validating and managing Out-of-Control (OOC) periods using CHKOOC60

---

### Key Concepts

1. **Calibration Precision**  
   Precision refers to the smallest measurable change in analyzer output that can be reliably detected. It impacts how often calibration should occur and how operating minutes are calculated.

2. **Calibration Correction**  
   Automatic calibration correction adjusts analyzer readings based on daily zero and span reference values to maintain accuracy between calibrations.

3. **PADEP Certification Requirements**  
   PADEP mandates specific certification tests (e.g., 7-day drift, DAHS verification) and defines calculation methods such as LMESE (Lowest Monitored Emissions Standard Equivalent).

4. **7-Day Calibration Error Test**  
   A regulatory test to verify that analyzer drift remains within allowable limits over a seven-day period.

5. **Out-of-Control (OOC) Management**  
   OOC periods occur when calibration results exceed regulatory limits. Tools like CHKOOC60 automate identification and flagging of OOC data.

---

### Technical Details

#### 1. Calibration Precision Calculation (Document 1)
Two formulas are used depending on whether precision is greater than 60 or less than/equal to 60:

- **Precision > 60:**
  ```c
  calcdoptime = (int)((((3600.0/(calcprecision * 60.0) -1 + (calcminutes *60.0))/3600.0) * (calcprecision*60.0)) + 0.001) / (calcprecision * 60.0);
  ```
- **Precision ≤ 60:**
  ```c
  calcdoptime = (int)((((60.0/calcprecision -1 + calcminutes)/60.0) *calcprecision) + 0.001) / calcprecision;
  ```

These calculations determine optimal operating minutes between calibrations based on analyzer precision.

---

#### 2. Calibration Correction Implementation (Document 2)
- **Inputs:** Expected Span (default 1), Expected Zero (default 0), Span Result (default 1), Zero Result (default 0)
- **Process:**
  - Calculate zero offset and gain from daily calibration results.
  - Write constants at the end of calibration phase (set “Write Constants at End of Phase” to NO).
  - Include pseudo digital I/O to disable gain/offset when necessary.
  - Record all adjustments for compliance documentation.
- **Regulatory Note:** Adjustments must be logged and reset at the next calibration.

---

#### 3. PADEP Certification Terms (Document 3)
- **Tests Required:** 7-day drift, DAHS verification, QA/QC plan
- **LMESE Calculation:**  
  Default = Full Scale (FS) ÷ 2  
  Calibration Error (CE) = |Reference – Actual| ÷ LMESE × 100
- **Phase Implementation:**
  - Phase I: Implementation and Monitoring Plan approval
  - Phase II: Testing within 210 days of startup or 60 days of achieving normal capacity
  - Phase III: Certification for DAHS and EDR samples

---

#### 4. 7-Day Calibration Error Test (Document 4)
- **Purpose:** Verify analyzer drift remains within limits over seven consecutive days.
- **Parameters Tested:** Example – MC3NOXLO, MC3O2DRY, MC3NOXHI
- **Results:** Pass/Fail based on percent calibration error compared to limits.
- **Data Recorded:** Zero-level and span-level reference vs. actual values, percent error, and pass/fail status.

---

#### 5. CHKOOC60 Validation and OOC Rules (Document 5)
- **Function:** Validates Part 60 parameters during calibration drift and flags OOC periods.
- **Key Switches:**
  - `-n` No database update
  - `-r` No OOC flag propagation
  - `-o` Disable cascading
  - `-m` Overwrite method code
- **OOC Period Definitions (40 CFR 60):**
  - Start: End of previous good calibration
  - End: End of subsequent good calibration (limits vary by exceedance factor)
  - Special rules for consecutive exceedances and 24-hour limits
- **Dual Range Analyzer Handling:** Marks merge channel parameter OOC when either range is OOC.

---

### Best Practices

1. **Precision Management**
   - Use correct formula based on precision value.
   - Regularly review precision settings to optimize calibration intervals.

2. **Calibration Correction**
   - Always log adjustments and reset at next calibration.
   - Implement disable functionality for troubleshooting or maintenance.

3. **Compliance Testing**
   - Schedule and document all PADEP-required tests.
   - Maintain clear records of LMESE calculations and CE results.

4. **OOC Handling**
   - Configure CHKOOC60 with correct parameter group and fuel control file.
   - Ensure OOC periods are accurately flagged to prevent compliance violations.

5. **Data Integrity**
   - Avoid modifying historical calibration data unless required for compliance.
   - Use pseudo I/O controls to safeguard against unintended gain/offset changes.

---

### Source Attribution
- **[Document 1: Optime Precision.xls]**  
  Provided formulas for calculating optimal operating minutes based on analyzer precision.

- **[Document 2: Calibration Correction Standard]**  
  Detailed procedure for implementing automatic calibration correction, including configuration constants and disable functionality.

- **[Document 3: PADEP Terms and Notes]**  
  Defined certification phases, LMESE calculation, and calibration error formula.

- **[Document 4: 7-Day Calibration Error Test]**  
  Provided example test data, parameters, and pass/fail criteria for drift testing.

- **[Document 5: CHKOOC60 Validation]**  
  Explained OOC detection logic, tool switches, and regulatory definitions for OOC periods.

---

I can also create a **flowchart or procedural checklist** that integrates these calibration, correction, and OOC management steps if you want a visual operational guide. Would you like me to prepare that next?

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

- [[Environmental]] - This consolidated document outlines the key concep...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System


## Glossary

- **CEMS**: Continuous Emissions Monitoring System


## Glossary

- **CEMS**: Continuous Emissions Monitoring System


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
