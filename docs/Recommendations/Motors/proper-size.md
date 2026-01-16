# Replace Oversized Motors with Properly-Sized Units

Oversized motors running at partial load operate at reduced efficiency and power factor, wasting electrical energy compared to properly-sized motors. When replacing failed motors or upgrading equipment, selecting motors sized appropriately for the actual load reduces both energy consumption and demand charges while improving power factor.

**ARC Code(s):** X.XXXX

## Savings Calculation

Energy savings from proper motor sizing result from operating a motor closer to its optimal load point. Electric motors achieve peak efficiency between 75% and 100% of rated capacity. Motors operating below 50% of rated capacity suffer from reduced efficiency, poor power factor, and excessive magnetizing current that provides no useful work.

Identifying oversized motors requires comparing actual operating current to nameplate full load amps (FLA). Motors consistently running at less than 50% of FLA are candidates for downsizing. However, the economic analysis must consider several factors: the efficiency of the existing oversized motor at its actual operating point, the efficiency of a properly-sized new motor at its higher load factor, and the effect on power factor for facilities subject to demand charges.

Actual load factor is calculated as:

$$
\text{Load Factor} = \frac{I_{\text{actual}}}{I_{\text{FLA}}}
$$

Where $I_{\text{actual}}$ is measured operating current and $I_{\text{FLA}}$ is nameplate full load amps.

Actual mechanical power output:

$$
P_{\text{shaft,actual}} = \text{HP}_{\text{rated}} \times \text{Load Factor} \times 0.746 \text{ kW/HP}
$$

Motor input power at partial load:

$$
P_{\text{input,oversized}} = \frac{P_{\text{shaft,actual}}}{\eta_{\text{@load factor}}}
$$

Note that $\eta_{\text{@load factor}}$ must be obtained from motor performance curves, as efficiency varies significantly with load.

Select a properly-sized motor with rated capacity near the actual load (targeting 75-90% load factor):

$$
\text{HP}_{\text{properly-sized}} = \frac{P_{\text{shaft,actual}}}{0.746 \times 0.80}
$$

(Using 80% target load factor)

Annual energy savings:

$$
E_{\text{savings}} = \left(P_{\text{input,oversized}} - P_{\text{input,properly-sized}}\right) \times \text{Operating Hours}
$$

Power savings (kW) represent the reduction in motor input power:

$$
P_{\text{savings}} = P_{\text{input,oversized}} - P_{\text{input,properly-sized}}
$$



!!! warning "Starting Requirements"

    Some applications require high starting torque even if running loads are low. Compressors, loaded conveyors, and equipment with high inertia may need larger motors for starting duty even though running efficiency would favor a smaller motor. Verify starting requirements with equipment specifications before recommending downsizing.

## Anticipated Costs

Motor costs for properly-sized replacements follow the same pricing structure as [high efficiency motor upgrades](high-efficiency.md). Budget 2-4 hours of electrician labor for motors under 25 HP, plus additional time for mechanical modifications if required.

## Report Requirements

In addition to the [typical report requirements](../how-to.md) and the recommendation-specific savings and costs, the recommendation should include a table documenting all oversized motors recommended for replacement. The table should follow this structure:

- **Column 1:** Motor ID or equipment location

- **Column 2:** Current motor size (HP)

- **Column 3:** Measured load factor (%)

- **Column 4:** Recommended motor size (HP)

- **Column 5:** Annual operating hours (hrs/yr)

- **Column 6:** Annual energy savings (kWh/yr)

- **Column 7:** Annual power savings (kW-month)

- **Column 8:** Total Annual cost savings ($/yr)

Include a totals row at the bottom for multiple motors.

```latex
\begin{table}[H]
\centering
\caption{Motor Right-Sizing Recommendations}
\label{tab:motor-sizing}
\begin{tabular}{lccccccccc}
\toprule
Motor & Current & Measured & Recommended & Operating & Energy & Demand & Cost \\
Location & Size (HP) & Load (\%) & Size (HP) & Hours (hrs/yr) & Savings (kWh/yr) & Savings (kW-month) & Savings (\$/yr) \\
\midrule
Pump 1 &  &  &  &  &  &  &  \\
Fan 3 &  &  &  &  &  &  &  \\
Compressor 2 &  &  &  &  &  &  &  \\
\midrule
\textbf{Total} & \textbf{--} & \textbf{--} & \textbf{--} & \textbf{--} & \textbf{} & \textbf{} & \textbf{} & \textbf{} \\
\bottomrule
\end{tabular}
\end{table}
```
