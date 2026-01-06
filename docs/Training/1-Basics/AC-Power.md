# AC Power

## Why Alternating Current?

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; margin-bottom: 1em;">
  <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="https://www.youtube-nocookie.com/embed/c9gm_NL7KyE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

Nearly all industrial facilities run on alternating current (AC) rather than direct current (DC). The practical reason is transmission efficiency: AC voltage can be stepped up or down using transformers, which allows utilities to transmit power at high voltages (reducing current and therefore line losses) and then step it down to usable levels at the facility. DC systems would require far more complex and expensive conversion equipment to achieve the same thing.

In an AC system, voltage and current oscillate sinusoidally. In the United States, this oscillation occurs at 60 Hz, meaning the waveform completes 60 full cycles per second. The voltage you measure with a standard multimeter is the root-mean-square (RMS) value, which represents the equivalent DC voltage that would deliver the same power to a resistive load.

## Single-Phase vs. Three-Phase Systems

**Single-phase power** uses two conductors: one "hot" wire carrying the alternating voltage and one neutral wire that serves as the return path. This is what you find in most residential applications and powers things like lighting, small appliances, and office equipment. Single-phase power delivers energy in pulses, since the instantaneous power drops to zero twice per cycle (when the voltage crosses through zero).

**Three-phase power** uses three hot conductors, each carrying an AC waveform that is offset by 120 degrees from the others. The main benefit of this is reduced vibration in the outputs of motors. Because the three phases are offset, their combined instantaneous power never drops to zero. Thus, they produce a smoother output. Since vibrations are one of the main causes of failures in manufacturing systems, it's much better for reliability. 


Three-phase systems can be configured as either **wye (Y)** or **delta (Δ)** connections. In a wye configuration, each phase connects between a line conductor and a common neutral point. In a delta configuration, each phase connects between two line conductors with no neutral. The choice affects the relationship between line voltage (measured between any two hot conductors) and phase voltage (measured across a single winding). In a wye system, line voltage equals phase voltage multiplied by √3 (approximately 1.732). In a delta system, line voltage equals phase voltage. 

For ITAC assessments, you will most commonly encounter 480V three-phase delta systems for large motors and equipment, and 208V or 120/208V three-phase wye systems for smaller equipment and lighting.

## AC Power

When voltage and current are perfectly in phase (meaning they reach their peaks and zero crossings at the same instant), all the power delivered to the load does useful work. This is typical of purely resistive loads like electric heaters or incandescent lights.

However, most industrial loads are not purely resistive. Motors, transformers, and fluorescent lighting ballasts contain inductive elements that cause current to lag behind voltage. Some electronic equipment contains capacitive elements that cause current to lead voltage. When voltage and current are out of phase, the power situation becomes more complicated.

**Real power (P)** is measured in watts (W) or kilowatts (kW). This is the power that actually does useful work: turning motor shafts, producing heat, generating light. It is the power you ultimately pay for in terms of energy consumption (kWh).

**Reactive power (Q)** is measured in volt-amperes reactive (VAR) or kilovolt-amperes reactive (kVAR). Reactive power represents energy that sloshes back and forth between the source and the load's magnetic or electric fields without doing useful work. An induction motor, for example, needs reactive power to establish its magnetic field, but this power simply oscillates in and out of the motor windings rather than turning the shaft.

**Apparent power (S)** is measured in volt-amperes (VA) or kilovolt-amperes (kVA). This is the total power that the utility must supply and that the facility's wiring must carry. It represents the vector sum of real and reactive power:

$$S = \sqrt{P^2 + Q^2}$$

Alternatively, apparent power equals the product of RMS voltage and RMS current:

$$S = V \times I$$

## Power Factor

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; margin-bottom: 1em;">
  <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="https://www.youtube-nocookie.com/embed/Tv_7XWf96gg?start=535" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

Power factor (PF) is the ratio of real power to apparent power:

$$PF = \frac{P}{S}$$

Power factor ranges from 0 to 1 (often expressed as a percentage). A power factor of 1.0 (or 100%) means voltage and current are perfectly in phase, and all the apparent power is doing useful work. A power factor of 0.85 means only 85% of the apparent power is being converted to real power.

**Why power factor matters:**

1. **Utility penalties.** Many utilities charge penalties when a facility's power factor drops below a threshold (commonly 0.90 or 0.95). This is because the utility must generate, transmit, and distribute the full apparent power even though only the real power is billable as energy consumption.

2. **Capacity limitations.** Transformers, switchgear, and conductors are all rated in kVA (apparent power), not kW. A low power factor means you are using up capacity that could otherwise serve additional real load.

3. **Increased losses.** Higher current (for the same real power) means greater I²R losses in conductors and transformers.

**Lagging vs. leading power factor:**

Inductive loads (motors, transformers) cause current to lag voltage, producing a lagging power factor. This is by far the most common situation in industrial facilities.

Capacitive loads cause current to lead voltage, producing a leading power factor. This is less common but can occur with certain electronic equipment or when too many power factor correction capacitors are installed.

## Power Factor Correction

The most common method to improve (raise) a lagging power factor is to install power factor correction capacitors. Capacitors draw leading current, which partially cancels the lagging current drawn by inductive loads. The result is a net current that is more closely in phase with the voltage.

Capacitors can be installed at individual motors (local correction), at motor control centers (group correction), or at the main service entrance (central correction). Each approach has trade-offs:

| Location | Advantages | Disadvantages |
|----------|------------|---------------|
| Individual motor | Reduces current in all upstream conductors; correction automatically adjusts with motor operation | Higher installation cost; more capacitors to maintain |
| Motor control center | Reasonable balance of cost and effectiveness; easier to maintain than individual units | Does not reduce current in branch circuits |
| Main service entrance | Lowest installation cost; simplest to maintain | Only reduces utility demand charges; does not reduce internal conductor loading |

**Sizing capacitors:**

The reactive power (kVAR) needed to correct from an initial power factor (PF₁) to a target power factor (PF₂) can be calculated as:

$$Q_{correction} = P \times (\tan(\cos^{-1}(PF_1)) - \tan(\cos^{-1}(PF_2)))$$

Where P is the real power in kW.

!!! example

    To correct a 100 kW load from 0.80 PF to 0.95 PF:

    $$Q_{correction} = 100 \times (\tan(\cos^{-1}(0.80)) - \tan(\cos^{-1}(0.95)))$$

    $$Q_{correction} = 100 \times (0.75 - 0.33) = 42 \text{ kVAR}$$

!!! warning

    Over-correction (installing too much capacitance) can create a leading power factor, which some utilities also penalize. Additionally, capacitors can interact with harmonic currents in the system to create resonance problems. A qualified engineer should review any significant power factor correction installation.

## Demand vs. Consumption

With the electrical context established, we can now be more precise about demand and consumption:

**Consumption** is the total energy used over time, measured in kilowatt-hours (kWh). It equals the integral of real power over time. Your energy charge on the utility bill reflects consumption.

**Demand** is the average power drawn during a defined interval (typically 15 or 30 minutes), measured in kilowatts (kW). The utility records the highest demand interval during the billing period, and this peak demand determines your demand charge.

Because demand is based on real power (kW) while equipment sizing is based on apparent power (kVA), a low power factor effectively wastes capacity. If a facility is approaching the limits of its electrical infrastructure, power factor correction can defer or eliminate the need for expensive upgrades.