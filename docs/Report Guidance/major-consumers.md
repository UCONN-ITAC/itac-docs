---
hide:
  - toc
---

# Major Energy Consumers

This section has two parts that must both be filled in:

- **Report Sections → Major-Consumers.tex** — the main body section, with a summary table and short paragraphs on each applicable system
- **Appendices → Major-Systems-App.tex** — the detailed appendix write-up for each system

---

## Major-Consumers.tex

This section opens with a summary table (Table 1 in the report) listing every major energy-consuming system at the facility along with a brief description and estimated energy intensity. Below the table, each system gets its own short paragraph with more detail.

**Delete any system that does not apply to this facility.** If a system is present at the facility, it must be included here even if it is not the subject of any recommendation.

### Summary Table

For each applicable system, fill in:

- **Description** — what the system does and how it is used at this facility (1–2 sentences)
- **Estimated Energy Intensity** — the approximate power or heat load of the system, in the correct units:

| System | Units |
|---|---|
| Machines | kW (electric) |
| Compressed Air | kW (electric) |
| Boilers/Steam | MMBtu/hr (fuel) |
| Process Heat | MMBtu/hr (fuel) |
| Process Cooling | kW (electric) |
| HVAC | kW (electric) and/or MMBtu/hr (fuel) |

Energy intensity values typically come from nameplate data.

### System Paragraphs

Below the table, each system present at the facility gets a `\paragraph{}` entry. Write 2–4 sentences covering:

- What equipment makes up this system (make, model, quantity if known)
- How and when it is used in the production process
- Any observed operational details relevant to energy use (operating pressure, temperature, setpoints, scheduling, condition)

Keep these paragraphs factual and observational — this is not the place for recommendations. More detailed technical information belongs in the appendix (see below).


---

## Major-Systems-App.tex

The appendix contains one subsection per system type. These subsections provide full technical detail on each system.

Navigate to **Appendices → Major-Systems-App.tex**. The available subsections are:

- `\subsection*{Compressed Air}`
- `\subsection*{Boilers/Steam}`
- `\subsection*{Process Heat}`
- `\subsection*{Chillers/Process Cooling}`
- `\subsection*{Lighting}`
- `\subsection*{Onsite Generation}`
- Additional systems can be added under `%%% Other`

**Delete any subsection that does not apply to this facility**, consistent with what was kept in the Major-Consumers section.

For each subsection that remains, write a detailed description of the system covering:

- Equipment inventory (quantity, manufacturer, model, rated capacity, age/condition if known)
- Operating parameters (pressure, temperature, flow rates, setpoints)
- Controls and scheduling
- Distribution layout or system configuration where relevant
- Any observations from the walkthrough that characterize how the system is currently operating


Every system included in the summary table in Major-Consumers.tex must have a corresponding subsection in Major-Systems-App.tex, and vice versa. 
