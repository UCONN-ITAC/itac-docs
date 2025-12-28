# Technical Writing

## Introduction

Technical writing is about making an argument, not transferring information onto a page. Every assessment recommendation should have a thesis and build a case for it. "Informative" writing without a point of view produces reports that get skimmed, filed, and forgotten. Your goal is to convince someone to take action.

This document covers the principles and conventions that govern technical writing at ITAC.

## Core Principles

### Concise, Precise, and Right

These three words should guide every sentence you write.

**Concise** means eliminating unnecessary words. If a sentence works without a word, delete that word. If a paragraph works without a sentence, delete that sentence.

**Precise** means using specific numbers and avoiding vague qualifiers. "Significant energy savings" means nothing. "Annual savings of 47,000 kWh ($5,640)" means something.

**Right** means verifying everything. Check your calculations. Confirm your unit conversions. Validate your data sources. A single error undermines the credibility of your entire report.

### Tell a Story, Make an Argument

Every assessment recommendation follows the same narrative structure: here is a problem, here is the evidence that the problem exists, here is a solution, here is why the solution works, and here is why you should implement it.

Do not simply present data and leave interpretation to the reader. Draw conclusions. Make recommendations. Take a position and defend it.

## Voice

### Person and Perspective

Never use first person singular. "I observed" and "I recommend" are not appropriate in technical reports.

Collective "we" is acceptable when representing the assessment team: "We measured the compressed air pressure at three locations" or "We recommend installing VFDs on the cooling tower fans."

When possible, use constructions that focus on the work itself rather than who performed it: "Measurements were taken at three locations" or "The data indicate a 15% efficiency loss."

### Active vs. Passive Voice

Passive voice has its place in technical writing, but overuse makes prose weak and evasive.

| Passive (weaker) | Active (stronger) |
|------------------|-------------------|
| It was found that the boiler efficiency was below expected levels. | The boiler operates at 76% efficiency, below the expected 82%. |
| The recommendation is made that VFDs should be installed. | We recommend installing VFDs on all three pumps. |
| Energy savings of $4,200 annually would be achieved. | This measure saves $4,200 annually. |

Use passive voice when the actor is unknown, unimportant, or when you want to emphasize the action over the actor. Use active voice everywhere else.

### Hedging Language

Hedging undermines your recommendations. If you have done the analysis and the numbers support your conclusion, state it directly. AI models do this a lot. Don't be like ChatGPT. 

| Hedging (weaker) | Direct (stronger) |
|------------------|-------------------|
| It appears that there may be an opportunity to potentially reduce energy consumption. | Replacing the current motor with a premium efficiency model reduces energy consumption by 12%. |
| It is possible that some savings could be achieved. | This measure saves 23,000 kWh annually. |
| The facility might want to consider looking into LED lighting. | We recommend replacing all T8 fluorescent fixtures with LED panels. |

Reserve hedging language for situations with genuine uncertainty, and quantify that uncertainty when possible: "Savings estimates range from $3,200 to $4,800 depending on production levels."

## Audience Awareness

Your reports serve multiple audiences with different needs and technical backgrounds.

### Executive Summary

The executive summary must be accessible to anyone, regardless of technical background. A plant manager, a CFO, or an operations director should be able to read the summary and understand the key findings, recommendations, and financial implications.

Avoid jargon and technical terms in the summary. If you must use a technical term, provide a brief explanation. Focus on outcomes (cost savings, payback periods, implementation costs) rather than technical details.

**Example (too technical for summary):**
"Installation of variable frequency drives on the 50 HP centrifugal pumps serving the chilled water loop will reduce affinity law losses during part-load operation."

**Example (appropriate for summary):**
"Installing variable speed controls on the chilled water pumps saves $8,400 annually by reducing electricity consumption when full pump speed is not needed. The project costs $12,000 and pays for itself in 1.4 years."

### Technical Sections

The other sections of recommendations can assume the reader holds a general engineering degree. You do not need to explain fundamental concepts like heat transfer, fluid dynamics, or electrical power relationships. You should explain your specific assumptions, data sources, and methodology clearly enough that another engineer could reproduce your analysis.

## Figures and Tables

Figures and tables are useful tools for technical communication. However, they should support your argument, not exist as decoration. Before including a visual, ask: what point does this help me make? If you cannot answer that question, reconsider whether you need it. Furthermore, every figure and table must be referenced in the body text. The reader should never encounter a figure or table without context. If there's not a natural place to reference it, it is probably relevant enough to be included. 


### Captions

Captions should be descriptive enough to stand alone. A reader skimming the report should understand what a figure shows without reading the surrounding text.

**Weak caption:**
"Figure 3: Boiler data"

**Strong caption:**
"Figure 3: Boiler stack temperature and combustion efficiency measurements, showing efficiency drop from 82% to 76% as excess air increases"

## Common Pitfalls

### Burying the Lead

State your main point early. Do not make the reader wade through background, methodology, and data before discovering your conclusion.

**Burying the lead:**
"The assessment team measured compressed air pressure at 12 locations throughout the facility. A data logger was installed on the main header for a period of two weeks. Analysis of the pressure data revealed fluctuations between 95 and 142 psi. Industry standards recommend maintaining pressure within a 10 psi band. The wide pressure variation suggests that there may be opportunities to improve system control. We recommend installing a pressure/flow controller."

**Leading with the point:**
"We recommend installing a pressure/flow controller on the compressed air system. Current pressure fluctuates between 95 and 142 psi, well outside the 10 psi band recommended by industry standards. A controller would stabilize pressure, reduce compressor cycling, and save an estimated 45,000 kWh annually."

### Vague Quantification

Words like "significant," "substantial," "considerable," and "major" mean different things to different people. Replace them with numbers.

| Vague | Specific |
|-------|----------|
| The facility uses a significant amount of compressed air. | The facility uses 850 scfm of compressed air during peak production. |
| There is substantial heat loss through the roof. | Heat loss through the uninsulated roof sections totals 1.2 MMBtu/hr. |
| The lighting upgrade offers considerable savings. | The lighting upgrade saves 112,000 kWh and $13,400 annually. |

### Unsupported Claims

Every claim should trace back to a measurement, calculation, or credible source. If you state that a boiler operates at 76% efficiency, the reader should be able to find your combustion analysis data. If you claim a measure saves $15,000 annually, the calculation should be documented.

## Before and After Examples

### Example 1: Compressed Air Leak Assessment

**Before (weak):**
"During the assessment, it was observed by the assessment team that there appeared to be several compressed air leaks in various locations throughout the facility. These leaks are potentially causing the compressors to run more than might be necessary. It is recommended that the facility consider implementing a leak detection and repair program that could  reduce compressed air energy consumption by a significant amount."

**After (strong):**
"We identified 23 compressed air leaks during the ultrasonic survey, representing an estimated 145 scfm of wasted capacity. At the facility's electric rate of $0.09/kWh and 6,500 annual operating hours, these leaks cost $12,300 per year. We recommend repairing all identified leaks and establishing a quarterly leak survey program. Repair costs are are estimated to be $3,000, and the project pays for itself within three months."

### Example 2: Lighting Recommendation

**Before (weak):**
"The facility currently uses older lighting technology in the warehouse areas. Newer LED lighting options are available that use less energy. It might be beneficial for the facility to look into upgrading some or all of the warehouse lighting to LEDs at some point in the future, as this could result in energy savings."

**After (strong):**
"The 48,000 square foot warehouse uses 156 T8 fluorescent high-bay fixtures operating 4,380 hours annually. Replacing these with LED high-bay fixtures reduces lighting power from 89 kW to 42 kW and saves 206,000 kWh ($18,500) per year. At an installed cost of $31,200, the project has a simple payback of 1.7 years. LED fixtures also reduce maintenance costs by eliminating lamp and ballast replacements."

### Example 3: Motor Replacement

**Before (weak):**
"There is a motor in the machine shop that is quite old. Old motors tend to be less efficient than newer motors. The facility may want to consider replacing this motor with a more efficient one, which would probably save some energy."

**After (strong):**
"The 30 HP motor driving the machine shop exhaust fan is original equipment from 1987 and operates at an estimated 88% efficiency. Replacing it with a NEMA Premium efficiency motor (94.1% efficiency) saves 8,900 kWh ($800) annually. The motor operates 6,200 hours per year at an average load of 72%. At a cost of $1,850 installed, the project has a simple payback of 2.3 years. We recommend scheduling replacement during the next planned maintenance shutdown."