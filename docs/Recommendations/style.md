# Recommendation Page Style Guide

> **Internal reference only** — not linked in site navigation.

This guide documents the conventions used across every methodology page in `docs/Recommendations/`. Follow it when writing new pages or editing existing ones so the docs stay consistent.

---

## Frontmatter

Every methodology page starts with the same YAML block:

```yaml
---
hide:
  - toc
---
```

No other frontmatter keys are used.

---

## Page Structure (Methodology Pages)

Methodology pages follow a fixed section order. Not every section appears on every page, but the order never changes.

| Order | Section | Required? | Notes |
|-------|---------|-----------|-------|
| 1 | **H1 Title** | Yes | Single H1; describes the action, not the category |
| 2 | **Intro paragraph** | Yes | 1–3 sentences explaining what the measure is and why it matters |
| 3 | **ARC Code(s)** | Yes | Bold label, e.g. `**ARC Code(s):** 2.4236` |
| 4 | **Background / How It Works** | Sometimes | Only when the reader needs context before the math |
| 5 | **Savings Calculation** | Yes | Core methodology; uses H2 and H3 subsections |
| 6 | **Anticipated Costs** | Yes | Equipment, labor, incentives, payback |
| 7 | **Report Requirements** | Usually | Extra deliverables beyond [how-to.md](how-to.md) |
| 8 | **Interactive Calculator** | Sometimes | Link to a calculator page, always last |

### Title

- Use a single `# H1`.
- Phrase it as an action or noun phrase that tells the reader what to *do*: "Repair Compressed Air Leaks," "Upgrade to Efficient Lighting Fixtures," "Don't Pay Late Fees."
- Don't prefix with the category name (no "Compressed Air: Cold Air Intake").

### ARC Code(s)

- Always bold the label: `**ARC Code(s):** 2.XXXX`
- Place on its own line directly after the intro paragraph, separated by a blank line.
- If listing multiple codes, separate with commas: `**ARC Code(s):** 2.7133, 2.7134, 2.7135`

---

## Headings

- **H1 (`#`)** — page title only; one per page.
- **H2 (`##`)** — major sections: "Savings Calculation," "Anticipated Costs," "Report Requirements," etc.
- **H3 (`###`)** — subsections within a major section: "Annual Energy Savings," "Peak Demand Savings," "Annual Cost Savings," "Methodology," etc.
- Don't skip heading levels.

---

## Prose Style

1. **Be concise.** One or two sentences to set up an equation is enough.
2. **Be precise.** State actual numbers, efficiencies, and operating points; avoid "approximately" or "around" without a specific range.
3. **Use active, direct voice.** "Install a 150 kVAR capacitor bank" — not "It is recommended that a capacitor bank be installed."
4. **Write for an introductory-engineering audience.** Assume the reader knows basic units and concepts but not your specific methodology.
5. **Don't name vendors** unless unavoidable (and if so, list 3+ with a disclaimer).

---

## Equations

### When to Use an Equation

Use a displayed `$$` equation when:

- The formula contains non-trivial constants, subscripts, or repeated multiplication.
- The reader needs to reproduce the calculation.

If an equation can be stated in a single plain-English sentence (adding two numbers, multiplying by a simple constant), **write it as prose instead**.

### Formatting

- Use `$$ ... $$` fenced blocks for displayed equations (never inline `$...$` for standalone formulas).
- Separate the `$$` delimiters from surrounding text with blank lines.
- Use `\text{}` for all descriptive subscripts and labels inside LaTeX: `$Q_{\text{leaks}}$`, not `$Q_{leaks}$`.
- Greek letters and standard math symbols (`\pi`, `\times`, `\frac`) stay un-texted.
- Use `\times` for multiplication in displayed equations, not `*`.
- Where applicable, include units in the subscript or note them in the variable list.

### Variable Lists

Immediately after a displayed equation, define every variable in a **"Where:" list**:

```markdown
Where:

- $Q_{\text{leaks}}$ = total leak flow rate repaired (CFM)
- $H$ = annual leaking hours (hrs/yr)
```

Rules:

- Start with the word `Where:` on its own line, followed by a blank line before the list.
- Each item is a bullet (`-`), starting with the variable in inline math, then ` = ` (space-equals-space), then the plain-English description including units in parentheses.
- List variables in the order they appear in the equation.

---

## Admonitions

Use MkDocs admonition syntax (`!!! type` or `??? type` for collapsible):

```markdown
!!! warning "Optional custom title"

    Body text indented four spaces.
```

| Type | When to Use |
|------|-------------|
| `note` | Helpful context, data source tips, methodology clarifications |
| `warning` | Must-know caveats, calculation traps, verification requirements |

- Keep admonition bodies short (one paragraph preferred).
- Don't stack admonitions back-to-back without intervening content.
- Use collapsible `???` for supplementary details (e.g., where to find CAGI datasheets) that aren't critical reading.

---

## Tables

### Data / Reference Tables

Use standard Markdown pipe tables for reference data, comparison matrices, and parameter look-ups:

```markdown
| Compressor Type | Heat Rejection Factor | Source / Notes |
|---|---|---|
| Lubricant-injected rotary screw | 0.80 to 0.90 | DOE Sourcebook |
```

- Always include a header row and a separator row.
- Left-align text columns; right-align numeric columns when practical.
- Use `--` (two hyphens) for empty cells; never leave a cell blank.

### LaTeX Report Tables

Report Requirements sections include LaTeX table templates for the final report when relevant. Wrap these in fenced `latex` code blocks:

```markdown
```latex
\begin{table}[H]
...
\end{table}
```​
```

- Use `booktabs` commands (`\toprule`, `\midrule`, `\bottomrule`).
- Include a `\caption` and `\label` in every table.
- Show placeholder rows with example location names; use `--` for empty data cells.
- Include a **bold Totals row** separated by `\midrule` at the bottom.

Only include a table when there are multiple pieces of equipment in question. For example, recommendations including several motors, HVAC units, or similar should have a table. Recommendations including a single piece of equipment, or the savings apply to the whole system, not per-equipment (like reducing compressor setpoints), should not have a table.

---

## Anticipated Costs Section

Follow this pattern:

1. **Equipment** costs — describe what is purchased; give per-unit cost or range when possible.
2. **Labor** costs — give time per unit (e.g., "15 minutes per leak," "2–4 hours per motor") at standard rates.
3. **Continuing costs** — only if applicable.
4. **Utility incentives** — mention that the measure typically qualifies; instruct writers to check with the local utility. Subtract incentives before payback.
5. **Payback** — state the typical payback range; include the LaTeX payback formula when provided in [how-to.md](how-to.md).

Use **bold labels** at the start of each item followed by a colon, either as bullet points or as separate paragraphs:

```markdown
**Equipment:** Purchase price of...

**Labor:** Budget 15 minutes per leak at...
```

---

## Report Requirements Section

- Open with the sentence: *"In addition to the [typical report requirements](../how-to.md), the recommendation must include:"* (or slight variation referencing `../how-to.md`).
- List required columns for the summary table using a bulleted list with bold column labels.
- Follow the column list with the LaTeX table template.
- For any extra deliverables (images, screenshots, MEASUR output), list them as bullets.

---

## Interactive Calculator Links

When a page links to a companion calculator, place it at the very end of the page in its own H2 section:

```markdown
---

## Interactive [Name] Calculator

Use the dedicated calculator to...

[Open [Name] Calculator](../../calculators/[slug].md){ .md-button }
```

- Precede the section with a horizontal rule (`---`).
- Use a `.md-button` class on the link.

---

## Assumptions

Whenever a calculation relies on assumed values (operating hours, load factors, efficiency defaults, coincidence factors), list them explicitly under a heading or as a bulleted list labeled **"Important assumptions to state in the analysis:"**:

```markdown
Important assumptions to state in the analysis:

- Baseline belt efficiency: 93%
- Notched V-belt efficiency: 97%
```

---

## Images

- Use `![Alt text](path)` syntax.
- Store images in `docs/assets/docs/`.
- Reference images inline in the text near where they are discussed.

---

## Links

- Cross-reference the how-to guide as `[typical report requirements](../how-to.md)` (always from the page's relative path).
- Link to companion methodology pages when one page's methodology depends on another (e.g., proper-size → high-efficiency).
- Link to external calculators or tools using `.md-button` class.

---

## Common Deviations to Avoid

| ❌ Don't | ✅ Do |
|----------|------|
| Skip the ARC code line | Always include `**ARC Code(s):** ...` |
| Use `$$ ... $$` for trivial arithmetic | Write trivial equations as prose |
| Leave LaTeX table cells blank | Fill empty cells with `--` |
| Stack multiple admonitions with no content between them | Separate admonitions with at least one paragraph |
| Name a specific vendor without alternatives | Provide 3+ vendors or omit vendor names entirely |
| Put the calculator link in the middle of the page | Calculator link is always the last section |
| Use H1 for anything other than the page title | One H1 per page; everything else H2–H4 |
| Write vague cost estimates ("about $500") | Give ranges or per-unit formulas |
| Forget the `hide: toc` frontmatter | Every methodology page hides the ToC |
