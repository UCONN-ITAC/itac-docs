# Upgrade to Efficient Lighting Fixtures

Older lighting fixtures using incandescent, fluorescent, or high-intensity discharge (HID) lamps consume significantly more energy than modern LED fixtures to produce the same light output. Replacing inefficient fixtures with LED or other high-efficiency lighting reduces electrical consumption, cooling loads, and maintenance costs.

**ARC Code(s):** 2.7142

## Savings Calculation

Energy savings from efficient lighting fixtures result from reduced wattage to produce the same or better illumination levels. The savings depend on the wattage difference between baseline and proposed fixtures, annual operating hours, and the impact on cooling loads from reduced heat generation.

### Annual Energy Savings

Annual energy savings from replacing fixtures are:

$$
\Delta kWh_{\text{lighting}} = \frac{(W_{\text{baseline}} - W_{\text{proposed}}) \times H \times N}{1000}
$$

Where:

- $W_{\text{baseline}}$ = Wattage of existing fixture (watts)
- $W_{\text{proposed}}$ = Wattage of proposed efficient fixture (watts)
- $H$ = Annual operating hours (hours/year). Use 5,793 hours/year if facility-specific operating hours cannot be determined.
- $N$ = Number of fixtures being replaced

### Cooling Load Reduction

Reduced fixture wattage decreases heat gain to conditioned spaces, reducing cooling energy consumption:

$$
\Delta kWh_{\text{cool}} = \frac{\Delta kWh_{\text{lighting}} \times F}{COP}
$$

Where:

- $F$ = Fraction of lighting energy savings that reduces cooling load (see table below)
- $COP$ = Coefficient of performance for cooling system (use 3.5 for retrofit applications)

| Building Description | F |
|---------------------|---|
| HVAC system includes an economizer | 0.35 |
| No economizer, building area < 2,000 ft² | 0.48 |
| No economizer, building area 2,000 – 20,000 ft² | $0.48 + \frac{0.195 \times (A - 2000)}{18000}$ |
| No economizer, building area > 20,000 ft² | 0.675 |

Total annual electric savings:

$$
\Delta kWh = \Delta kWh_{\text{lighting}} + \Delta kWh_{\text{cool}}
$$

### Peak Demand Savings

Summer peak demand savings include both lighting reduction and cooling load impact:

$$
\Delta kW_{\text{summer}} = \frac{(W_{\text{baseline}} - W_{\text{proposed}}) \times N \times (1 + G/COP)}{1000}
$$

Winter peak demand savings exclude cooling effects:

$$
\Delta kW_{\text{winter}} = \frac{(W_{\text{baseline}} - W_{\text{proposed}}) \times N}{1000}
$$

Where:

- $G$ = Estimated lighting energy heat to space (0.73)

!!! warning "Summer and Winter Period Definitions"

    For demand savings calculations, "summer" represents 3 months of the year and "winter" represents 9 months of the year. Apply the appropriate demand savings calculation for each period when estimating annual demand cost savings.

### Annual Demand Savings

Annual demand savings in kW-month are calculated by applying peak factors to the summer and winter demand savings:

$$
\Delta kW\text{-month} = (\Delta kW_{\text{summer}} \times PF_{\text{summer}} \times 3) + (\Delta kW_{\text{winter}} \times PF_{\text{winter}} \times 9)
$$

Where:

- $PF_{\text{summer}}$ = Summer peak factor (0.83 for manufacturing facilities)
- $PF_{\text{winter}}$ = Winter peak factor (0.665 for manufacturing facilities)
- 3 = number of summer months
- 9 = number of winter months

Important assumptions to state in the analysis:

- Lighting operating hours should be facility-specific where possible; use 5,793 hours/year if measured data unavailable
- Baseline and proposed fixture wattages should include ballast/driver losses
- Light output (lumens) of proposed fixtures should meet or exceed baseline fixtures
- Verify that proposed fixtures are compatible with existing controls and mounting hardware


## Anticipated Costs

Obtain equipment costs from vendor quotes or manufacturer pricing for the specific fixture type being recommended. Include both fixture costs and any required accessories (mounting hardware, lenses, etc.). Installation labor costs should be obtained from local electrical contractors or estimated based on project-specific conditions including ceiling height, access constraints, and disposal requirements for existing fixtures.

Check with the local utility provider for current energy efficiency incentive programs. Lighting fixture upgrades often qualify for prescriptive rebates based on fixture type and wattage reduction. Document incentive eligibility requirements and application procedures in the cost analysis.

## Report Requirements

In addition to the [typical report requirements](../how-to.md) and the recommendation-specific savings and costs, the recommendation should include a table documenting all fixtures being replaced. The table should follow this structure:

- **Column 1:** Location or fixture description
- **Column 2:** Number of fixtures
- **Column 3:** Baseline fixture wattage (W)
- **Column 4:** Proposed fixture wattage (W)
- **Column 5:** Operating hours (hrs/yr)
- **Column 6:** Annual energy savings (kWh/yr)
- **Column 7:** Annual demand savings (kW-month)
- **Column 8:** Annual cost savings ($/yr)

If multiple fixture types are being replaced, include a totals row at the bottom.

```latex
\begin{table}[H]
\centering
\caption{Efficient Lighting Fixture Upgrade Summary}
\label{tab:lighting-upgrade}
\begin{tabular}{lcccccccc}
\toprule
Location & Quantity & Baseline & Proposed & Operating & Energy & Demand & Cost \\
 &  & Wattage (W) & Wattage (W) & Hours (hrs/yr) & Savings (kWh/yr) & Savings (kW-month) & Savings (\$/yr) \\
\midrule
Warehouse High Bay &  &  &  &  &  &  &  \\
Office Troffers &  &  &  &  &  &  &  \\
Parking Lot &  &  &  &  &  &  &  \\
\midrule
\textbf{Total} & \textbf{} & \textbf{--} & \textbf{--} & \textbf{--} & \textbf{} & \textbf{} & \textbf{} \\
\bottomrule
\end{tabular}
\end{table}
```
