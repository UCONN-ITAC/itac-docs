# Distribution

Once compressed air is generated in the compressor room, it must be delivered to end uses throughout the facility. The distribution system—pipes, receivers, valves, and fittings—determines how efficiently that air reaches its destination. Poor distribution design wastes energy through pressure drop and creates the conditions for leaks.

## Pressure Drop in Piping

When air flows through pipes, friction between the air and pipe walls causes pressure loss. This pressure drop must be overcome by the compressor, which consumes additional energy. Minimizing pressure drop is critical for system efficiency.

For a given flow rate, pressure drop varies approximately with the **inverse fifth power** of pipe diameter:

$$\Delta P \propto \frac{1}{d^5}$$

Where:
- $\Delta P$ = Pressure drop
- $d$ = Pipe inside diameter

This relationship means that small reductions in pipe diameter cause dramatic increases in pressure drop.

!!! example

    If you reduce pipe diameter by half (from 2" to 1"), the pressure drop increases by a factor of approximately:

    $$\frac{1}{(0.5)^5} = \frac{1}{0.03125} = 32$$

    The pressure drop becomes **32 times higher**, requiring significantly more compressor energy to maintain the same flow rate.

Even modest undersizing of compressed air piping creates enormous energy waste. Conversely, slightly oversizing pipes costs little in materials but saves substantial energy over the system's lifetime.

Pressure drop depends on:

1. **Flow rate:** Higher flow = higher pressure drop (approximately proportional to flow squared)
2. **Pipe diameter:** Smaller diameter = much higher pressure drop (inverse fifth power)
3. **Pipe length:** Longer pipe = more pressure drop (directly proportional)
4. **Pipe roughness:** Rough interior surfaces increase friction
5. **Fittings and valves:** Each elbow, tee, or valve adds resistance


Compressed air systems are particularly sensitive to pressure drop because:

1. **Air must be compressed to overcome distribution losses:** If the end use needs 70 psig but distribution has 15 psig of pressure drop, the compressor must generate 85 psig. This increases compressor energy consumption by approximately 7-8%.

2. **Compression is energy-intensive:** Generating compressed air requires about 7-8 kW of electricity per 1 HP of compressor capacity. Small pressure increases compound into significant costs.

!!! example

    A facility needs 90 psig at the point of use. If the distribution system has 15 psi of pressure drop, the compressor must produce 105 psig instead of 90 psig.

    Using the rule of thumb that every 2 psig increase costs 1% more energy:

    $$\text{Energy increase} = \frac{15 \text{ psi}}{2} \times 1\% = 7.5\%$$

    For a 100 HP compressor running 6,000 hours/year at $0.12/kWh:

    $$\text{Annual cost} = 100 \text{ HP} \times 0.746 \frac{\text{kW}}{\text{HP}} \times 6{,}000 \text{ hr} \times \$0.12/\text{kWh} \times 0.075 = \$4{,}018/\text{yr}$$

    Simply reducing pressure drop would save over $4,000 per year.

## Storage Receivers

Receiver tanks serve multiple critical functions in compressed air systems. They act as buffers, smoothing out pressure fluctuations when demand varies. Without receivers, cyclic demand creates pressure swings that affect tool performance. They store compressed air to meet short-term peak demands without requiring the compressor to increase output immediately. As compressed air cools in the receiver, condensation forms and collects at the bottom. Receivers should have automatic or manual drains to remove this water.

The rule of thumb for receiver sizing is to store 10 seconds of compressor capacity.

!!! example

    For a 25 HP compressor producing 100 CFM:

    $$\text{Required volume} = \frac{100 \text{ CFM} \times 10 \text{ sec}}{60 \text{ sec/min}} = 16.7 \text{ ft}^3$$

    Converting to gallons (1 ft³ = 7.48 gallons):

    $$\text{Tank size} = 16.7 \times 7.48 = 125 \text{ gallons}$$

    A 130-gallon receiver would be appropriate.

Many facilities use multiple receivers at different locations: a primary receiver near the compressor (wet receiver), secondary receivers near high-demand areas, and point-of-use receivers for equipment with intermittent high demand. Some facilities require that their pressure is artificially high because pressure drops when they turn on specific equipment. However, co-locating a receiver with that equipment is typically a more cost-effective solution.

!!! tip

    If a receiver has a pressure gauge halfway up the tank, and you remove it to install a pressure sensor, water pouring out indicates the tank is full of water. This is surprisingly common and indicates failed condensate drainage.


## Distribution System Assessment

When evaluating a compressed air distribution system during an ITAC assessment, measure pressure at the compressor discharge (or look at the compressor screen) and at various end uses during normal operation. The difference indicates distribution losses. Total distribution pressure drop should be under 5 psi. If pressure drop exceeds this target, identify bottlenecks and look for restrictions. Also evaluate whether pressure swings during demand changes are acceptable and whether pressure drops excessively when high-demand equipment starts.

Common distribution problems include undersized piping (original design for lower capacity, plant added equipment without upgrading pipes), temporary fixes that became permanent (flexible hoses installed for "temporary" connections remain in service for years, creating restrictions and leak points), abandoned equipment still connected (unused machinery remains connected to compressed air, creating potential leak paths), and no pressure regulation at end use (equipment receives full line pressure when lower pressure would suffice, wasting air).

Distribution system inefficiency is often invisible. Unlike a broken tool or a failed compressor, excessive pressure drop simply costs money without creating obvious problems. Systematic measurement and assessment are essential.
