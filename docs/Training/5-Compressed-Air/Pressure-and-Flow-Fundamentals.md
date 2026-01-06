# Pressure and Flow Fundamentals

Compressed air systems introduce new units for measuring pressure and flow that you haven't encountered in previous modules. Understanding these units and their relationships is essential for analyzing compressed air system performance and calculating energy savings.

## Pressure: Gauge vs Absolute

You've probably heard of psi as a unit. It stands for pounds per square inch and measures pressure. However, there's an important subtlety: pressure can be measured relative to different reference points.

Consider this: atmospheric pressure at sea level is 14.7 psi, while a basketball is typically inflated to 7.5-8.5 psi. Wouldn't that mean the ball gets crushed by the outside atmosphere?

Since that clearly doesn't happen, there's something else going on. The basketball's pressure measurement is **relative** to atmospheric pressure. Meanwhile, the atmospheric pressure is given in **absolute** terms. To avoid this confusion, we use two different units:

**Pounds per Square Inch, Gauge (psig):** Pressure measured relative to standard atmospheric pressure at sea level. This is what most pressure gauges read. When you inflate a tire to 35 psi, that's 35 psig—35 psi above atmospheric pressure.

**Pounds per Square Inch, Absolute (psia):** Pressure measured relative to perfect vacuum (absolute zero pressure). This is the actual total pressure.

The relationship between these units is:

$$\text{psia} = \text{psig} + 14.7$$

!!! example 

    A basketball inflated to 8 psig actually contains air at:

    $$8 \text{ psig} + 14.7 = 22.7 \text{ psia}$$

    The air inside the ball is at absolute pressure of 22.7 psia, which is higher than the 14.7 psia atmospheric pressure outside, so the ball stays inflated.

For compressed air systems, we typically work in **psig** because we care about pressure relative to atmosphere. A compressor set to 100 psig delivers air at 100 psi above atmospheric pressure.

!!! tip 

    - Use **psig** for compressed air system pressures, gauge readings, and most ITAC calculations
    - Use **psia** for thermodynamic calculations involving ideal gas law or when absolute pressure matters

    When in doubt, check the context. If someone says "our system runs at 90 psi," they almost certainly mean 90 psig.

## Flow Rate and Volume

For compressed air systems, we work with horsepower (HP) as our unit for compressor power and kilowatt-hours (kWh) for energy consumption—after all, compressors are motor-driven systems. However, we also have units that act as **proxies** for power and energy on the air side:

**Cubic Feet per Minute (CFM):** The volumetric flow rate of compressed air. This is analogous to power—it tells you how much air is moving per unit time.

**Centi-Cubic Feet (CCF):** The volume of compressed air used. This is analogous to energy—it's the total amount consumed over time. (1 CCF = 100 cubic feet)

While these aren't actually measures of power and energy, they serve similar roles when analyzing compressed air systems. More flow (CFM) requires more compressor power. More total volume (CCF) requires more total energy.

## The Pressure Problem

Here's the complicating factor: **compressed air volume depends on pressure**.

One hundred cubic feet of air at 100 psig contains more air (in terms of mass or moles) than 100 cubic feet at 90 psig. The higher-pressure air is more compressed—more molecules packed into the same volume.

This creates a problem when comparing air consumption across different pressures. If one tool uses 10 CFM at 100 psig and another uses 10 CFM at 80 psig, which one uses more air? They're using the same volumetric flow rate, but the higher-pressure tool is actually consuming more mass of air per minute.

## Standard Conditions: SCFM and SCCF

To solve this problem, we reference all measurements to **standard conditions**—a fixed reference pressure and temperature. This lets us compare air consumption meaningfully.

**Standard Cubic Feet per Minute (SCFM):** Flow rate of air corrected to standard conditions (14.7 psia and 68°F). This tells you the equivalent flow rate if the air were at atmospheric pressure and room temperature.

**Standard Centi-Cubic Feet (SCCF):** Volume of air corrected to standard conditions.

When you measure SCFM, you're asking: "How much atmospheric air is the compressor taking in and compressing?" This is the actual mass flow rate, which determines compressor power consumption.

!!! example 

    A compressed air tool operating at 100 psig uses 20 CFM (measured at 100 psig).

    To find SCFM, we need to know how much atmospheric air must be compressed to supply that 20 CFM at 100 psig.

    Using the relationship between gauge and absolute pressure:

    $$\text{SCFM} = \text{CFM} \times \frac{P_{\text{actual}}}{P_{\text{standard}}} = 20 \times \frac{100 + 14.7}{14.7} = 20 \times 7.8 = 156 \text{ SCFM}$$

    The compressor must take in 156 cubic feet per minute of atmospheric air to supply 20 CFM at 100 psig to this tool.

## Converting Between CFM and SCFM

The general conversion formula is:

$$\text{SCFM} = \text{CFM} \times \frac{P_{\text{actual}}}{P_{\text{standard}}} \times \frac{T_{\text{standard}}}{T_{\text{actual}}}$$

Where:

- $P_{\text{actual}}$ = actual absolute pressure (psia)

- $P_{\text{standard}}$ = standard pressure = 14.7 psia

- $T_{\text{actual}}$ = actual absolute temperature (°R = °F + 460)

- $T_{\text{standard}}$ = standard temperature = 528°R (68°F)

For typical compressed air systems operating near room temperature, the temperature correction is small and often ignored, simplifying to:

$$\text{SCFM} \approx \text{CFM} \times \frac{P_{\text{actual}}}{14.7}$$

$$\text{SCFM} \approx \text{CFM} \times \frac{P_{\text{gauge}} + 14.7}{14.7}$$

!!! example 

    For a system running at 100 psig:

    $$\text{SCFM} \approx \text{CFM} \times \frac{100 + 14.7}{14.7} \approx \text{CFM} \times 7.8$$

    Every 1 CFM of air at 100 psig requires the compressor to intake about 7.8 CFM of atmospheric air.