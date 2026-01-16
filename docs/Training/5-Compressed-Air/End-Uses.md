# End Uses

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; margin-bottom: 1em;">
  <iframe style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="https://www.youtube-nocookie.com/embed/7o1BlPfzY-Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

The demand side of a compressed air system determines how efficiently compressed air is used. While supply-side improvements (better compressors, controls, dryers) are important, reducing inappropriate demand and eliminating waste often provides the quickest payback.

## Artificial Demand

**Artificial demand** is the extra loss associated with operating the system at higher pressure than necessary. When system pressure is 100 psig but end uses only need 75 psig:

1. Leaks flow at higher rates (when measured in SCFM)
2. Unregulated uses consume more air
3. Compressor energy increases by ~1% per 2 psig

Reducing system pressure from 100 psig to 75 psig can reduce total compressed air consumption by 15-20%.

## Appropriate Compressed Air Applications

Compressed air is well-suited for certain applications where its unique properties provide value.

Pneumatic tools include grinders, sanders, nail guns, impact wrenches, drills, and cutoff wheels. Compressed air tools offer several advantages over electric equivalents: lighter weight (no heavy electric motor in the tool), better power-to-weight ratio, precise speed and torque control, no electrical shock hazard in wet or hazardous environments, and simpler construction (fewer parts to fail). Hand tools consume anywhere from 3-15 CFM depending on size and type. A 1/2" impact wrench might use 5-7 CFM, while a large grinder could use 12-15 CFM. Best practice is to match tool pressure requirements to supply pressure. Many tools work fine at 70-80 psig, yet facilities often supply 100+ psig, wasting air.

Pneumatic actuators move, position, and manipulate materials during manufacturing. They include linear actuators (extending/retracting cylinders), rotary actuators (rotating motion), grippers (pick and place operations), and diverters (route products on conveyor lines). A single packaging line might use 15-20 different actuator types to handle, position, orient, and move products through the process. Pneumatic actuators offer compact size for the force generated, smooth controlled motion, precise positioning, and fail-safe operation (loss of air pressure stops motion). These uses are typically non-negotiable. Process requirements dictate actuator use, and replacing them isn't practical. The focus should be on ensuring they operate at appropriate pressure and don't waste air when idle.

Legitimate specialized uses include air knives (blow liquid or debris off products in food processing, parts washing, and web drying), spot coolers (use vortex tubes to create cold air streams for localized cooling), aeration and mixing (bubble air through liquids for mixing, oxygenation in wastewater treatment, or chemical reactions), sandblasting (propel abrasive media to clean, deburr, or prepare surfaces for painting), spray painting (atomize paint into fine droplets for even application), and blow molding (form plastic containers by inflating heated plastic inside molds). These applications are appropriate when no reasonable alternative exists or when compressed air provides specific benefits (cleanliness, precision, safety).

## Inappropriate Compressed Air Uses

Compressed air is expensive to produce—roughly 7-8 times more expensive per unit of energy delivered than electricity. Using compressed air when alternatives are available wastes money.

Workers sometimes blow compressed air on themselves for cooling in hot facilities. A small fan uses a fraction of the energy and provides better airflow. A compressed air nozzle delivering 20 CFM at 90 psig might cost $10/hour to operate, while a small fan costs pennies. Provide portable fans, improve facility ventilation, or use evaporative cooling systems instead. Compressed air blown on skin can cause injury. OSHA limits compressed air for cleaning purposes to 30 psig, and it should never be directed at people.

Compressed air nozzles sometimes blow continuously to keep dust off products, dry parts after washing, or clear debris from workstations. Continuous operation means air flows 24/7, even when not needed. Compressed air costs approximately $0.25 per 1,000 cubic feet, so continuous 10 CFM use costs about $3.50 per day or $1,300 per year. Use electric fans or blowers for airflow (1/10 the energy cost), interlock with equipment to only activate when product is present, use air knives instead of open nozzles (more efficient for surface drying), or use vacuum systems for dust removal. Occasional blow-off for workbench cleaning is fine. Continuous 24/7 operation is not.

Pneumatic motors sometimes drive mixers, conveyors, or other continuous-duty equipment. Air motors are about 10-30% efficient at converting compressed air energy to mechanical work. Electric motors are 85-95% efficient. For the same mechanical output, air motors cost 10 times more to operate. Air motors are appropriate in hazardous environments where electric sparks are dangerous (flammable atmospheres), washdown environments (food processing, pharmaceuticals), or applications requiring variable speed control without electronics (though VFDs now make electric motors competitive). Replace air motors with electric motors except in genuinely hazardous or washdown applications.

Equipment no longer in use sometimes remains connected to compressed air lines. Compressed air continues to flow to these devices, leaking at disconnects, regulators, and tool inlets, with airflow continuing 24/7 even though equipment produces nothing. Valve off any equipment not in current use. Install shut-off valves on branch lines so unused sections can be isolated.

## Air Leaks

Air leaks are the single largest source of waste in most compressed air systems, accounting for 20-30% of total compressed air production. The rule of thumb is that 1 CFM of air leakage costs approximately $80-100 per year (assuming $0.12/kWh electricity, 6,000 operating hours, and 100 psig system pressure).

!!! example

    A facility with a 100 HP compressor producing 400 CFM has 25% leakage (100 CFM). Annual leak cost:

    $$100 \text{ CFM} \times \$80/\text{CFM-year} = \$8{,}000/\text{year}$$

    If electricity costs $0.15/kWh instead of $0.12/kWh, the cost rises proportionally.

Leaks are difficult to quantify individually because they experience choked flow (sonic velocity through the orifice), making leak rate dependent on hole size (as long as pressure is sufficiently high). That's why we have an Ultrasonic Imager. Leaks occur primarily at joints and fittings, quick connects, and valves, so our studies usually focus on these locations. 

The most practical approach for quantifying overall leakage is system-wide measurement. Shut down all production equipment and measure how long it takes for system pressure to drop from max to min (or measure compressor cycle time). Alternatively, install flow meters on distribution branches, isolate a section, turn off all known uses, and measure residual flow. This is leakage. Best practice is to achieve leakage under 10% of system capacity.

The other method we use is examining compressor power when no loads on the system are active. Using a CAGI datasheet, we can equate power input to CFM delivered, providing an alternate route to estimate leak rates.

Effective leak management requires continuous vigilance, not one-time fixes. Leaks reappear constantly due to vibration loosening fittings, thermal cycling (expansion/contraction), equipment modifications creating new connections, and aging components (seals, valves). Elements of a successful program include regular surveys (monthly or quarterly leak detection surveys using ultrasonic detectors), tagging identified leaks with date, location, and estimated size, logging repairs and verifying fixes, assigning leak detection and repair to specific personnel or contractor, and tracking leakage as percentage of production capacity. Many facilities lack time or expertise for effective leak management. Third-party services specialize in leak detection and repair, often on a performance contract basis.

## Demand-Side Assessment Approach

When evaluating compressed air end uses during an ITAC assessment, walk the plant and categorize compressed air applications (production actuators and tools, continuous blow-off or drying, air motors, idle or abandoned equipment). For each inappropriate use, ask: Can a fan or blower replace it? Can an electric motor replace an air motor? Can the application be eliminated entirely? Can it be interlocked to operate only when needed?

Conduct system-wide leak assessment to calculate estimated system leak rate, perform ultrasonic survey to identify major leaks, and calculate annual cost of leakage. Check operating pressures: What pressure do end uses actually require? Can system pressure be reduced?