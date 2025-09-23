---
title: Environmental
consolidated: true
sources: 6
conflicts: 0
confidence: 0.80
generated: ['data\\extracted\\set_004\\engineering_white_papers_WhitePapers_AmmoniaSlip_AmmoniaSlipCalculationxlsx_7514d17d.md', 'data\\extracted\\set_004\\engineering_white_papers_WhitePapers_AmmoniaSlip_EmpireNH3slipxlsx_7399a0a4.md', 'data\\extracted\\set_004\\engineering_white_papers_WhitePapers_AmmoniaSlip_ESCAmmoniaSlipCalculationxls_cbc4be89.md', 'data\\extracted\\set_004\\engineering_white_papers_WhitePapers_AmmoniaSlip_NH3slipcalculationsxls_692ae2a3.md', 'data\\extracted\\set_004\\engineering_white_papers_WhitePapers_AmmoniaSlip_NH3TONSfromNH3PPM111210Rev1xlsx_ee61d34a.md', 'data\\extracted\\set_004\\engineering_white_papers_WhitePapers_AmmoniaSlip_NH3TONSfromNH3PPMxlsx_4a7890af.md']  # This would be a timestamp
---

# **Ammonia Slip Calculation & Compliance Guide**  
*A comprehensive, interconnected reference for engineers, operators, and compliance specialists*

---

## **Overview**
Ammonia slip refers to the amount of unreacted ammonia (NH₃) emitted from a Selective Catalytic Reduction (SCR) system after NOx reduction. Accurate calculation and monitoring are critical for **regulatory compliance**, **emissions reporting**, and **process optimization**.

This guide consolidates multiple industry-standard calculation methods, integrates practical spreadsheet tools, and provides cross-links to related topics such as **SCR operation**, **NOx measurement**, and **CEMS data handling**.  

**Navigation Tip:**  
- Start with **Basic Concepts** if you are new to ammonia slip.  
- Jump to **Calculation Methods** for formulas and worked examples.  
- Use **Integrated Tools** to perform real-time calculations.  
- Explore **Advanced Topics** for oxygen correction, compliance testing, and tonnage conversions.

---

## **1. Basic Concepts**

### **What is Ammonia Slip?**
Ammonia slip occurs when injected ammonia (or urea-derived ammonia) passes through the SCR catalyst without reacting with NOx. It is typically measured in **parts per million by volume (ppmv)** at a reference oxygen concentration (often 15% O₂).

**Why it matters:**
- **Environmental compliance:** Regulatory agencies (e.g., TCEQ, EPA) set limits on ammonia slip.
- **Operational efficiency:** Excess slip indicates over-injection or catalyst performance issues.
- **Safety:** High ammonia emissions can be hazardous.

**Related Topics:**
- [Selective Catalytic Reduction (SCR) Fundamentals](SCR_Fundamentals.md) – How SCR systems work and why ammonia slip occurs.
- [NOx Measurement & Correction](NOx_Measurement.md) – Understanding inlet/outlet NOx readings and oxygen correction.
- [Continuous Emissions Monitoring Systems (CEMS)](CEMS_Overview.md) – How ammonia slip data is collected and processed.

---

## **2. Core Calculation Methods**

Multiple calculation approaches exist, depending on regulatory requirements and plant instrumentation. The following are the most common:

### **2.1 ESC Standard Equation**
From *ESC Ammonia Slip Calculation.xls*:

\[
As = \left[ A - \frac{B \cdot C}{1{,}000{,}000} \right] \cdot \left( \frac{1{,}000{,}000}{B} \cdot D \right) \cdot \left( \frac{20.9 - CF}{20.9 - O_2} \right)
\]

Where:  
- **As** = Ammonia Slip (ppmv @ 15% O₂)  
- **A** = NH₃ Injection Rate (lb/hr) ÷ 17 (lb/lb-mol) × %NH₃ in reagent  
- **B** = Dry Exhaust Gas Flow Rate (scfh) ÷ 385.5 (scf/lb-mol)  
- **C** = ΔNOx across catalyst (ppmv @ 15% O₂)  
- **D** = Correction factor (measured/calculated slip ratio)  
- **CF** = O₂ correction factor  
- **O₂** = Measured stack oxygen concentration (%)  

**Tool Integration:**  
Use the **[ESC Ammonia Slip Calculator Spreadsheet](ESC_Ammonia_Slip_Calculation.xls)** to input CEMS readings and automatically compute slip values with oxygen correction. This tool is ideal for **annual compliance testing** and **daily operational checks**.

---

### **2.2 TCEQ Equation (§117.8130)**
From *NH3 slip calculations.xls*:

\[
NH_3 = \left[ \frac{a}{b} \times 10^6 - c \right] \times d
\]

Where:  
- **a** = NH₃ injection rate (lb/hr) ÷ 17 lb/lb-mol  
- **b** = Dry exhaust flow rate (lb/hr) ÷ 29 lb/lb-mol  
- **c** = ΔNOx across catalyst (ppmv)  
- **d** = Correction factor  

**Variation:** Modified TCEQ equation includes oxygen correction:  
\[
NH_3 @ 15\% O_2 = \left( \left[ \frac{a}{b} \times 10^6 - c \right] \times d \right) \times \frac{5.9}{20.9 - O_2}
\]

**Tool Integration:**  
Use the **[NH3 Slip Calculations Spreadsheet](NH3_slip_calculations.xls)** for TCEQ-compliant calculations, including worked examples for multiple plants.

---

### **2.3 Empire Method**
From *Empire NH3slip.xlsx*:

\[
NH3SLIP = \frac{NH3}{17} - \left( \frac{DRYGAS}{29} \cdot \frac{NOX_{in} - NOX_{out}}{1{,}000{,}000} \right) \cdot \frac{1{,}000{,}000}{DRYGAS/29}
\]

Includes adjustment for %NH₃ in slurry.

**Tool Integration:**  
The **[Empire NH3 Slip Calculator](Empire_NH3slip.xlsx)** is tailored for plants using slurry injection systems.

---

## **3. Oxygen Correction**

Most ammonia slip limits are specified at a reference oxygen concentration (commonly 15% O₂). If measured O₂ differs, correction is required:

\[
Correction\ Factor = \frac{20.9 - CF}{20.9 - O_2}
\]

**Related Topics:**
- [Oxygen Correction in Emissions Reporting](Oxygen_Correction.md) – Why and how oxygen correction is applied.
- [CEMS O₂ Measurement Best Practices](CEMS_O2_Measurement.md) – Ensuring accurate oxygen readings.

---

## **4. Converting NH₃ ppm to Tons per Year**

From *NH3TONS from NH3PPM.xlsx* and *NH3TONS from NH3PPM 111210 Rev1.xlsx*:

**Step 1:** Calculate stack flow rate (Qs) from fuel flow and F-factor.  
**Step 2:** Convert NH₃ ppm to lb/hr:  
\[
E_{lb/hr} = \frac{NH_3\ ppm \times MW_{NH_3} \times Q_s}{1{,}000{,}000 \times IdealGasCF}
\]
**Step 3:** Convert lb/hr to tons/year:  
\[
NH3TONS = E_{lb/hr} \times \frac{Hours\ of\ Operation}{2000}
\]

**Tool Integration:**  
Use the **[NH3 Tons from NH3 PPM Calculator](NH3TONS_from_NH3PPM.xlsx)** to quickly estimate annual emissions for reporting.

**Related Topics:**
- [Emission Inventory Reporting](Emission_Inventory.md) – How ammonia slip tonnage fits into regulatory submissions.
- [Ideal Gas Conversion Factors](Ideal_Gas_Conversion.md) – Understanding SCF/lb-mol constants.

---

## **5. Compliance Testing & Correction Factors**

Annual compliance testing involves:
- Measuring actual ammonia slip via stack sampling.
- Comparing measured slip to calculated slip.
- Deriving a **correction factor (D)** for ongoing calculations.

**Best Practice:**  
Maintain historical correction factors and update annually to reflect catalyst aging and process changes.

**Related Topics:**
- [Compliance Test Procedures](Compliance_Testing.md) – Step-by-step guide for ammonia slip verification.
- [Catalyst Performance Monitoring](Catalyst_Performance.md) – How slip trends indicate catalyst health.

---

## **6. Integrated Tools Library**

| Tool Name | Purpose | When to Use |
|-----------|---------|-------------|
| **ESC Ammonia Slip Calculator** | Computes slip with oxygen correction using ESC method | Annual compliance, daily checks |
| **NH3 Slip Calculations Spreadsheet** | TCEQ-compliant slip calculation | Texas regulatory reporting |
| **Empire NH3 Slip Calculator** | Slip calculation for slurry injection systems | Plants with wet reagent |
| **NH3 Tons from NH3 PPM Calculator** | Converts ppm to annual tonnage | Emission inventory reporting |
| **Ideal Gas Conversion Factor Sheet** | Reference for SCF/lb-mol constants | Any gas flow conversion |

---

## **See Also**
- [SCR Fundamentals](SCR_Fundamentals.md) – Understanding catalyst operation and ammonia injection.
- [NOx Measurement & Correction](NOx_Measurement.md) – How NOx readings affect slip calculations.
- [CEMS Overview](CEMS_Overview.md) – Continuous monitoring systems for emissions.
- [Oxygen Correction in Emissions Reporting](Oxygen_Correction.md) – Adjusting readings to reference oxygen.
- [Emission Inventory Reporting](Emission_Inventory.md) – Annual reporting requirements.
- [Ideal Gas Conversion Factors](Ideal_Gas_Conversion.md) – Gas law constants for flow calculations.
- [Catalyst Performance Monitoring](Catalyst_Performance.md) – Using slip data to assess catalyst health.
- [Compliance Test Procedures](Compliance_Testing.md) – How to verify ammonia slip compliance.

---

**Breadcrumb Navigation:**  
Home → Emissions Control → SCR Systems → Ammonia Slip Calculation & Compliance Guide

---

✅ **Next Step Recommendation:**  
If you are preparing for a compliance test, start with the **ESC Ammonia Slip Calculator** and review the **Compliance Testing** section. If you need to report annual emissions, use the **NH3 Tons from NH3 PPM Calculator** and cross-check with your CEMS data.

---

Do you want me to **create linked subpages** for each calculation method so users can click directly from the overview to a deep-dive page with worked examples and downloadable tools? That would make this wiki truly navigable and interconnected.

## Glossary

- **CEMS**: Continuous Emissions Monitoring System
