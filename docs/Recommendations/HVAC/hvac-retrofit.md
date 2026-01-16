# Install Rooftop Unit (RTU) Retrofits

**ARC Code(s):** 2.7232 - Replace existing HVAC unit with high efficiency model

## Overview

This measure involves retrofitting rooftop units (RTUs) with higher efficiency equipment. These upgrades significantly reduce both heating and cooling energy consumption, especially in older packaged systems operating without advanced controls.

## Required Information

- Number of RTUs
- Rated cooling capacity (Btu/hr or tons)
- Rated heating capacity (Btu/hr)
- Baseline and installed efficiency values: SEER, IEER, EER, HSFF, COP
- ZIP code (for CDD and HDD)
- Electricity cost ($/kWh)

## Calculation Methodology

The baseline EER from the original equipment can be calculated from the product data. This is found either on the nameplate or by searching online. Due to yearly degradation, a 1% compounding decrease in efficiency per year from the date of manufacturing is assumed.

$$
\text{EER}_b = \text{EER}_{\text{true}} \times (0.99)^{\text{Years}}
$$

This same formula applies to IEER and SEER.

!!! note
    Effective full-load hours (EFLH) accounts for the fact that HVAC equipment rarely operates at full capacity. The calculation uses climate data (cooling degree days and heating degree days) along with equipment efficiency ratings to determine equivalent full-load operating hours.

**Effective full-load hours:**

$$
\text{EFLH}_{\text{Cooling}} = \frac{(\text{CDD} / 33.5) \times 24}{\text{IEER}}
$$

$$
\text{EFLH}_{\text{Heating}} = \frac{(\text{HDD} / 33.5) \times 24}{\text{HSFF}}
$$

**Energy Savings:**

$$
\text{Cooling Energy Savings (kWh)} = \text{Capacity}_{\text{cooling}} \times \text{EFLH}_{\text{Cooling}} \times \left(\frac{1}{\text{EER}_b} - \frac{1}{\text{EER}_{\text{new}}}\right)
$$

$$
\text{Heating Energy Savings (kWh)} = \text{Capacity}_{\text{heating}} \times \text{EFLH}_{\text{Heating}} \times \left(\frac{1}{\text{COP}_b} - \frac{1}{\text{COP}_{\text{new}}}\right)
$$

**Cost Savings:**

$$
\text{Annual Savings (\$)} = (\text{Cooling Savings} + \text{Heating Savings}) \times \text{Electricity Cost}
$$

## Anticipated Costs

Implementation costs include equipment purchase, installation labor, removal of existing units, and any necessary electrical or structural modifications. Obtain quotes from HVAC contractors for accurate pricing.

!!! warning
    RTU retrofits may qualify for utility rebates or efficiency incentives. Check with the local utility provider before finalizing cost estimates. Subtract any incentives from the implementation cost before calculating payback.

