# Fluids

## Part 1: Pressure Drop in Piping

### Understanding Pressure Drop

When fluids flow through pipes, friction between the fluid and pipe walls causes a loss of pressure. This pressure drop must be overcome by pumps (for liquids) or compressors (for gases), which consume energy. Minimizing unnecessary pressure drop is critical for reducing energy consumption.

The pressure drop in a pipe depends on several factors:

- Flow rate (higher flow = higher pressure drop)
- Pipe diameter (smaller diameter = higher pressure drop)
- Pipe length (longer pipe = higher pressure drop)
- Fluid viscosity and density
- Pipe roughness and fittings

### The Relationship Between Pipe Size and Pressure Drop

For a given flow rate, pressure drop varies approximately with the inverse fifth power of pipe diameter:

$$\Delta P \propto \frac{1}{d^5}$$

Where:

- $\Delta P$ = Pressure drop
- $d$ = Pipe inside diameter

This means that even small reductions in pipe diameter cause dramatic increases in pressure drop.

!!! example

    If you reduce a pipe diameter by half (from 2" to 1"), the pressure drop increases by a factor of approximately:

    $$\frac{1}{(0.5)^5} = \frac{1}{0.03125} = 32$$

    The pressure drop becomes 32 times higher, requiring significantly more energy to maintain the same flow rate.

### Application: Compressed Air Systems

!!! info "Why Compressed Air Systems Are Sensitive to Pressure Drop"

    Compressed air systems are particularly sensitive to pressure drop because:

    1. Air must be compressed to overcome both the end-use pressure requirements AND all pressure losses in the distribution system
    2. Compression is energy-intensive (typically 7-8 kW of electricity per CFM of compressed air capacity)

**Why oversized piping saves energy:**

If a compressed air system has excessive pressure drop in the distribution piping, the compressor must generate higher pressure at the source to compensate. This requires additional compressor work.

!!! example

    A facility needs 90 psig at the point of use. If the distribution system has 15 psi of pressure drop, the compressor must produce 105 psig instead of 90 psig. This increases compressor energy consumption by approximately 8-10%.

**Why reducing leaks lowers compressor load:**

Leaks increase the total flow rate through the system. Since pressure drop increases with flow rate, leaks cause both:

1. Direct energy waste (compressing air that escapes)
2. Indirect energy waste (increased pressure drop requires higher compressor discharge pressure)

!!! tip

    A 10% reduction in leak flow can reduce compressor energy consumption by more than 10% due to these combined effects.

### Application: Pumping Systems

The same principles apply to liquid pumping. Oversized piping, smooth pipe interiors, and minimal fittings all reduce the pressure (head) that pumps must develop, which reduces energy consumption.

!!! example

    A cooling water system pumps 500 GPM through 300 feet of pipe. If you increase the pipe diameter from 3" to 4", the pressure drop might decrease from 25 psi to 8 psi. This means the pump motor can potentially be downsized or operated at lower speed, saving energy.

## Part 2: Affinity Laws

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/siXbmrNsoCQ?si=-eQoxMvU8ZHJiMzC" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### The Foundation of VFD Savings

The affinity laws (also called fan laws or pump laws) describe how the performance of fans and pumps changes when their rotational speed changes. These relationships explain why Variable Frequency Drives (VFDs) are so effective for energy savings.

### The Three Affinity Laws

For a fan or pump at different speeds, with constant fluid density and system geometry:

**Flow is proportional to speed:**

$$\frac{Q_2}{Q_1} = \frac{N_2}{N_1}$$

**Pressure (or head) is proportional to speed squared:**

$$\frac{P_2}{P_1} = \left(\frac{N_2}{N_1}\right)^2$$

**Power is proportional to speed cubed:**

$$\frac{W_2}{W_1} = \left(\frac{N_2}{N_1}\right)^3$$

Where:

- $Q$ = Flow rate (CFM for air, GPM for liquids)
- $N$ = Rotational speed (RPM)
- $P$ = Pressure (for fans) or head (for pumps)
- $W$ = Power consumption
- Subscript 1 = initial condition
- Subscript 2 = new condition

### Why VFDs Save So Much Energy

The cubic relationship between speed and power is the key to VFD energy savings. Small reductions in speed produce dramatic reductions in power consumption.

!!! example

    A fan operates at 1,200 RPM and consumes 50 kW. If a VFD reduces the speed to 960 RPM (80% of original speed), what is the new power consumption?

    Using the affinity laws:

    $$\frac{N_2}{N_1} = \frac{960}{1{,}200} = 0.8$$

    $$\frac{W_2}{W_1} = (0.8)^3 = 0.512$$

    $$W_2 = 50 \text{ kW} \times 0.512 = 25.6 \text{ kW}$$

    The power consumption drops to 25.6 kW, a savings of 49%. This is why slowing a fan or pump to 80% speed saves about 50% of the energy, not 20%.

### Practical Application: Part-Load Operation

Most HVAC systems and many process systems operate at part load most of the time. Building cooling loads vary with outdoor temperature and occupancy. Process demands fluctuate with production schedules.

**Traditional throttling approach:**

Without a VFD, operators reduce flow by:
- Closing a damper (for fans)
- Throttling a valve (for pumps)

This maintains high speed while creating artificial resistance. The pressure drop across the damper or valve wastes energy. The fan or pump still operates at nearly full power even though it delivers reduced flow.

**VFD approach:**

A VFD reduces the motor speed to match the required flow. Because power drops with the cube of speed, energy savings are substantial.

!!! example

    An air handler supplies 10,000 CFM at full speed (1,200 RPM) and consumes 40 kW. During mild weather, only 6,000 CFM is needed.

    With damper control: The fan still runs at 1,200 RPM, consuming nearly 40 kW, while a damper restricts flow.

    With VFD control: Using the affinity laws:

    $$\frac{N_2}{N_1} = \frac{Q_2}{Q_1} = \frac{6{,}000}{10{,}000} = 0.6$$

    $$\frac{W_2}{W_1} = (0.6)^3 = 0.216$$

    $$W_2 = 40 \text{ kW} \times 0.216 = 8.6 \text{ kW}$$

    The VFD approach uses only 8.6 kW instead of 40 kW, a savings of 78%.

### Limitations and Considerations

!!! info "Affinity Law Assumptions"

    The affinity laws assume:

    1. The fan or pump operates on the same system (same ductwork or piping)
    2. Fluid properties remain constant
    3. Efficiency changes with speed are negligible (reasonable approximation for moderate speed changes)

!!! tip

    In real systems, efficiency does change somewhat with speed, but the cubic relationship still dominates. Actual savings may be 5-15% less than predicted by the affinity laws alone, which still represents enormous energy savings.

### Summary: Why Affinity Laws Matter for ITAC Work

The affinity laws are the fundamental reason why VFDs on fans and pumps are among the highest-value energy efficiency measures available. When you evaluate a facility and find constant-speed fans or pumps serving variable loads, you immediately know that VFDs could save 30-70% of the motor energy consumption, depending on the load profile.

Understanding this cubic relationship allows you to:

- Quickly estimate VFD savings potential
- Explain to facility managers why VFDs are worthwhile investments
- Prioritize opportunities (larger motors, more variable loads = bigger savings)
- Recognize when throttling dampers or valves indicate energy waste

## Part 3: Practical Applications

### Identifying Opportunities

When walking through a facility, look for:

**Compressed air systems:**
- Undersized piping (high velocity, pressure drop)
- Audible leaks
- Excessive system pressure (often compensating for distribution losses)

**Pumping systems:**
- Throttled valves (indicating oversized pumps or variable demand)
- Multiple pumps running at low load
- Hot pump motors (friction from excessive flow restriction)

**Fan systems:**
- Dampers in partially closed positions
- Variable air volume systems without VFDs
- Constant-speed fans serving spaces with varying occupancy