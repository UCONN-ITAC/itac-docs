# Upgrade to High Efficiency Motors

Standard efficiency motors waste significant energy as heat during operation. Upgrading to NEMA Premium high efficiency motors reduces electrical consumption, particularly in motors that run continuously or for long hours on constant loads like pumps, fans, and compressors.

**ARC Code(s):** 2.4133

## Savings Calculation

Energy savings from high efficiency motors result from reduced electrical losses in the windings, magnetic core, and mechanical components. The savings depend on three factors: the efficiency difference between the baseline and new motor, the motor's rated horsepower, and annual operating hours.

The calculation compares the electrical input power required by the existing standard efficiency motor versus the input power required by a NEMA Premium motor to deliver the same mechanical output. The difference in input power, multiplied by annual operating hours, yields the annual energy savings.

Motor input power is calculated as:

$$
P_{\text{shaft}} = P_\text{input} \times \eta
$$

Where $P_{\text{shaft}}$ is the mechanical power output (HP converted to kW using 0.746 kW/HP) and $\eta$ is motor efficiency as a decimal.

Annual energy savings are calculated as:

$$
E_{\text{savings}} = \left(\frac{P_{\text{shaft}}}{\eta_{\text{baseline}}} - \frac{P_{\text{shaft}}}{\eta_{\text{premium}}}\right) \times \text{Operating Hours}
$$

Power savings (kW) represent the reduction in electrical demand:

$$
P_{\text{savings}} = \frac{P_{\text{shaft}}}{\eta_{\text{baseline}}} - \frac{P_{\text{shaft}}}{\eta_{\text{premium}}}
$$

Annual cost savings are calculated by multiplying the energy savings by the facility's blended electricity rate ($/kWh).

Important assumptions to state in the analysis:

- Motor operates at or near its rated capacity (load factor >75%)

- Operating hours should be measured or estimated based on production schedules

- Baseline efficiency should be obtained from motor nameplate or manufacturer data

- NEMA Premium efficiency values can be found in NEMA MG-1 Table 12-12 or manufacturer specifications

- For older motors (>15 years), consider additional degradation: reduce nameplate efficiency by 1% per year of operation

!!! warning "Load Factor Verification"

    High efficiency motor upgrades only make economic sense when motors run at high load factors (>75% of rated capacity) for significant hours per year. Motors running at low load factors (<50%) should first be evaluated for right-sizing rather than efficiency upgrades. Verify actual operating current against nameplate full load amps before recommending this measure.

## Anticipated Costs

Equipment costs for NEMA Premium motors vary with horsepower rating and enclosure type (ODP vs TEFC). Prices depend on vendor, voltage, speed, and mounting configuration. Obtain quotes from local suppliers for project-specific pricing.

Installation labor includes motor removal, new motor installation, alignment (for direct-coupled applications), and electrical connections. For belt-driven applications, sheave installation and belt tensioning are required. Budget 2-4 hours of electrician labor for motors under 25 HP, 4-8 hours for larger motors. If the motor is difficult to access or requires rigging equipment, add additional labor costs.

Most utility energy efficiency programs offer prescriptive rebates for qualifying motor replacements. Typical incentive structures include:

- Early retirement incentives: Replace a working standard efficiency motor before failure (higher rebates)

- Replace-on-burnout incentives: Replace a failed motor with high efficiency model (lower rebates)

Incentives are subject to utility-specific eligibility requirements, which may include minimum efficiency ratings, minimum horsepower thresholds, and minimum annual operating hours. Check with the local utility provider for current incentive offerings and verify eligibility before finalizing cost estimates.

Simple payback periods for high efficiency motor upgrades typically range from 2-5 years for early retirement applications and less than 2 years for replace-on-burnout scenarios after utility incentives. Motors running more than 4,000 hours per year generally show better economics than those with intermittent operation.

## Report Requirements

In addition to the [typical report requirements](../how-to.md) and the recommendation-specific savings and costs, the recommendation should include a table documenting all motors being replaced. The table should follow this structure:

- **Column 1:** Motor ID or location description

- **Column 2:** Rated horsepower (HP)

- **Column 3:** Baseline efficiency (%)

- **Column 4:** Premium efficiency (%)

- **Column 5:** Annual operating hours (hrs/yr)

- **Column 6:** Annual energy savings (kWh/yr)

- **Column 7:** Annual power savings (kW)

- **Column 8:** Annual cost savings ($/yr)

If multiple motors are being replaced, include a totals row at the bottom.

```latex
\begin{table}[H]
\centering
\caption{High Efficiency Motor Upgrade Summary}
\label{tab:high-eff-motors}
\begin{tabular}{lccccccc}
\toprule
Motor Location & HP & Baseline Eff. (\%) & Premium Eff. (\%) & Operating Hours & Energy Savings & Power Savings & Cost Savings \\
 & & & & (hrs/yr) & (kWh/yr) & (kW) & (\$/yr) \\
\midrule
Pump 1 &  &  &  &  &  &  &  \\
Fan 3 &  &  &  &  &  &  &  \\
Compressor 2 &  &  &  &  &  &  &  \\
\midrule
\textbf{Total} & \textbf{} & \textbf{--} & \textbf{--} & \textbf{--} & \textbf{} & \textbf{} & \textbf{} \\
\bottomrule
\end{tabular}
\end{table}
```


