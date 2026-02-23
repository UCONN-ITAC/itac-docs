---
hide:
  - toc
---

# Rooftop Unit (RTU) Retrofits

**ARC Code(s):** 2.7232 - Replace existing HVAC unit with high efficiency model

## Overview

This measure involves retrofitting rooftop units (RTUs) with higher efficiency equipment. These upgrades significantly reduce cooling energy consumption, especially in older packaged systems operating without advanced controls.

## Required Information

- Number of RTUs
- Rated cooling capacity (Btu/hr or tons)
- Baseline and installed EER values
- ZIP code (for CDD)
- Electricity cost ($/kWh)

## Calculation Methodology

The baseline EER from the original equipment can be calculated from the product data. This is found either on the nameplate or by searching online. Due to yearly degradation, a 1% compounding decrease in efficiency per year from the date of manufacturing is assumed.

$$
\text{EER}_b = \text{EER}_{\text{true}} \times (0.99)^{\text{Years}}
$$

This same formula applies to IEER and SEER.

!!! note
    Effective full-load hours (EFLH) accounts for the fact that HVAC equipment rarely operates at full capacity. The calculation uses climate data (cooling degree days) along with design temperatures to determine equivalent full-load operating hours.

**Effective full-load hours:**

$$
\text{EFLH}_{\text{Cooling}} = \frac{\text{CDD} \times 24}{T_{\text{design,cool}} - 65}
$$

where $T_{\text{design,cool}}$ is the ASHRAE 1% cooling design dry-bulb temperature (°F) for the facility's location.

**Energy Savings:**

$$
\Delta \text{kWh}_C = \text{CAP}_C \times \left(\frac{1}{\text{EER}_b} - \frac{1}{\text{EER}_i}\right) \times \frac{1}{1000} \times \text{EFLH}_C
$$

**Peak Demand Savings:**

$$
\Delta \text{kW}_{\text{Summer}} = \frac{\Delta \text{kWh}_C}{\text{EFLH}_C} \times 0.42
$$

**Cost Savings:**

$$
\text{Annual Savings (\$)} = \Delta \text{kWh}_C \times \text{Electricity Cost}
$$

## Anticipated Costs

**Equipment:** Research high efficiency units to retrofit that have pricing available. Look for a unit that is the same size of the one that is being replaced. 

**Installation:** We assume that rigging, installation, and commissioning takes approximately 30 hours per unit. Multiply this by the standard labor rate for high-skilled labor to determine labor costs. 

!!! warning
    RTU retrofits usually qualify for utility rebates or efficiency incentives. Check with the local utility provider before finalizing cost estimates. Subtract any incentives from the implementation cost before calculating payback.

## Design Temperature Reference

The following representative design temperatures are from the ENERGY STAR County-Level Design Temperature Reference Guide (ASHRAE 2013 Handbook of Fundamentals).

| Location (representative) | 1% Cooling (°F) | Cooling ΔT |
|---|---|---|
| CT, Hartford Co. | 89 | 24 |
| CT, Fairfield Co. | 85 | 20 |
| CT, New London Co. | 85 | 20 |
| MA, Suffolk Co. (Boston) | 91 | 26 |
| RI, Providence Co. | 89 | 24 |
| NH, Hillsborough Co. | 90 | 25 |
| VT, Chittenden Co. (Burlington) | 87 | 22 |
| ME, Cumberland Co. (Portland) | 86 | 21 |
| NY, Albany Co. | 90 | 25 |
| NY, New York Co. (Manhattan) | 92 | 27 |

