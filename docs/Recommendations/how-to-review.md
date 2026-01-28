# How to Review a Recommendation

Reviewing recommendations is a critical quality control step that ensures technical accuracy, completeness, and professional presentation before submission to facilities. Your job is to verify that the recommendation follows established methodologies, contains accurate calculations, and clearly communicates actionable information. Substantive errors (calculation errors, methodology deviations, data inconsistencies) require a virtual meeting with the author to discuss corrections. Non-substantive changes (spelling, grammar, formatting) can be documented in written feedback.

## General Principles

1. **Be Thorough:** Check every calculation, assumption, and claim. If you cannot reproduce a result using the stated methodology and assumptions, it requires correction.

2. **Be Constructive:** Frame feedback as opportunities for improvement, not criticism. Remember that the goal is to help the author produce excellent work, not to find fault.

3. **Be Methodical:** Follow the same order every time. Use the section-by-section checklist below to ensure consistent, complete reviews.

!!! warning
    The checkboxes on this page are clickable. However, if you refresh the page, they will reset. Do with this what you will. 

## High-Level Review Checklist

Before diving into section-by-section review, verify these overarching elements:

- [ ] **Correct ARC code(s)** referenced and matches recommendation type
- [ ] **Methodology follows** the appropriate page
- [ ] **All calculations are reproducible** from stated assumptions and methodology
- [ ] **Recommendation reflects facility reality** based on assessment observations
- [ ] **Length is appropriate** (maximum 2 pages; appendix for detailed calculations if needed)
- [ ] **Tone is professional** and uses active voice
- [ ] **No vendor-specific language** (if unavoidable, 3+ options with disclaimer)
- [ ] **Utility incentives researched** and documented if applicable
- [ ] **All figures referenced** in text and properly captioned
- [ ] **Units are correct and consistent** throughout
- [ ] **Correct variables** are used where needed

!!! warning "Virtual Meeting Requirement"

    If you identify any of the following, schedule a virtual meeting with the author immediately:

    - Calculation errors or unreproducible results

    - Methodology that deviates from established docs/Recommendations/[category] guidance

    - Missing or incorrect data that affects savings estimates

    - Assumptions that don't match facility conditions observed during assessment

    - Incomplete baseline documentation

    - Cost estimates that appear significantly incorrect

## Section-by-Section Review

### Summary

The Summary should be written last by the author, so it should synthesize information from all other sections accurately.

**Review checklist:**

- [ ] **Four sentences:** One summarizing each of the four main sections (Current Practices, Recommended Action, Anticipated Savings, Costs and Payback)
- [ ] **Summary table present** and correctly formatted using the standard LaTeX template
- [ ] **Summary table values match** calculations in other sections
- [ ] **Consumption savings** grouped correctly (all energy types under "Consumption Savings")
- [ ] **Implementation cost** is the sum of all components (equipment + labor - incentives)
- [ ] **Payback calculation** matches: (Implementation Cost) / (Annual Savings - Continuing Costs)
- [ ] **Empty cells** contain two dashes (--), not left blank
- [ ] **AR number** in table caption matches recommendation

**Common issues:**

- Summary table numbers don't match detailed calculations (requires virtual meeting)

- Payback calculated incorrectly when continuing costs are present

- Forgetting to subtract utility incentives from implementation cost

---

### Current Practices and Observations

This section establishes the baseline. Everything here should be verifiable from assessment data, measurements, or facility documentation.

**Review checklist:**

- [ ] **Quantitative baseline data** is specific and complete (equipment nameplate data, measured values, operating parameters)
- [ ] **Operating hours** are clearly stated and reasonable for the facility's production schedule
- [ ] **Baseline efficiency values** have sources cited (nameplate, manufacturer spec sheet, NEMA standards, etc.)
- [ ] **Load factors** documented when relevant (e.g., motors should run at adequate load for efficiency upgrades)
- [ ] **Qualitative observations** describe physical condition, layout, and operational context
- [ ] **All figures referenced** in text with descriptive captions
- [ ] **No vague language** (avoid "approximately," "around," "about" without specific ranges)

**Red flags to watch for:**

- Missing efficiency sources (e.g., "existing motor is 85% efficient" with no citation)

- Baseline conditions that don't match facility observations from the assessment

- Averaged data used when monthly variation is significant

- Missing baseline data required by the methodology (e.g., power factor for utility measures, demand charges, etc.)

!!! note "What to Include"
    If a piece of facility data is used to calculate savings, it should be included here. 

!!! warning "Baseline Documentation Standards"

    The baseline must be detailed enough that someone reading the recommendation years later can understand exactly what conditions existed before implementation. If you cannot reproduce the baseline scenario from the documentation provided, the section needs revision.

---

### Recommended Action

This section should be concise and direct. 

**Review checklist:**

- [ ] **Action stated clearly** in direct terms (e.g., "We recommend installing a 150 kVAR capacitor bank")
- [ ] **Specific equipment identified** with relevant specifications (HP, efficiency rating, capacity, etc.)
- [ ] **No vendor names** unless unavoidable (and if so, 3+ options with disclaimer that we don't endorse)
- [ ] **No sourcing or installation logistics** included (facility handles procurement)

**Common issues:**

- Too much detail about installation procedures or contractor selection

- Recommended equipment doesn't match the capacity/specifications used in savings calculations

- Action is vague (e.g., "Improve lighting efficiency" instead of "Replace 47 T8 fluorescent fixtures with LED high bay fixtures")

---

### Anticipated Savings

This is typically the longest section and requires the most careful review. You must verify that calculations are mathematically correct and follow the established methodology.

**Review checklist:**

- [ ] **Methodology description** is clear and references the appropriate docs page
- [ ] **Complex calculations** moved to appendix **with explicit reference**
- [ ] **All assumptions listed** explicitly (operating hours, load factors, efficiency values, rates, etc.)
- [ ] **Assumptions are reasonable** and match facility conditions
- [ ] **Energy savings** presented in native units first (kWh, kW, MMBtu, Tgal)
- [ ] **Cost savings** calculated separately as final step using facility utility rates
- [ ] **All calculations reproducible** from stated inputs and methodology

**Calculation verification process:**

1. **Identify the measure category** and locate the corresponding methodology page. 

2. **Verify methodology alignment:**
    - Compare the recommendation's calculation approach to the methodology page
    - Check that all required formulas are used correctly

3. **Check the math:**
    - Reproduce calculations independently using stated inputs
    - Verify unit conversions 
    - Check that intermediate results are carried through correctly

**Red flags for calculations:**

- Results that seem too good to be true (extreme energy savings without extraordinary circumstances)

- Operating hours >8,760 hours/year (impossible)

- Efficiency values that don't make physical sense (e.g., >100% unless dealing with heat pumps)

- Missing secondary effects when methodology requires them

- Demand savings calculated without accounting for seasonal or temporal variations

- Month-by-month analysis missing when required by methodology

!!! warning "Calculation Errors Require Virtual Meeting"

    Any mathematical error, unreproducible calculation, or methodology deviation requires a virtual meeting. Do not attempt to fix calculation errors in written feedback alone. Discuss the approach with the author to ensure they understand the correct methodology.

---

### Costs and Payback

This section itemizes implementation costs and calculates simple payback. Verify that cost estimates are reasonable and complete.

**Review checklist:**

- [ ] **Equipment costs** itemized and sourced (quotes preferred, or industry estimates)
- [ ] **Labor costs** included with reasonable hour estimates
- [ ] **Continuing costs** documented if applicable (maintenance, consumables, operational changes)
- [ ] **Utility incentives researched** and documented with eligibility criteria
- [ ] **Incentives subtracted** from implementation cost before payback calculation
- [ ] **Payback formula correct:** (Implementation Cost) / (Annual Savings - Continuing Costs)
- [ ] **Payback uses LaTeX format** from how-to.md template
- [ ] **Cost estimates are reasonable** for the measure type and scale

**Common issues:**

- Not accounting for continuing costs in payback denominator

- Equipment costs that seem unrealistic (too low or too high) without explanation

- Missing labor costs or unrealistic labor hour estimates

- Labor costs and equipment costs not listed separately

- Utility incentive eligibility not verified with local utility program


!!! note "Utility Incentive Research"

    Most utility energy efficiency programs offer prescriptive rebates for common measures (motors, lighting, HVAC, compressed air, power factor correction). The reviewer should verify that the author has researched applicable incentives. If no incentives are mentioned for a typically-qualifying measure, ask the author if they checked with the local utility.

---

## Documenting Feedback

After completing your review, organize feedback into two categories:

### Substantive Issues (Requires Virtual Meeting)

Document these issues clearly and schedule a virtual meeting with the author to discuss:

- List each substantive issue with specific location references (section name, paragraph, equation number)

- Note what the issue is and why it matters (easiest to do with Overleaf comments)

**Example substantive feedback documentation:**

> **Anticipated Savings Section - Cooling Effect Calculation**
>
> The cooling effect calculation appears to be missing or incorrectly applied. According to the [LED methodology page](Lighting/led.md), lighting upgrades in conditioned spaces should include cooling load reduction calculations. The current recommendation only shows lighting energy savings without the cooling component.
>
> This affects both the energy savings and demand savings calculations. Let's discuss the correct approach in our meeting, including how to determine the appropriate cooling fraction F based on the building characteristics.

### Non-Substantive Issues (Written Feedback)

For spelling, grammar, formatting, and style issues, provide clear written feedback that the author can address independently:

- Use track changes or comment features in document review tools
- Be specific about what needs to change
- Provide corrected text for typos and grammar issues
- Note formatting inconsistencies with references to style guide

**Example non-substantive feedback:**

> - Page 2, paragraph 3: "effeciency" → "efficiency"
> - Summary section: Add comma after introductory phrase: "By replacing the motor, the facility will save..."
> - Figure 2 caption: Not referenced in text. Add reference in Current Practices section.
> - Table formatting: Use two dashes (--) for empty cells instead of leaving blank

---

## Reviewer Qualifications

Effective recommendation reviewers should have:

1. **Technical understanding** of the measure category being reviewed (motors, lighting, HVAC, compressed air, utility, etc.)

2. **Familiarity with methodologies** documented in docs/Recommendations/[category] pages

3. **Attention to detail** sufficient to catch calculation errors and inconsistencies

4. **Assessment context** - ideally, reviewers should have participated in the facility assessment or reviewed assessment notes to understand facility-specific conditions

5. **Communication skills** to provide constructive, clear feedback that helps authors improve

!!! note "Learning Through Review"

    Reviewing recommendations is an excellent way to learn proper methodology and identify common pitfalls. If you're reviewing a measure type you're less familiar with, spend extra time with the corresponding methodology page and don't hesitate to consult with more experienced team members when you have questions.

---

## Review Timeline

Complete reviews promptly to avoid bottlenecks in the assessment report production process:

- **Initial review:** Within 3 days of receiving the recommendation
- **Virtual meeting:** Schedule within 2 business days of identifying substantive issues
- **Follow-up review:** Within 1 business day of receiving revised recommendation

If you cannot meet these timelines due to workload or other commitments, communicate with the author and your supervisor immediately so work can be reassigned if necessary.
