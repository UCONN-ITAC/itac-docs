# Thermodynamics

## Part 1: First Law Energy Balances

### The First Law of Thermodynamics

The First Law of Thermodynamics is a statement of energy conservation: energy cannot be created or destroyed, only converted from one form to another. For any system, the energy entering must equal the energy leaving plus any accumulation within the system.

$$ \text{Energy In} = \text{Energy Out} + \text{Accumulation}$$ 

For steady-state processes (no accumulation), this simplifies to:

$$ \text{Energy In} = \text{Energy Out}$$ 

This fundamental principle allows us to analyze equipment performance and identify energy losses.

### Applying Energy Balances to Equipment

**Boilers:**

A boiler converts fuel energy into heat in steam or hot water. The energy balance is:

$$ \dot{Q}_{\text{fuel}} = \dot{Q}_{\text{output}} + \dot{Q}_{\text{losses}}$$ 

Where:

- $\dot{Q}_{\text{fuel}}$ = Energy input from fuel (MMBtu/hr)
- $\dot{Q}_{\text{output}}$ = Useful heat output to steam or hot water (MMBtu/hr)
- $\dot{Q}_{\text{losses}}$ = Heat losses through flue gas, radiation, and blowdown (MMBtu/hr)

!!! example

    A boiler burns natural gas at 20 MMBtu/hr input and produces steam carrying 16 MMBtu/hr of useful heat. The losses are:

    $$ \dot{Q}_{\text{losses}} = 20 - 16 = 4 \text{ MMBtu/hr}$$ 

    These 4 MMBtu/hr leave primarily through hot flue gases, representing 20% of the fuel input.

**Chillers:**

A chiller removes heat from a chilled water loop and rejects it to a condenser water loop or air. The energy balance includes electrical work input:

$$ \dot{Q}_{\text{evaporator}} + \dot{W}_{\text{compressor}} = \dot{Q}_{\text{condenser}}$$ 

Where:

- $\dot{Q}_{\text{evaporator}}$ = Heat removed from chilled water (cooling capacity)
- $\dot{W}_{\text{compressor}}$ = Electrical work input to compressor
- $\dot{Q}_{\text{condenser}}$ = Heat rejected to condenser water or outdoor air

!!! example

    A chiller provides 300 tons of cooling (1,200,000 BTU/hr) and draws 200 kW of electrical power. The condenser must reject:

    $$ \dot{Q}_{\text{condenser}} = 1{,}200{,}000 \text{ BTU/hr} + 200 \text{ kW} \times 3{,}412 \frac{\text{BTU/hr}}{\text{kW}}$$ 

    $$ \dot{Q}_{\text{condenser}} = 1{,}200{,}000 + 682{,}400 = 1{,}882{,}400 \text{ BTU/hr}$$ 

    The cooling tower or air-cooled condenser must reject about 1.57 times the cooling load.

**Heat Exchangers:**

In a heat exchanger, hot fluid transfers heat to cold fluid with no external work input. Assuming no heat loss to surroundings:

$$ \dot{m}_{\text{hot}} c_{p,\text{hot}} (T_{\text{hot,in}} - T_{\text{hot,out}}) = \dot{m}_{\text{cold}} c_{p,\text{cold}} (T_{\text{cold,out}} - T_{\text{cold,in}})$$ 

Where:

- $\dot{m}$ = Mass flow rate
- $c_p$ = Specific heat capacity
- $T$ = Temperature

The heat lost by the hot fluid equals the heat gained by the cold fluid.

!!! example

    Hot water flows through a heat exchanger at 10 GPM, cooling from 180°F to 120°F. Cold water flows at 8 GPM, entering at 60°F. What is the outlet temperature of the cold water?

    Assuming water has $c_p = 1$ BTU/(lb·°F) and density of 8.34 lb/gal:

    Heat lost by hot water:
    $$ \dot{Q} = (10 \text{ GPM} \times 8.34 \text{ lb/gal}) \times 1 \times (180 - 120) = 5{,}004 \text{ BTU/min}$$ 

    Heat gained by cold water:
    $$ 5{,}004 = (8 \times 8.34) \times 1 \times (T_{\text{out}} - 60)$$ 

    $$ T_{\text{out}} = 60 + \frac{5{,}004}{66.72} = 135°\text{F}$$ 

## Part 2: Enthalpy and Latent Heat

### Understanding Enthalpy

Enthalpy is the total heat content of a substance, including both sensible heat (temperature-related) and latent heat (phase change energy). For phase changes like boiling or condensation, enthalpy changes dramatically with no temperature change.

### Sensible vs. Latent Heat

**Sensible heat** changes temperature:

$$ Q = m c_p \Delta T$$ 

**Latent heat** changes phase at constant temperature:

$$ Q = m h_{fg}$$ 

Where:

- $h_{fg}$ = Latent heat of vaporization (BTU/lb)

!!! info "Latent Heat Magnitude"

    For water at atmospheric pressure, $h_{fg} \approx 970$ BTU/lb. This means it takes about 970 BTU to evaporate 1 lb of water at 212°F, but only about 180 BTU to heat that same pound of water from 32°F to 212°F.

### Application: Steam Systems

Steam systems leverage latent heat for efficient heat transfer. When steam condenses, it releases its latent heat without a significant temperature drop, making it ideal for process heating.

**Why condensate return matters:**

When steam condenses, the resulting condensate is hot water (typically 180-212°F depending on pressure). This condensate contains significant sensible heat. Returning it to the boiler feedwater tank recovers this heat and reduces makeup water heating requirements.

!!! example

    A facility generates 10,000 lb/hr of steam at 150 psig. Steam condenses in heat exchangers and could be returned to the boiler feedwater tank at 280°F.

    If condensate is returned, makeup water only needs to be heated from 60°F to 280°F.
    If condensate is wasted, makeup water must be heated from 60°F to 280°F for the entire flow.

    Heat content of condensate (relative to 60°F):
    $$ Q = 10{,}000 \text{ lb/hr} \times 1 \text{ BTU/(lb·°F)} \times (280 - 60) = 2{,}200{,}000 \text{ BTU/hr}$$ 

    Returning condensate saves 2.2 MMBtu/hr of boiler fuel input, worth approximately $20,000-30,000 annually.

**How steam traps work:**

Steam traps automatically discharge condensate while preventing live steam from escaping. They exploit differences in temperature, density, or phase between steam and condensate. A failed-open steam trap wastes enormous energy by venting live steam.

!!! example

    A steam trap fails open, venting steam at 100 psig. If the orifice is 1/8" diameter, approximately 25 lb/hr of steam escapes.

    Energy loss:
    $$ Q = 25 \text{ lb/hr} \times 970 \text{ BTU/lb} = 24{,}250 \text{ BTU/hr}$$ 

    Annual energy waste at 8,000 operating hours:
    $$ 24{,}250 \times 8{,}000 = 194 \text{ MMBtu/year}$$ 

    At $10/MMBtu natural gas, this single failed trap costs about $1,940/year.

**Blowdown losses:**

Boilers require blowdown to remove dissolved solids that concentrate in the boiler water. Blowdown discharges hot boiler water, wasting both the water itself and its heat content.

!!! example

    A boiler operates at 150 psig (366°F saturated temperature) with 5% blowdown rate on a 10,000 lb/hr steam load.

    Blowdown flow:
    $$ \dot{m}_{\text{blowdown}} = 10{,}000 \times 0.05 = 500 \text{ lb/hr}$$ 

    Heat content of blowdown water (relative to 60°F makeup):
    $$ Q = 500 \times 1 \times (366 - 60) = 153{,}000 \text{ BTU/hr}$$ 

    Installing a blowdown heat exchanger to preheat makeup water can recover 60-70% of this energy.

## Part 3: Efficiency Definitions

### Combustion Efficiency

Combustion efficiency measures how much of the fuel's chemical energy is transferred to the working fluid (steam or hot water) versus lost up the stack in flue gases.

$$ \eta_{\text{combustion}} = \frac{\text{Heat absorbed by steam/water}}{\text{Fuel energy input}}$$ 

!!! info "Typical Combustion Efficiencies"

    - Modern condensing boilers: 90-96%
    - Non-condensing boilers (well-maintained): 80-85%
    - Older or poorly maintained boilers: 70-80%

Combustion efficiency decreases when:

- Excess air is too high (heating unnecessary air)
- Stack temperature is excessive (hot flue gases carry away energy)
- Boiler surfaces are fouled (poor heat transfer)

!!! example

    A boiler burns natural gas at 10 MMBtu/hr input. Combustion analysis shows 82% combustion efficiency.

    Useful heat delivered:
    $$ \dot{Q}_{\text{output}} = 10 \times 0.82 = 8.2 \text{ MMBtu/hr}$$ 

    Stack losses:
    $$ \dot{Q}_{\text{stack}} = 10 - 8.2 = 1.8 \text{ MMBtu/hr}$$ 

    Improving combustion efficiency to 85% would increase output by 0.3 MMBtu/hr (3.7% fuel savings).

### Thermal Efficiency

Thermal efficiency accounts for all heat losses from equipment, including combustion losses, radiation losses, and blowdown losses.

$$ \eta_{\text{thermal}} = \frac{\text{Net heat output to process}}{\text{Fuel energy input}}$$ 

!!! tip

    Thermal efficiency is always lower than combustion efficiency because it includes additional losses. For boilers, radiation and blowdown typically reduce thermal efficiency by 1-3 percentage points below combustion efficiency.

### System Efficiency

System efficiency considers the entire system, including distribution losses, end-use efficiency, and utilization.

$$ \eta_{\text{system}} = \eta_{\text{generation}} \times \eta_{\text{distribution}} \times \eta_{\text{utilization}}$$ 

!!! example

    A steam system has:
    - Boiler thermal efficiency: 83%
    - Distribution losses (piping, traps, leaks): 15% (85% reaches the process)
    - Process utilization: 90% (some steam vented during startup/shutdown)

    Overall system efficiency:
    $$ \eta_{\text{system}} = 0.83 \times 0.85 \times 0.90 = 0.635 \text{ or } 63.5\%$$ 

    This means only 63.5% of the fuel energy input actually performs useful work. The rest is lost at various stages.

### Interpreting Equipment Specifications

When evaluating equipment:

- **Nameplate ratings** show capacity under design conditions, not actual efficiency
- **Combustion efficiency** from a test report tells you stack losses only
- **Thermal efficiency** is more complete but may not reflect actual operating conditions
- **System efficiency** requires analyzing the entire system in real operating conditions

!!! tip "Why Actual Performance Differs from Specifications"

    Actual performance often differs from specifications due to:

    - Part-load operation (most equipment operates at part load most of the time)
    - Poor maintenance (fouling, air leaks, worn components)
    - Oversized equipment (cycling losses, poor turndown)
    - Distribution system losses not accounted for in equipment specs

## Part 4: Second Law Concepts

### The Second Law of Thermodynamics

The Second Law states that heat naturally flows from hot to cold, and all real processes increase the total entropy (disorder) of the universe. Practically, this means:

1. You cannot convert heat to work with 100% efficiency
2. You cannot transfer heat from cold to hot without work input
3. Temperature differences limit heat recovery potential

### Why You Cannot Recover All Waste Heat

Heat recovery is limited by temperature differences. To transfer heat from a waste stream to a useful stream, the waste stream must be hotter than the destination stream. The greater the temperature difference, the more heat you can recover and the smaller the heat exchanger required.

**The temperature pinch:**

In a heat exchanger, the minimum temperature difference between the hot and cold streams (called the "approach temperature" or "pinch") limits heat recovery. Trying to achieve zero approach temperature would require an infinitely large heat exchanger.

!!! example

    Exhaust air leaves a building at 75°F. Incoming outdoor air is at 20°F. A heat recovery ventilator can preheat the incoming air, but not to 75°F.

    With a 10°F approach temperature, the incoming air can be heated to:
    $$ T_{\text{preheat}} = 75 - 10 = 65°F$$ 

    You cannot recover the last 10°F of temperature difference without an impractically large heat exchanger. The heat content in that final 10°F remains in the exhaust stream.

### What Limits Heat Exchanger Performance

Heat exchanger effectiveness is limited by:

1. **Temperature approach:** Smaller approach requires larger, more expensive heat exchangers
2. **Flow rates:** If flows are unbalanced, the stream with higher thermal capacity (flow × specific heat) limits heat transfer
3. **Heat transfer coefficients:** Fouling, air films, and material properties reduce heat transfer rates
4. **Counterflow vs. parallel flow:** Counterflow arrangement achieves closer approach temperatures

The effectiveness of a heat exchanger is defined as:

$$ \varepsilon = \frac{\text{Actual heat transferred}}{\text{Maximum possible heat transfer}}$$ 

!!! info "Heat Exchanger Effectiveness"

    Maximum possible heat transfer would bring the outlet temperature of one stream to the inlet temperature of the other stream. Real heat exchangers achieve 50-90% effectiveness depending on design.

### Why Refrigeration Requires Work Input

The Second Law prevents heat from flowing naturally from cold to hot. Air conditioning and refrigeration move heat "uphill" from a cold space to a warm space, which requires work input.

A refrigeration cycle uses a compressor to:
1. Compress refrigerant, raising its temperature above the outdoor/condenser temperature
2. Reject heat to the outdoors through the condenser (heat flows hot to cold)
3. Expand refrigerant, lowering its temperature below the indoor/evaporator temperature
4. Absorb heat from indoors through the evaporator (heat flows hot to cold)

The compressor work input is essential to maintain the temperature difference that drives heat flow in the desired direction.

**Coefficient of Performance (COP):**

Refrigeration efficiency is measured by COP:

$$ \text{COP} = \frac{\text{Cooling delivered}}{\text{Work input}}$$ 

The Second Law sets theoretical limits on COP based on operating temperatures. For cooling:

$$ \text{COP}_{\text{Carnot}} = \frac{T_{\text{cold}}}{T_{\text{hot}} - T_{\text{cold}}}$$ 

Where temperatures are in absolute units (Rankine or Kelvin).

!!! example

    An ideal refrigeration cycle operates between an evaporator at 40°F (500°R) and a condenser at 100°F (560°R).

    Maximum theoretical COP:
    $$ \text{COP}_{\text{Carnot}} = \frac{500}{560 - 500} = \frac{500}{60} = 8.33$$ 

    Real chillers achieve COP of 3-6, well below the Carnot limit due to real-world inefficiencies (compressor losses, pressure drops, heat transfer limitations).

    A chiller with COP = 4.5 means every kW of electrical input provides 4.5 kW of cooling, or every ton of cooling requires 0.78 kW (converted to tons: 12,000 BTU/hr ÷ 3,412 BTU/hr/kW ÷ 4.5 = 0.78 kW/ton).

### Practical Implications for ITAC Work

Understanding Second Law limitations helps you:

1. **Identify realistic heat recovery opportunities:** Don't propose recovering heat from 120°F waste water to heat a process requiring 150°F input
2. **Evaluate heat exchanger sizing:** Recognize that approach temperatures of 5-15°F are typical; claiming 2°F approach requires justification
3. **Understand refrigeration costs:** Recognize that cooling is fundamentally more expensive than heating because it requires work input to move heat against its natural direction
4. **Assess system quality:** Large temperature differences (hot stack temperatures, cold condensate returns, high condenser temperatures) indicate wasted energy and improvement opportunities

The Second Law tells us that temperature is a measure of energy quality. High-temperature heat can do more useful work than low-temperature heat. Degrading high-quality energy (burning fuel to make low-temperature heat) is thermodynamically wasteful, which is why cogeneration and heat cascading are valuable strategies.
