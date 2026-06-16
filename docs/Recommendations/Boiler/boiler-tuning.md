---
hide:
  - toc
---

# Boiler Tuning

Boiler tuning (combustion tuning) aligns fuel and air delivery to achieve complete combustion with minimal excess air. Proper tuning reduces stack losses, lowers fuel consumption, and reduces emissions.

## Summary

Boiler tuning targets combustion efficiency improvements of 1–5 percentage points for poorly tuned systems. Typical measures include adjusting fuel/air ratio, optimizing burner controls, repairing leaks in air/fuel delivery, and verifying control setpoints.

## Current Practices and Observations

- Operators often accept factory burner settings or previous tuning without verification.
- Common issues: excessive excess air, fouled heat transfer surfaces, leaking dampers, poor control response, and incorrect stack temperature setpoints.

## Recommended Action

- Measure current stack temperature, O2 (or CO2), and flue gas composition.
- Reduce excess air to the minimum safe level while keeping CO/CO2 and flame stability within safe limits.
- Clean heat transfer surfaces and inspect boiler controls and airflow seals.
- Implement a scheduled tuning and maintenance program (annually or after major service).

## Savings Calculation

Estimate annual fuel savings using a simple stack-loss approach. Baseline and tuned combustion efficiencies are used to calculate fuel reduction:

$$\Delta kBtu = \frac{Annual\ Fuel_{baseline} \times (\eta_{tuned} - \eta_{baseline})}{\eta_{baseline}}$$

Where:
- $Annual\ Fuel_{baseline}$ = baseline annual fuel consumption (kBtu/yr)
- $\eta_{baseline}$ = baseline combustion efficiency (fraction)
- $\eta_{tuned}$ = post-tuning combustion efficiency (fraction)

After computing $\Delta kBtu$, convert to fuel cost savings:

$$Savings\ ($/yr) = \Delta kBtu \times Fuel\ Price\ ($/kBtu)$$

Where typical inputs are:
- Baseline combustion efficiency: 75%–85% (poorly tuned boilers near 70–75%)
- Tuned combustion efficiency: baseline + 1–5 percentage points
- Fuel price: site-specific (e.g., $/MMBtu or $/therm)

### Example

- Baseline fuel = 10,000 MMBtu/year (10,000,000 kBtu/yr)
- $\eta_{baseline} = 0.80$, $\eta_{tuned} = 0.84$ (4 percentage-point improvement)

$$\Delta kBtu = \frac{10{,}000{,}000 \times (0.84 - 0.80)}{0.80} = 500{,}000\ kBtu/yr$$

If fuel price = $0.01/kBtu (i.e., $10/MMBtu):

$$Savings = 500{,}000 \times 0.01 = $5{,}000/yr$$

## Anticipated Costs

- Typical boiler tune-up cost: $300–$1,200 depending on boiler size and service complexity.
- Additional costs for repairs or surface cleaning may apply (variable).

## Report Requirements

- Document baseline and tuned stack temperatures, O2/CO2 readings, and any measured CO values.
- Note the measured combustion efficiencies used and the assumed fuel price.
- Provide before/after photos or instrumentation screenshots if available.

## References and Notes

- Maintain safe combustion limits; do not reduce excess air below manufacturer recommendations.
- Use qualified service personnel for tuning and safety checks.
