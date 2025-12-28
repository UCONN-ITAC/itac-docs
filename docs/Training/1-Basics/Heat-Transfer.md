# Heat Transfer

## Part 1: Conduction and R-Values

### Understanding Conduction

Conduction is heat transfer through a solid material. Heat flows from hot to cold, with the rate of flow depending on:

- Temperature difference across the material
- Thermal conductivity of the material
- Thickness of the material
- Surface area

The fundamental equation for conduction is Fourier's Law:

$$Q = \frac{k \cdot A \cdot \Delta T}{L}$$

Where:

- $Q$ = Heat flow rate (BTU/hr)
- $k$ = Thermal conductivity (BTU·in/(hr·ft²·°F))
- $A$ = Surface area (ft²)
- $\Delta T$ = Temperature difference (°F)
- $L$ = Thickness (inches)

### Thermal Resistance (R-Value)

In practice, we often use thermal resistance (R-value) instead of conductivity. R-value represents the resistance to heat flow:

$$R = \frac{L}{k}$$

The heat flow equation becomes:

$$Q = \frac{A \cdot \Delta T}{R}$$

Where $R$ = Thermal resistance (hr·ft²·°F/BTU)

Higher R-values mean better insulation. R-values are additive for multiple layers:

$$R_{\text{total}} = R_1 + R_2 + R_3 + ...$$

### Application: Insulation

Insulation works by providing high thermal resistance.

!!! info "Common Insulation Materials"

    | Material | R-Value per inch |
    |----------|------------------|
    | Fiberglass batt | 3.0-3.5 |
    | Mineral wool | 3.0-3.3 |
    | Spray foam (closed cell) | 6.0-7.0 |
    | Rigid foam board | 4.0-5.0 |
    | Calcium silicate (pipe) | 2.4-2.8 |

!!! example

    A wall has 6 inches of fiberglass insulation (R-3.5 per inch). The total R-value is:

    $$R_{\text{total}} = 6 \times 3.5 = 21 \text{ hr·ft²·°F/BTU}$$

    If the indoor temperature is 70°F and outdoor is 20°F, the heat loss per square foot is:

    $$\frac{Q}{A} = \frac{\Delta T}{R} = \frac{70 - 20}{21} = 2.38 \text{ BTU/(hr·ft²)}$$

    For a 1,000 ft² wall, total heat loss is:

    $$Q = 2.38 \times 1{,}000 = 2{,}380 \text{ BTU/hr}$$

### Calculating Bare Pipe Losses

Uninsulated pipes carrying hot fluids or steam lose heat to the surroundings. The heat loss depends on pipe diameter, surface temperature, and ambient conditions.

For horizontal cylindrical surfaces (pipes), a simplified approach:

$$Q = h \cdot A \cdot \Delta T$$

Where:

- $h$ = Combined convection and radiation heat transfer coefficient (BTU/(hr·ft²·°F))
- $A$ = Pipe surface area (ft²)
- $\Delta T$ = Surface temperature - ambient temperature (°F)

For bare pipes in still air, $h \approx 2.0$ BTU/(hr·ft²·°F) is a typical approximation.

!!! example

    A bare 4-inch diameter steam pipe is 100 feet long with surface temperature of 300°F in a room at 70°F.

    Surface area:
    $$A = \pi \cdot d \cdot L = \pi \times \frac{4}{12} \text{ ft} \times 100 \text{ ft} = 104.7 \text{ ft²}$$

    Heat loss:
    $$Q = 2.0 \times 104.7 \times (300 - 70) = 48{,}162 \text{ BTU/hr}$$

    Annual energy loss (8,000 operating hours):
    $$48{,}162 \times 8{,}000 = 385 \text{ MMBtu/year}$$

    At $10/MMBtu for natural gas, this bare pipe costs $3,850/year in heat losses.

**With insulation:**

When pipe insulation is added, it increases the effective R-value and reduces surface temperature. The outer surface of insulation is much cooler than the pipe surface, reducing losses by 85-95%.

!!! example

    Adding 2 inches of calcium silicate insulation (R = 2.5 per inch) to the same 4-inch pipe:

    With insulation, the outer surface temperature might drop to about 90°F (vs. 300°F bare).

    New heat loss:
    $$Q \approx 2.0 \times A_{\text{insulated}} \times (90 - 70)$$

    Even accounting for the larger outer diameter, heat loss drops to approximately 5,000 BTU/hr (90% reduction).

    Annual savings: 340 MMBtu/year or about $3,400/year.

### Calculating Tank Losses

Tanks and vessels lose heat through their walls, top, and bottom. Each surface can be analyzed separately using:

$$Q_{\text{total}} = Q_{\text{walls}} + Q_{\text{top}} + Q_{\text{bottom}}$$

For each surface:

$$Q = \frac{A \cdot \Delta T}{R}$$

!!! example

    A cylindrical hot water storage tank is 6 feet in diameter and 8 feet tall, holding water at 180°F in a 70°F room. The tank has 2 inches of insulation with R = 5 per inch (total R = 10).

    Wall area:
    $$A_{\text{wall}} = \pi \cdot d \cdot h = \pi \times 6 \times 8 = 150.8 \text{ ft²}$$

    Top and bottom areas:
    $$A_{\text{top}} = A_{\text{bottom}} = \pi \cdot r^2 = \pi \times 3^2 = 28.3 \text{ ft²}$$

    Heat loss from walls:
    $$Q_{\text{wall}} = \frac{150.8 \times (180 - 70)}{10} = 1{,}659 \text{ BTU/hr}$$

    Heat loss from top and bottom (assuming same R-value):
    $$Q_{\text{top+bottom}} = \frac{2 \times 28.3 \times 110}{10} = 623 \text{ BTU/hr}$$

    Total heat loss:
    $$Q_{\text{total}} = 1{,}659 + 623 = 2{,}282 \text{ BTU/hr}$$

### Understanding Building Envelope Heat Flow

Building envelope heat loss combines conduction through walls, roofs, windows, and infiltration (air leakage). The total heating or cooling load depends on:

1. **Conduction through envelope:** $Q = \frac{A \cdot \Delta T}{R}$ for each building component
2. **Infiltration:** $Q = 1.08 \times \text{CFM} \times \Delta T$ for sensible heat
3. **Windows:** Lower R-values (typically R-2 to R-5) compared to walls (R-13 to R-30)

!!! tip

    Windows are often the weakest link in building envelopes. Single-pane windows have R ≈ 1, while double-pane windows have R ≈ 2-3, and high-performance triple-pane windows reach R ≈ 5.

!!! example

    A facility has 500 ft² of single-pane windows (R = 1) and considers upgrading to double-pane (R = 3).

    Current heat loss through windows (indoor 70°F, outdoor 20°F):
    $$Q_{\text{current}} = \frac{500 \times (70 - 20)}{1} = 25{,}000 \text{ BTU/hr}$$

    After upgrade:
    $$Q_{\text{new}} = \frac{500 \times 50}{3} = 8{,}333 \text{ BTU/hr}$$

    Savings: 16,667 BTU/hr or 67% reduction in window heat loss.

## Part 2: Convection Basics

### Understanding Convection

Convection is heat transfer between a solid surface and a moving fluid (liquid or gas). The fluid motion carries heat away from or toward the surface. Convection heat transfer is described by:

$$Q = h \cdot A \cdot \Delta T$$

Where:

- $h$ = Convection heat transfer coefficient (BTU/(hr·ft²·°F))
- $A$ = Surface area (ft²)
- $\Delta T$ = Temperature difference between surface and fluid (°F)

The heat transfer coefficient $h$ depends on:

- Fluid properties (density, viscosity, thermal conductivity)
- Flow velocity (higher velocity = higher $h$)
- Flow regime (laminar vs. turbulent)
- Surface geometry

### Why Airflow Matters for Heat Exchangers

Heat exchangers rely on convection to transfer heat from one fluid to another through a separating wall. The overall heat transfer rate depends on convection coefficients on both sides.

Higher flow rates increase convection coefficients, improving heat transfer. However, this comes at the cost of increased pumping or fan energy and pressure drop.

**Design trade-off:**

- Too low airflow: Poor heat transfer, large/expensive heat exchanger required
- Too high airflow: High fan energy, excessive pressure drop
- Optimal airflow: Balances heat transfer performance with energy consumption

!!! example

    A cooling coil has water flowing inside tubes and air flowing across the outside. Doubling the air flow rate might increase the air-side heat transfer coefficient from 10 to 16 BTU/(hr·ft²·°F) (60% increase).

    However, pressure drop increases approximately with the square of velocity, so doubling flow rate increases fan energy by about 4 times (affinity laws).

    The optimal flow rate provides adequate heat transfer without excessive fan energy.

### How Fouled Coils Reduce Performance

Fouling occurs when dirt, dust, scale, or biological growth accumulates on heat exchanger surfaces. Fouling acts as an additional layer of insulation with low thermal conductivity, reducing the effective heat transfer coefficient.

For a fouled surface:

$$\frac{1}{U_{\text{fouled}}} = \frac{1}{U_{\text{clean}}} + R_{\text{fouling}}$$

Where:

- $U$ = Overall heat transfer coefficient
- $R_{\text{fouling}}$ = Fouling thermal resistance

Fouling reduces $U$, which directly reduces heat transfer rate:

$$Q = U \cdot A \cdot \Delta T_{\text{log mean}}$$

!!! example

    A chiller condenser has $U_{\text{clean}} = 200$ BTU/(hr·ft²·°F). After fouling, $R_{\text{fouling}} = 0.002$ hr·ft²·°F/BTU.

    $$\frac{1}{U_{\text{fouled}}} = \frac{1}{200} + 0.002 = 0.005 + 0.002 = 0.007$$

    $$U_{\text{fouled}} = \frac{1}{0.007} = 143 \text{ BTU/(hr·ft²·°F)}$$

    Heat transfer capacity drops to:
    $$\frac{143}{200} = 71.5\% \text{ of design capacity}$$

    This 28.5% reduction in heat transfer forces the chiller to work harder (higher condensing temperature and pressure), increasing compressor energy consumption by 10-15%.

!!! tip "Practical Implications of Fouling"

    - Dirty air filters restrict airflow and accumulate dust on coils
    - Scale buildup in water-side heat exchangers acts as insulation
    - Regular cleaning and maintenance restore heat transfer performance
    - Fouling is progressive and often goes unnoticed until performance degrades significantly

### The Relationship Between Flow Rate and Heat Transfer

For a given heat exchanger, increasing fluid flow rate:

1. **Increases convection coefficient $h$** (better heat transfer per unit area)
2. **Increases temperature difference** (less time for fluid to approach equilibrium)
3. **Increases pressure drop** (requires more pump/fan energy)

The relationship between flow rate and heat transfer coefficient is approximately:

$$h \propto \dot{m}^{0.8}$$

Where $\dot{m}$ = mass flow rate

This means a 25% increase in flow rate increases $h$ by about 20%, but pressure drop increases by about 56% (square relationship).

!!! example

    A hot water heating coil normally operates at 10 GPM flow rate. The building automation system reduces flow to 7 GPM (70% of design) during mild weather.

    Heat transfer coefficient changes:
    $$\frac{h_2}{h_1} = \left(\frac{7}{10}\right)^{0.8} = 0.74$$

    The heat transfer coefficient drops to 74% of design, but the pump energy drops to:
    $$\frac{W_2}{W_1} = \left(\frac{7}{10}\right)^3 = 0.343$$

    Pump energy is only 34% of design (66% energy savings), while heat transfer capability remains at 74%.

    If heating load is also reduced (mild weather), this is an excellent trade-off.

## Part 3: Radiation

### Understanding Thermal Radiation

All objects emit electromagnetic radiation based on their temperature. Unlike conduction and convection, radiation does not require a medium—it can transfer heat through a vacuum (like solar radiation through space).

The Stefan-Boltzmann Law describes radiation heat transfer:

$$Q = \varepsilon \cdot \sigma \cdot A \cdot (T_{\text{hot}}^4 - T_{\text{cold}}^4)$$

Where:

- $Q$ = Radiation heat transfer rate (BTU/hr)
- $\varepsilon$ = Emissivity (0 to 1, dimensionless)
- $\sigma$ = Stefan-Boltzmann constant (0.1714 × 10⁻⁸ BTU/(hr·ft²·°R⁴))
- $A$ = Surface area (ft²)
- $T$ = Absolute temperature (°R = °F + 460)

**Key concepts:**

- Radiation increases with the fourth power of absolute temperature
- Emissivity describes how effectively a surface emits radiation (black surfaces ≈ 0.9, shiny metals ≈ 0.1)
- Hot surfaces radiate much more than cool surfaces

### Application: Process Heating

In furnaces, ovens, and industrial heating processes, radiation is often the dominant heat transfer mechanism at high temperatures.

For example, in a gas-fired oven operating at 1,500°F, radiation provides the majority of heat transfer to the product. Combustion gases also provide convective heating, but radiation becomes more significant as temperature increases.

!!! example

    A furnace wall at 1,500°F (1,960°R) with emissivity 0.85 faces a part at 500°F (960°R). The net radiation heat transfer per square foot is:

    $$\frac{Q}{A} = 0.85 \times 0.1714 \times 10^{-8} \times (1{,}960^4 - 960^4)$$

    $$\frac{Q}{A} = 0.85 \times 0.1714 \times 10^{-8} \times (1.47 \times 10^{13} - 8.49 \times 10^{11})$$

    $$\frac{Q}{A} = 0.85 \times 0.1714 \times 10^{-8} \times 1.38 \times 10^{13} = 20{,}130 \text{ BTU/(hr·ft²)}$$

    This extremely high heat flux demonstrates why radiation dominates at high temperatures.

### Application: Solar Gain

Solar radiation entering buildings through windows contributes to cooling loads in summer and reduces heating loads in winter. Solar gain depends on:

- Window area and orientation
- Solar intensity (varies by time of day, season, and weather)
- Window properties (single vs. double pane, coatings)
- Shading (trees, overhangs, blinds)

!!! info "Typical Solar Radiation on a Sunny Day"

    - South-facing window (summer, noon): 200-250 BTU/(hr·ft²)
    - East/west-facing window (morning/afternoon): 150-200 BTU/(hr·ft²)
    - North-facing window: 50-100 BTU/(hr·ft²)

!!! example

    A facility has 1,000 ft² of west-facing windows receiving 200 BTU/(hr·ft²) of solar radiation during afternoon hours. If windows transmit 80% of incident radiation:

    $$Q_{\text{solar}} = 1{,}000 \times 200 \times 0.80 = 160{,}000 \text{ BTU/hr}$$

    This equals 13.3 tons of additional cooling load during sunny afternoons (12,000 BTU/hr = 1 ton).

    Installing solar film or shades that reduce transmission to 30% would cut solar gain to 60,000 BTU/hr, reducing cooling load by 8.3 tons.

### Why Surface Temperature Matters for Losses from Hot Equipment

Hot equipment (tanks, pipes, furnaces, dryers) loses heat through both convection and radiation. At high surface temperatures, radiation losses become significant and increase rapidly with temperature.

Combined heat loss from a hot surface:

$$Q_{\text{total}} = Q_{\text{convection}} + Q_{\text{radiation}}$$

$$Q_{\text{total}} = h_c \cdot A \cdot (T_s - T_\infty) + \varepsilon \cdot \sigma \cdot A \cdot (T_s^4 - T_\infty^4)$$

Where:

- $h_c$ = Convection coefficient
- $T_s$ = Surface temperature
- $T_\infty$ = Ambient temperature

!!! tip

    At surface temperatures above 200°F, radiation becomes a significant fraction of total heat loss. At 500°F and above, radiation often dominates.

!!! example

    An industrial dryer has an exterior surface at 350°F (810°R) with emissivity 0.9 in a 70°F (530°R) room. Surface area is 200 ft².

    Convection loss (assuming $h_c = 2.0$):
    $$Q_{\text{conv}} = 2.0 \times 200 \times (350 - 70) = 112{,}000 \text{ BTU/hr}$$

    Radiation loss:
    $$Q_{\text{rad}} = 0.9 \times 0.1714 \times 10^{-8} \times 200 \times (810^4 - 530^4)$$

    $$Q_{\text{rad}} = 0.9 \times 0.1714 \times 10^{-8} \times 200 \times (4.30 \times 10^{11} - 7.89 \times 10^{10})$$

    $$Q_{\text{rad}} = 109{,}000 \text{ BTU/hr}$$

    Total heat loss:
    $$Q_{\text{total}} = 112{,}000 + 109{,}000 = 221{,}000 \text{ BTU/hr}$$

    Radiation accounts for 49% of heat loss. Adding insulation reduces surface temperature, cutting both convection and radiation losses.

### Practical Implications for ITAC Work

Understanding heat transfer mechanisms helps you:

1. **Quantify insulation opportunities:** Calculate actual savings from insulating pipes, tanks, and equipment
2. **Diagnose heat exchanger problems:** Recognize when fouling or inadequate airflow limits performance
3. **Evaluate building envelope improvements:** Prioritize window upgrades, wall insulation, and infiltration reduction
4. **Understand temperature's role:** Recognize that high surface temperatures mean disproportionately high heat losses due to radiation
5. **Optimize system operation:** Balance heat transfer performance against fan/pump energy consumption

Surface temperature is a critical indicator. Hot surfaces visible during facility walkthroughs represent energy loss opportunities. A thermal imaging camera makes these losses visible and helps prioritize improvements.
