---
hide:
  - toc
---

# Facility Overview

The Facility Overview is the opening section of the assessment report, found under **Report Sections** → **Introduction.tex** in the LaTeX sidebar. It gives the reader a concise sense of who the client is, what they make, and where they operate — without disclosing any identifying details.

## What to Write

Write **1–2 paragraphs** covering the following:

- What the company does and what products or services it provides
- How the facility is organized (production processes, workforce, notable capabilities)
- Any relevant context about scale, history, or market position that helps frame the energy assessment

Utilize information from the company's website and other publicly available sources. **Do not include any identifying information** — no company name, street address, or other details that would identify the client.

The section must include an aerial image of the facility (typically sourced from Google Earth if no other photo is available). Reference it naturally within the text using a phrase such as *"shown in the aerial view in Figure 1"*, *"as seen below in Figure 1"*, or *"please refer to Figure 1"*.


The final sentence of the section is auto-generated from report variables and will read:

     This on-site assessment was conducted on [date], led by ITAC director, Dr. Liang Zhang. ITAC Students who participated in the assessment include [student names].*

You do not write this sentence manually — it is produced by filling in the variables described below.

## Filling In the Date and Students

Navigate to the **Variables** section in the LaTeX sidebar → **Report-Variables.tex** → look for the block marked `% Report and Students %`. Two commands need to be filled in:

**Visit date:**
```latex
\newcommand{\VisitDate}{--}
```
Replace `--` with the date of the assessment, written in the format used consistently across other reports (e.g.,`December 16th, 2025`).

**Student list (for the Facility Overview paragraph):**
```latex
\providecommand{\StudentList}{Student 1, Student 2, Student 3}
```
Replace the placeholder names with a comma-separated list of **all students who attended the assessment**, including the student lead and safety lead. This list appears in the auto-generated closing sentence of the Facility Overview.

**Warning! "StudentList vs. StudentRows":**

  `\StudentList` (used here) includes **everyone** — the student lead, safety lead, and all other students.
    
   `\newcommand{\StudentRows}` is a separate command used elsewhere in the report and contains only the students who are **not** the student lead or safety lead. See the [Filling Out Variables](../variables.md) section for a full explanation of both.


## Tips for writing the paragraphs
- Lead with what the company makes and who they serve. Mention any distinctive process features (e.g., solvent recovery, tool room, smart manufacturing investments) that are relevant context to the energy assesment.
- Avoid generic filler phrases. If the company has been operating for decades or has a notable market position, say so specifically.
- Keep it factual and neutral — this is not a sales pitch. One tight paragraph is often better than two loose ones.
