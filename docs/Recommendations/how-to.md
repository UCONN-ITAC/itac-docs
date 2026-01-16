# How to Write a Recommendation

Every recommendation you write will have the same 5 sections: Summary, Current Practices and Observations, Recommended Action, Anticipated Savings, and Costs and Payback. These sections will never change. You don't need to add or remove sections. Seriously, don't. 

When writing, do all of the math before you begin writing. The purpose of prose (as opposed to strictly calculations) is to provide necessary and useful context. If you don't know the inputs and results of the calculations are, your prose will be less-than-useful. Furthermore, write the Summary section last. In that section, you'll be pulling details from the other sections. Since you're probably not clairvoyant, this would be difficult to write first. 

## General Notes

1. **Be Concise:** Shorter is better. You want your rec to be as short as possible without sacrificing *necessary* information. 
2. **Be Precise:** Don't say vague things. It (a) signals that you don't know what you're talking about and (b) doesn't tell the reader what they need to know. 
3. **Be Correct:** Don't be wrong. If you're unsure about something, ask. 

!!! note
    Recommendations should not be longer than two pages. If they are, it is either because they contain too many irrelevant details (delete these), or there are too many detailed calculations (move these to the appendix).

### Math Style

Writing out equations can be a helpful tool when communicating calculation methodology. However, too many equations makes the text feel inaccessible to people without a strong math background. So, we need to strike a balance. 

A good rule of thumb is that is the equation can be described in a single sentence of normal, everyday English words, it should probably be a sentence. We'll call these equations "trivial." Common examples include simply adding a couple of numbers together or multiplication by a "simple" constant. Examples of trivial equations include: 

$$
\text{Total Cost} = \text{Labor Cost} + \text{Materials Cost}
$$

$$
\text{Materials Cost} = \text{No. of Units} * \text{\$15 per unit}
$$

If your equation includes constants that are commonly referred to as variables ($\pi$, $e$, etc.) or includes repeated multiplication, it should be included either in the text or in the appendix. 

## Summary

This should be the last section you write. It should almost always be four sentences long (one sentence for each other section), followed by the summary table. 

When filling in the summary table, it may seem like your numbers don't fit the headings. They do. Group all consumption charges (Electricity, Natural Gas, etc) under the "Consumption Savings" heading. If there are multiple types of consumption savings, add both on separate lines. All parts of the implementation cost should be summed before entering them in the table. If a given cell doesn't have a value (including if the payback is immediate), keep the two hyphens. 

Use this template for the summary table: 

```latex

\begin{table}[H]
\centering
\caption{Summary of the savings for AR-\themyAR: XXXXX}
\label{tab:latefees}
\begin{tabular}{ccccc}
\toprule
Consumption Savings & Demand Savings & Annual Savings & Implement.\ Cost & Payback \\
\midrule
-- & -- & -- & -- & -- \\
\bottomrule
\end{tabular}
\end{table}

```

## Current Practices and Observations

This section establishes the baseline case: how the facility currently operates with respect to the system or process under consideration. The goal is to give the reader a clear picture of existing conditions before any changes are made.

**What to include:**

1. **Quantitative data:** Present measured values, operating parameters, and relevant metrics collected during the assessment. This includes equipment nameplate data, metered readings, production rates, operating hours, and any other numerical information that characterizes current performance. Establish the baseline that will be used to calculate the savings. 

2. **Qualitative observations:** Describe the physical condition of equipment, operational practices, layout considerations, and any contextual factors that affect system performance. Note visible issues such as leaks, damage, or suboptimal configurations.

3. **Figures and visuals:** Supplement the discussion with photographs, thermal images, diagrams, or charts where they help illustrate the current state. Each figure should have a caption and be referenced in the text.


The baseline established here serves as the reference point for all savings calculations. Be thorough and specific, as reviewers and facility personnel will use this section to verify that the recommendation applies to their situation.


## Recommended Action

This section states what the facility should do. Write as if you are a manager directing employees: clear, authoritative, and focused on the outcome rather than implementation logistics.

**Guidelines:**

- Keep this section concise. It is often the shortest part of the recommendation.

- State the action in direct terms. For example: "Install a 150 kVAR capacitor bank to improve power factor" or "Replace the existing 10 HP motor with a premium efficiency model."

- Do not include sourcing details, installation procedures, or contractor selection. The facility will determine these based on their own procurement processes.

- Avoid naming specific vendors. If a recommendation requires specialized equipment where vendor identification is unavoidable, include at least three options. If fewer than three vendors exist, list all available options and add the following statement: "These mentions are not an endorsement of any product or vendor."


## Anticipated Savings

This section explains both the methodology and the results of your savings calculations. It is typically the longest section of the recommendation.

**Structure:**

1. **Methodology description:** Explain how savings were calculated in terms accessible to someone with introductory engineering knowledge. If the calculations involve complex derivations, advanced equations, or lengthy procedures, summarize the approach here and place the full treatment in an appendix. Reference the appendix explicitly.

2. **Assumptions:** Clearly state all assumptions that materially affect the results. Include operating hours, load factors, efficiency values, production rates, or any other parameters not directly measured. Assumptions should be useful and relevant; do not list trivial or obvious ones.

3. **Energy savings:** Present all savings in their native energy units first. Use kWh for electricity, kW for demand reduction, MMBtu for fuel, and Tgal (thousand gallons) for water. Show the calculations or reference the appendix where they appear.

4. **Cost savings:** Convert energy savings to dollars as the final step, using the utility rates established in the report. This separation ensures transparency and allows the facility to update projections if rates change.

## Costs and Payback

This section itemizes implementation costs and calculates the simple payback period.

**Cost components:**

Break down costs into the following categories, stating each explicitly unless the value is zero:

- **Equipment costs:** Purchase price of hardware, materials, and any required ancillary components.

- **Labor costs:** Installation, commissioning, and any professional services required.

- **Continuing costs:** Ongoing expenses such as maintenance, consumables, or operational changes that differ from the baseline. These are annual figures.

**Utility incentives:**

If the facility qualifies for utility incentives, explain the eligibility criteria and the incentive amount. Subtract incentives from the total implementation cost before calculating payback.

**Payback calculation:**

Subtract any continuing costs from the annual savings to obtain net annual savings. Use the following format for the payback calculation:

```latex
\begin{align*}
\text{Payback Period} &=
\frac{\text{Implementation Cost}}{\text{Annual Savings}} = \frac{\XXImplementation}{\XXTotalSavings} = \textbf{\XXPayback~years}
\end{align*}
```


