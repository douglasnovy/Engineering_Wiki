---
title: Calibration
consolidated: true
sources: 2
conflicts: 3
confidence: 0.60
generated: ['data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationActivityBottlesxlsx_4c681ef1.md', 'data\\extracted\\ui_generated_1758664533\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationsActivityCustomerdocx_242035cd.md']  # This would be a timestamp
---

## Title  
**Calibration Procedures for Dual-Range NOx and CO Systems with O₂ Diluent in StackVision**

---

## Overview  
Calibration is a critical process for ensuring the accuracy and reliability of emissions monitoring systems, particularly those operating under regulatory frameworks such as U.S. EPA Part 75. This consolidated guide outlines calibration procedures for a dual-range NOx and CO system using O₂ as a diluent, integrated with StackVision and Thermo analyzers. It combines calibration gas specifications with operational scheduling and procedural requirements to support compliance, minimize downtime, and maintain measurement integrity.

---

## Key Concepts  

### 1. **Dual-Range Measurement**  
- **NOx**: Measured in both high and low ranges to accommodate varying emission levels.  
- **CO**: Also measured in high and low ranges for flexibility in monitoring.  
- **O₂**: Used as a diluent gas and measured across multiple span levels.

### 2. **Calibration Phases**  
- Each calibration consists of multiple phases (zero, low span, high span) for each gas.  
- Phase duration: **1 minute**, with only the **last 30 seconds** of data used for evaluation.  
- Post-calibration settling time: **1 minute**, during which the system remains flagged as "in calibration mode."

### 3. **Thermo Analyzer Integration**  
- Thermo analyzers can initiate diagnostic or internal calibrations.  
- These calibrations are hardwired to the 8864 controller, which manages calibration mode signaling and feedback.

### 4. **Regulatory Context**  
- NOx and O₂ measurements are reported under **Part 75** requirements.  
- Calibration scheduling and execution must avoid downtime and ensure valid data capture.

---

## Technical Details  

### Calibration Gas Specifications (from Document 1)  
| Gas | Range | Concentration |
|-----|-------|---------------|
| NOx | High Range High Level | 900 ppm |
| NOx | High Range Mid Level  | 500 ppm |
| NOx | High Range Low Level  | 200 ppm |
| NOx | Low Range High Level  | 90 ppm  |
| CO  | High Range High Level | 950 ppm |
| CO  | Low Range High Level  | 95 ppm  |
| O₂  | High Level            | 0.22    |
| O₂  | Mid Level             | 0.16    |
| O₂  | Low Level             | 0.09    |

### Calibration Types (from Document 2)  
1. **Daily Calibration**  
   - Runs at **06:00** daily or **4 hours after startup**.  
   - Must start in the first quadrant after valid data capture to avoid downtime.  
   - Sequence: Zero → Low NOx span → High NOx span → Low CO span → High CO span → O₂ span.  
   - This sequence improves result consistency.

2. **Diagnostic Calibration (Thermo-initiated)**  
   - Mimics daily calibration but triggered outside the normal schedule.  
   - Must not overlap with other calibrations to prevent conflicts.

3. **Thermo Internal Calibration**  
   - Addresses issues with high ranges and O₂ measurements.  
   - Initiated by Thermo analyzer as needed.  
   - Feedback is read by the 8864 controller.

4. **Linearization Calibration**  
   - Required only for specific environmental compliance needs.  
   - Frequency determined by environmental team.

---

## Best Practices  

1. **Scheduling**  
   - Align calibrations to avoid overlap between daily, diagnostic, and internal calibrations.  
   - Ensure calibrations occur after valid data capture to prevent downtime.

2. **Phase Timing**  
   - Maintain consistent phase durations (1 minute) and data capture windows (last 30 seconds).  
   - Allow adequate settling time post-calibration while keeping calibration mode active.

3. **Sequence Optimization**  
   - Follow the recommended order (zero → NOx spans → CO spans → O₂ span) for improved accuracy.  
   - Verify calibration gas concentrations match specifications.

4. **Integration Management**  
   - Monitor Thermo analyzer signals to coordinate with StackVision and 8864 controller logic.  
   - Prevent simultaneous calibrations to avoid data conflicts.

5. **Regulatory Compliance**  
   - Document calibration events and results for Part 75 reporting.  
   - Maintain calibration gas certificates and ensure traceability.

---

## Source Attribution  

- **Document 1**: Provided calibration gas concentration specifications for NOx, CO, and O₂ across multiple ranges and levels.  
- **Document 2**: Detailed operational calibration procedures, scheduling requirements, phase timing, integration with Thermo analyzers, and regulatory context for Part 75 reporting.

---

If you’d like, I can also create a **calibration scheduling diagram** that visually maps daily, diagnostic, and internal calibrations to avoid conflicts. Would you like me to add that?

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

- [[Environmental]] - **Linearization Calibration**  
   - Required only...
- [[Environmental]] - - Frequency determined by environmental team...


## Glossary

- **8864**: Data controller platform used by engineering
