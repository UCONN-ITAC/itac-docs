# Variable Frequency Drives and Soft Starters

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; margin-bottom: 1em;">
  <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="https://www.youtube-nocookie.com/embed/YA-6TNhFsE4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## What Is a VFD?

A variable frequency drive (VFD), also called a variable speed drive or inverter, is a power electronic device that converts fixed-frequency AC input to variable-frequency AC output. By varying the frequency, the VFD controls the speed of an AC induction motor.

Most VFDs use pulse-width modulation (PWM) to synthesize a variable-frequency AC waveform from DC power. The typical VFD contains three stages:

1. **Rectifier:** Converts incoming AC to DC using diodes.
2. **DC bus:** Filters and stores DC energy in capacitors.
3. **Inverter:** Switches DC into variable-frequency AC using transistors (IGBTs or similar devices).

The VFD adjusts both frequency and voltage together to maintain proper magnetic flux in the motor. This is called constant volts-per-hertz (V/Hz) control and is the most common VFD operating mode.

## Why VFDs Save Energy

As discussed in the Affinity Laws section, power consumption in centrifugal equipment (fans and pumps) varies with the **cube** of speed. Reducing fan or pump speed by 20% reduces power consumption by nearly 50%.

This cubic relationship is why VFDs are so effective for energy savings. Traditional throttling control (dampers on fans, valves on pumps) keeps the motor running at full speed and creates artificial restriction to reduce flow. The motor still consumes nearly full power because you are forcing it to push against a closed damper or valve.

VFD control reduces motor speed to match the required flow. The motor consumes only the power needed to deliver the actual demand. There is no artificial restriction, just less speed and therefore less power.

For detailed examples of VFD energy savings calculations using the affinity laws, refer to the previous section.

**Important limitation:** The affinity laws strictly apply only to centrifugal loads (fans and centrifugal pumps). For positive displacement equipment (screw compressors, positive displacement pumps), reducing speed proportionally reduces flow, but power reduction is much less dramatic and roughly linear with speed. VFDs can still provide savings on these applications by avoiding unloaded run time and providing better process control, but the cubic relationship does not apply.

## Benefits Beyond Energy Savings

**Soft starting:** VFDs ramp up motor speed gradually over several seconds. This eliminates the high inrush current (typically 6 to 8 times full load current) that occurs when starting a motor across-the-line. Soft starting reduces mechanical stress on belts, couplings, and driven equipment, extends equipment life, and avoids voltage sags that can affect other facility equipment. For very large motors, this eliminates the need for expensive reduced-voltage starters.

**Process control:** VFDs enable precise speed control for process optimization. Maintaining constant pressure in a water distribution system, controlling airflow to match oven temperature requirements, or matching conveyor speed to production rate all become straightforward with VFD control.

**Reduced maintenance:** By eliminating mechanical flow control devices (dampers, valves, vortex dampers) and reducing mechanical stress during starting, VFDs can reduce maintenance requirements.

## VFD Considerations and Limitations

**Harmonics:** VFDs draw non-sinusoidal current from the utility. This creates harmonic currents at multiples of the fundamental frequency (180 Hz, 300 Hz, 420 Hz, etc. for a 60 Hz system). Harmonics can cause overheating of transformers and neutral conductors, interference with sensitive electronic equipment, and resonance problems with power factor correction capacitors. Six-pulse drives (the most common type) typically have 5th and 7th harmonics as the dominant components. Twelve-pulse drives, line reactors, or active harmonic filters can mitigate these issues but add cost.

**Motor heating at low speeds:** Standard motors rely on shaft-mounted fans for cooling. At reduced speeds, cooling airflow decreases while motor losses may not decrease proportionally. Motors running continuously below 50% of rated speed may require external cooling or derating. Inverter-duty motors have improved insulation and more robust cooling designs to handle VFD operation.

**Cable length limitations:** VFDs produce high-frequency voltage spikes due to fast IGBT switching. These spikes can stress motor insulation, and the effect worsens with cable length due to reflections on long cable runs. Most manufacturers recommend cable lengths under 100 feet for standard motors, or up to several hundred feet with proper cable selection and motor insulation. Inverter-duty motors and shielded VFD cable extend these limits.

**Not appropriate for constant speed applications:** If a motor runs at full speed continuously, a VFD provides no energy savings and adds complexity, cost, and potential reliability concerns. VFDs make sense for variable loads, not constant loads.

## Soft Starters

A soft starter is a simpler and less expensive alternative to a VFD when the primary need is to reduce starting current and mechanical stress, rather than continuous speed control.

**How soft starters work:** A soft starter uses thyristors (silicon controlled rectifiers) to gradually ramp up voltage to the motor during starting. By controlling the firing angle of the thyristors, the soft starter increases voltage from a reduced level up to full voltage over a programmable time period (typically 5 to 30 seconds). Once the motor reaches full speed, the soft starter either bypasses itself with a contactor or remains in-line with minimal losses.

**Soft starter benefits:**

1. **Reduced starting current.** Starting current is typically limited to 200% to 400% of full load current instead of 600% to 800% for across-the-line starting.

2. **Reduced mechanical stress.** Gradual acceleration reduces stress on belts, chains, gearboxes, and driven equipment.

3. **Lower cost than VFDs.** Soft starters cost 30% to 50% of an equivalent VFD.

4. **Simpler installation.** Soft starters do not require special motor cables or harmonic mitigation.

**Soft starter limitations:**

1. **No speed control.** Once the motor reaches full speed, a soft starter provides no ongoing control. If the application would benefit from variable speed operation, a VFD is the better choice.

2. **No energy savings on variable loads.** A soft starter cannot slow down a motor to match reduced load. It only controls the starting ramp.

3. **Limited torque at starting.** Reducing voltage reduces available torque, so soft starters are not suitable for high-inertia or high-friction loads that require full torque to start.


## Selecting Between VFDs and Soft Starters

Use a **VFD** when:

- Flow or speed varies with load or process conditions

- Energy savings from speed control justify the higher cost

- Precise speed control is needed for the process

Use a **soft starter** when:

- The motor runs at constant speed once started

- The primary goal is to reduce starting current and mechanical stress

- Budget constraints favor the lower-cost option

Use **across-the-line starting** when:

- The motor is small (under 10 HP) and starting current is not a concern

- Starting frequency is low

- Simplicity and lowest cost are priorities

## VFD Sizing and Application

VFDs are rated in horsepower or kVA, and must be sized for the motor they control. The VFD rating should match or exceed the motor's full load current and horsepower. Oversizing the VFD is sometimes done to handle high-inertia loads or to provide additional overload capacity.

For retrofit applications, verify that the existing motor is suitable for VFD operation. Standard motors manufactured after approximately 1990 typically have adequate insulation for VFD use, but older motors or motors that will run at low speeds continuously may require replacement with inverter-duty motors.

Input voltage must match the VFD's rated input. Most industrial VFDs are available in 208V, 230V, 460V, and 575V versions. Output voltage is adjustable but cannot exceed input voltage.

For ITAC assessments, VFD recommendations typically focus on large fans and pumps (25 HP and above) with variable loads, where the affinity laws deliver substantial energy savings. The recommendation should quantify current energy consumption, estimate savings at typical reduced-speed operation, account for VFD installation and any required electrical work, and calculate simple payback based on annual savings.
