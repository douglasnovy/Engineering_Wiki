---
title: Calibration
consolidated: true
sources: 2
conflicts: 1
confidence: 0.60
generated: ['data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationActivityBottlesxlsx_4c681ef1.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationsActivityCustomerdocx_242035cd.md']  # This would be a timestamp
---

## Title  
**Calibration Procedures for Dual-Range NOx and CO Systems with O₂ Diluent in StackVision**

---

## Overview  
Calibration of Continuous Emissions Monitoring Systems (CEMS) is essential for ensuring accurate measurement and compliance with regulatory requirements such as U.S. EPA Part 75. This consolidated guide focuses on calibration procedures for systems running **dual-range NOx and CO analyzers** with **O₂ as the diluent gas**, specifically within the **StackVision** platform. It integrates calibration gas specifications, operational timing, and procedural sequencing to optimize accuracy and minimize downtime.

---

## Key Concepts  

### 1. **Dual-Range Calibration**  
Dual-range analyzers measure gases across two distinct concentration ranges (low and high). Calibration must be performed for each range to ensure accuracy across the full measurement spectrum.

### 2. **Calibration Gases and Concentrations**  
Calibration gases are stored in bottles with known concentrations. These gases are used to verify analyzer accuracy at multiple span levels.

**Example Calibration Gas Concentrations:**
| Gas | Range | Level | Concentration |
|-----|-------|-------|---------------|
| NOx | High Range | High | 900 ppm |
| NOx | High Range | Mid | 500 ppm |
| NOx | High Range | Low | 200 ppm |
| NOx | Low Range | High | 90 ppm |
| CO  | High Range | High | 950 ppm |
| CO  | Low Range | High | 95 ppm |
| O₂  | — | High | 0.22 |
| O₂  | — | Mid | 0.16 |
| O₂  | — | Low | 0.09 |

### 3. **Calibration Modes**  
- **Daily Calibration:** Scheduled routine calibration to verify analyzer performance.
- **Diagnostic Calibration:** Triggered by analyzer self-checks outside of the daily schedule.
- **Internal Analyzer Calibration:** Performed by the analyzer itself to address specific range or O₂ measurement issues.
- **Linearization Calibration:** Used to verify linearity of analyzer response across the measurement range.

---

## Technical Details  

### Calibration Timing and Phase Control  
- **Phase Duration:** Each calibration phase lasts **1 minute**.  
- **Data Capture:** Only the **last 30 seconds** of each phase are used for validation to allow stabilization.  
- **Post-Calibration Settling:** A **1-minute settling period** follows calibration, during which the system remains flagged as "in calibration mode" to external systems.  
- **Exception:** Thermo internal calibration (#3) may have different timing requirements.

### Calibration Sequence (Daily Calibration Example)  
1. **Zero Check** – Verify baseline measurement with zero gas.  
2. **NOx Low Span** – Apply low-range NOx calibration gas.  
3. **NOx High Span** – Apply high-range NOx calibration gas.  
4. **CO Low Span** – Apply low-range CO calibration gas.  
5. **CO High Span** – Apply high-range CO calibration gas.  
6. **O₂ Span** – Apply O₂ calibration gas.

### Scheduling Considerations  
- **Daily Calibration:**  
  - Runs at **06:00** daily OR **4 hours after startup**.  
  - Must start in the **first quadrant** after valid data acquisition to avoid downtime flags.  
- **Diagnostic Calibration:**  
  - Initiated by Thermo analyzer when required.  
  - Must not overlap with other calibrations to prevent conflicts.  
- **Internal Analyzer Calibration:**  
  - Triggered by analyzer for high-range or O₂ accuracy issues.  
  - Hardwired to 8864 controller for feedback monitoring.  
- **Linearization Calibration:**  
  - Performed only when required by environmental compliance staff.

---

## Best Practices  

1. **Sequence Optimization:**  
   - Perform zero checks before span checks to ensure baseline accuracy.  
   - Run NOx calibrations before CO calibrations, followed by O₂, for improved consistency.

2. **Avoid Overlap:**  
   - Ensure diagnostic and internal calibrations do not run during scheduled daily calibrations.

3. **Data Integrity:**  
   - Use only stabilized readings (last 30 seconds of phase) for calibration validation.  
   - Maintain calibration mode signal during settling to ensure proper data flagging.

4. **Regulatory Compliance:**  
   - Align calibration schedules and procedures with **EPA Part 75** requirements.  
   - Document all calibration events, including gas concentrations and analyzer responses.

5. **Maintenance Coordination:**  
   - Coordinate with environmental staff before performing linearization calibrations.  
   - Regularly verify calibration gas bottle concentrations and replace as needed.

---

## Source Attribution  

- **[Document 1]**: Provided detailed calibration gas bottle specifications and concentration values for NOx, CO, and O₂ across multiple ranges and levels.  
- **[Document 2]**: Contributed operational calibration procedures, timing requirements, sequencing preferences, scheduling logic, and integration details with Thermo analyzers and StackVision systems.

---

If you’d like, I can create a **visual flowchart** of the calibration sequence and timing to make this guide easier to follow for operators. Would you like me to add that?

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

- [[Environmental]] - - **Linearization Calibration:**  
  - Performed o...
- [[Environmental]] - **Maintenance Coordination:**  
   - Coordinate wi...


## Glossary

- **CEMS**: Continuous Emissions Monitoring System
- **8864**: Data controller platform used by engineering
