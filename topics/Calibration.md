---
title: Calibration
consolidated: true
sources: 2
conflicts: 2
confidence: 0.60
generated: ['data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationActivityBottlesxlsx_4c681ef1.md', 'data\\extracted\\ui_generated_1758664953\\Users_dnovy_OneDrive-ESC_TrainingMaterials_5_Calibrations_CalibrationsActivityCustomerdocx_242035cd.md']  # This would be a timestamp
---

# Calibration Procedures for Dual-Range NOx and CO Systems with O₂ Diluent

## Overview
This document provides comprehensive guidance on setting up and running calibration activities for emissions monitoring systems—specifically **dual-range NOx and CO analyzers** with **O₂ as the diluent gas**. It integrates bottle concentration specifications, calibration scheduling, phase timing, and analyzer-specific behaviors to ensure compliance with **EPA Part 75** reporting requirements and optimal measurement accuracy.

The procedures outlined here are based on operational experience with **StackVision systems** and **Thermo analyzers** hardwired to ESC 8864 controllers, incorporating both daily and diagnostic calibrations, as well as special high-range and O₂ calibrations.

---

## Key Concepts

### Calibration Types
1. **Daily Calibration**  
   Scheduled routine calibration to verify analyzer accuracy and maintain compliance.
   
2. **Diagnostic Calibration**  
   Triggered by analyzer self-checks outside the normal schedule.
   
3. **Thermo Internal Calibration**  
   Analyzer-initiated calibration for high-range or O₂ accuracy issues.
   
4. **Linearization Calibration**  
   Performed only when required by environmental compliance staff.

### Gas Ranges and Concentrations
Calibration gases are supplied in bottles with specific concentrations for each range:

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

---

## Technical Details

### Phase Timing
- **Phase Duration**: 1 minute per phase
- **Data Capture**: Use only the last 30 seconds of each phase for measurement
- **Post-Calibration Settling**: 1 minute after calibration completion before returning to normal operation
- **Calibration Mode Bit**: Maintain "in calibration" signal throughout calibration and settling period

### Daily Calibration Sequence
1. **Zero Check** – Establish baseline
2. **Low NOx Span** – Verify low-range NOx accuracy
3. **High NOx Span** – Verify high-range NOx accuracy
4. **Low CO Span** – Verify low-range CO accuracy
5. **High CO Span** – Verify high-range CO accuracy
6. **O₂ Span** – Verify O₂ measurement accuracy

**Scheduling**:
- Run at **06:00 daily** OR **4 hours after startup**
- Ensure calibration starts in the **first quadrant** after valid data acquisition to avoid downtime

### Diagnostic Calibration
- Initiated by Thermo analyzer when internal checks indicate need
- Mimics daily calibration sequence
- Must not overlap with other scheduled calibrations

### Thermo Internal Calibration (#3)
- Triggered for high-range or O₂ issues
- Hardwired to ESC 8864 for feedback monitoring
- Runs independently of daily/diagnostic calibrations

### Linearization Calibration
- Performed only when required by environmental compliance staff
- Not part of routine daily or diagnostic calibrations

---

## Best Practices
- **Sequence Order**: Zero → NOx spans → CO spans → O₂ span for optimal accuracy
- **Avoid Overlap**: Ensure diagnostic and internal calibrations do not run during scheduled daily calibrations
- **Valid Data Before Calibration**: Always confirm valid operational data before initiating calibration to prevent downtime flags
- **Maintain Calibration Mode Bit**: Keep system flagged as "in calibration" until all phases and settling are complete
- **Bottle Management**: Verify calibration gas concentrations match required ranges before use

---

## Implementation Example

**Scenario**:  
A plant starts up at 02:00.  
- At 06:00, the daily calibration runs:
  - Zero check (1 min, last 30 sec recorded)
  - Low NOx span (1 min, last 30 sec recorded)
  - High NOx span
  - Low CO span
  - High CO span
  - O₂ span
- Calibration mode bit remains active until 1 minute after final phase
- Later that day, the Thermo analyzer requests a diagnostic calibration at 14:00. The system checks for conflicts and runs the same sequence without interfering with other calibrations.

---

## Troubleshooting

| Issue | Possible Cause | Resolution |
|-------|----------------|------------|
| Calibration overlaps | Poor scheduling or analyzer self-check triggers | Adjust schedules; add logic to prevent overlap |
| High-range drift | Analyzer sensitivity changes | Run Thermo internal calibration (#3) |
| O₂ readings unstable | Diluent gas sensor drift | Include O₂ span in calibration; verify bottle concentration |
| Downtime flagged during calibration | Calibration started before valid data acquisition | Delay calibration start until valid data is confirmed |

---

## Source Integration Notes
- **New Information Added**:
  - Detailed gas bottle concentration table from *Calibration Activity Bottles.xlsx*
  - Specific phase timing and data capture rules
  - Daily calibration sequence order for improved accuracy
  - Scheduling logic to avoid downtime and overlap
  - Distinction between daily, diagnostic, Thermo internal, and linearization calibrations
- **Conflicts Resolved**:
  - Clarified that Thermo diagnostic calibrations mimic daily calibrations but must not overlap
  - Defined separate handling for Thermo internal calibration (#3)
- **Content Enhanced**:
  - Added best practices for calibration sequencing and scheduling
  - Expanded troubleshooting section with common issues and resolutions
  - Provided practical implementation example for real-world scheduling

---

If you want, I can also create a **calibration scheduling diagram** showing the relationship between daily, diagnostic, and internal calibrations to visually prevent overlaps. Would you like me to add that?