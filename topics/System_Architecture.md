---
title: System_Architecture
consolidated: true
sources: 3
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ControlCharts_CO2controlchartSVConfigurationdocx_47da83fd.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_Regulations_SubpartTTTT-CO2MassEmissions12MonthAverageGuidelinesRev11-01-21pdf_91bcb2f5.md', 'data\\extracted\\set_whitepapers\\engineering_white_papers_WhitePapers_ServerMigration_TCP-IPportsusedbyaStackVisionsystempdf_cf196824.md']  # This would be a timestamp
---

## Title
**CO₂ Control Chart Configuration, Regulatory Compliance, and StackVision Network Port Requirements**

---

## Overview
This consolidated guide provides a comprehensive reference for configuring CO₂ control charts in StackVision, ensuring compliance with Subpart TTTT 12-month CO₂ mass emission guidelines, and understanding TCP/IP port usage for StackVision systems.  
It integrates configuration procedures, regulatory calculation rules, and network communication specifications to support accurate emissions reporting, operational efficiency, and secure system connectivity.

---

## Key Concepts

### Control Charts
Control charts in StackVision are used to monitor and analyze CO₂ emissions data against load bins, enabling performance tracking and compliance verification.

### Subpart TTTT Compliance
U.S. EPA regulations under Subpart TTTT require facilities to calculate and report 12-month average CO₂ mass emissions on an output basis (lb/MWh or kg/MWh), ensuring data validity and completeness.

### StackVision Network Architecture
StackVision uses specific TCP/IP ports for communication between servers, clients, controllers, and external data sources. Proper configuration of these ports is essential for data integrity and system security.

---

## Technical Details

### 1. CO₂ Control Chart Configuration in StackVision
To enable and correctly configure CO₂ control charts:

1. **Enable Load Bin Calculations**  
   - Navigate to **Configuration → StackStudio → Plant-Sources-Parameters**.  
   - Select the desired parameter (e.g., CO₂ or backup CO₂).  
   - On the **Part 75 Settings** tab, check:
     - *Parameter Daily Record?*
     - *Load Range Enabled?*

2. **Configure Daily ProcessNow Sequence**  
   - Go to **ProcessNow → Sequences**.  
   - Select the daily sequence from the pick list.  
   - Ensure **Task PDR** is enabled.  
   - If the *Parameters* field is blank, all parameters are included; otherwise, verify the desired parameter is checked.

3. **Apply Changes**  
   - Click the *Apply* icon to update the StackVision Server.

4. **Verify Load Bin Selection**  
   - In **DataLab**, add the *Load Range* field from **Fields → Part 75** to confirm the correct bin number.

---

### 2. Subpart TTTT – 12-Month CO₂ Mass Emission Guidelines

**Hourly Data Rules:**
- Use hourly fuel flow data to calculate CO₂ lbs.
- Exclude hours where:
  - Load is missing/invalid.
  - Fuel flow is missing, invalid, or substituted under Part 75 missing data rules.
  - CO₂ lbs is missing, invalid, or substituted.
- For no-load hours, use load = 0 with actual CO₂ lbs.
- Include startup and shutdown data.

**12-Month Rolling Average:**
- Always include 12 operating months; if a month is non-operating, look back further to maintain 12 months.
- Operating month = any month with fuel combustion.

**Parameters:**
- CO₂#/MWh and CO₂KGMWh typically configured.
- Many permits specify ≤ 1000 lb/MWh.
- Annual Energy Sold and Annual Potential Electric Output must be entered manually in the EDR XML file (not calculated/stored in StackVision).

**Configuration Formulas:**
- **CO₂LBS** = CO₂T/HR × 2000 × UNITOPHR#100  
  (No invalidation logic based on load; load never invalid.)
- **LOADMWH** = (UNITLOAD × UNITOPHR#100) + (CO₂LBS × 0)  
  (Invalid if CO₂ is invalid; excluded from daily/monthly totals.)
- **UNITOPHR** = OPTIME parameter for Group 0.

---

### 3. TCP/IP Ports Used by StackVision Systems

**StackVision Server – Inbound Connections:**
- SQL Reporting Services (from SV Client)
- Data Link from FleetVision
- OPC/PI (if installed)
- StackVision Client Service
- Controller Emulation from SV Client

**StackVision Server – Outbound Connections:**
- Controller file transfer: ports **8832** or **8864** (to Data Controller)
- Controller Emulation: **8864** only
- Controller Configuration Compare: **8864** only
- SQL Server (if remote)
- Controller Polling: **8832** or **8864**

**StackVision Client – Outbound Connections:**
- SQL Reporting Services (to SQL Server)
- StackVision Client Service (to SV Server)
- Controller Emulation (to SV Server)

**Data Controller (8832) – Inbound Ports:**
- File Transfer and Controller Emulation (specific port assignments per configuration)

---

## Best Practices

1. **Configuration Integrity**
   - Always verify parameter inclusion in PDR sequences.
   - Confirm load bin assignments before running control chart reports.

2. **Regulatory Compliance**
   - Maintain strict adherence to Subpart TTTT data validity rules.
   - Regularly audit hourly data for missing or substituted values.
   - Keep manual EDR XML entries up to date for annual metrics.

3. **Network Security & Reliability**
   - Document and secure all TCP/IP port configurations.
   - Restrict inbound connections to trusted sources.
   - Monitor port activity to detect unauthorized access.

4. **Data Validation**
   - Use DataLab to cross-check load ranges and CO₂ calculations.
   - Implement automated checks for invalid or missing data before reporting.

---

## Source Attribution

- **[Document 1]**: Provided detailed procedures for enabling and configuring CO₂ control charts in StackVision, including load bin setup, PDR sequence configuration, and DataLab verification.
- **[Document 2]**: Outlined Subpart TTTT regulatory guidelines for calculating 12-month CO₂ mass emissions averages, including hourly data validity rules, parameter configurations, and compliance thresholds.
- **[Document 3]**: Listed TCP/IP port usage for StackVision servers, clients, and controllers, detailing inbound/outbound communication paths essential for system operation and security.

---

Would you like me to also create a **visual configuration workflow diagram** that integrates CO₂ control chart setup, Subpart TTTT compliance checks, and network port mapping? That would make this guide even more actionable.

## Glossary

- **8864**: Data controller platform used by engineering
