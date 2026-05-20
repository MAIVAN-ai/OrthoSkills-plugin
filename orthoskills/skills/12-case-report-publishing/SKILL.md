---
name: ortho-case-report-publishing
description: Use this skill to assemble a structured, publication-ready orthopaedic case report from the case record built by skills 01–11 — combining intake, imaging review, classification (AO/OTA + region-specific), differential reasoning, treatment, implant, outcomes, and aftercare into one coherent document, ready for export to JBJS Case Connector, OrthoWiki, a national registry, or a teaching repository. Trigger this when a user asks to "write up this case", "draft a case report", "export to JBJS", or wants a structured case summary for handover, teaching, MDT, or publication. Educational reference only; not medical advice; patient consent and anonymisation required before any export.
---

# Case Report Publishing

## Purpose

Turn the rich, structured case record built across skills 01–11 into a coherent narrative ready for export — for teaching, MDT, registry submission, or publication. The skill enforces both the narrative quality of a good case report (clear, structured, scientifically honest) and the safety basics (consent, anonymisation, copyright respect).

## When to use

Trigger this skill when:

- A user asks to "write up this case", "draft a case report", "export to JBJS", "create teaching slides from this case"
- A case has reached at least one defined outcome timepoint (most published case reports include at least 3-month follow-up)
- A registry submission window opens

## Workflow

### Step 1 — Verify consent and anonymisation

**Before anything else**, confirm:
- **Patient consent obtained** for case publication (in writing, per local IRB / ethics rules)
- **All identifiers removed** — name, DOB, MRN, exact dates (use intervals), identifying imaging features (visible jewellery, distinctive surgical markings, identifying tattoos in clinical photos)
- **Institution name** — include only with institutional approval

If consent or anonymisation status is unconfirmed, **refuse to proceed** with publication-ready output. Offer to produce a structured internal teaching document instead, clearly marked "not for external distribution".

### Step 2 — Choose the target format

| Target | Format characteristics |
|---|---|
| **JBJS Case Connector** | Academic structure; specific sections (Case, Discussion, Sources of Funding, Disclosure); structured abstract |
| **OrthoWiki / educational platform** | Wiki-style markdown; teaching-focused; figures with annotations |
| **National registry** (e.g. NORE, AOTrauma, country-specific) | Structured form rather than narrative; codes and outcomes |
| **MDT / handover** | Brief, structured, internal-use only |
| **Substack / blog (e.g. Topol-style)** | Narrative, reflective, connecting the case to broader themes; less rigid structure |
| **Teaching slides** | Visual; each slide single point |

Ask the user the target if unclear.

### Step 3 — Assemble the report structure

A canonical structure (for the academic JBJS-style format):

1. **Title** — concise, classification-anchored, e.g. "Reverse-Obliquity Intertrochanteric Fracture (AO/OTA 31-A3) in an Elderly Patient: Management with Long Cephalomedullary Nail and 12-Month Outcome"
2. **Structured abstract** — Background, Case, Outcome, Conclusion (4 short paragraphs)
3. **Introduction** — why this case is worth reporting; the educational point
4. **Case presentation** — from skill 01 intake, anonymised
5. **Imaging and classification** — figures with labels; AO/OTA + region-specific from skills 04, 05
6. **Decision-making** — differentials from skill 06; treatment reasoning from skill 07; implant choice rationale from skill 08
7. **Operative details** — approach, implant class, intra-op findings; **no operative drawings or step-by-step technique** (that's AO Surgery Reference's role)
8. **Post-operative course and aftercare** — from skill 11
9. **Outcomes** — from skill 10, at the defined timepoints; PROMs, union status, complications, mortality
10. **Discussion** — connect to the published literature (skill 09); what does this case add?
11. **Limitations** — single case, retrospective elements, follow-up duration
12. **Conclusion** — the educational take-home
13. **References** — from skill 09's evidence retrieval; only papers actually consulted, no fabricated citations

### Step 4 — Apply the writing-quality checks

| Check | Pass criterion |
|---|---|
| **Anonymisation** | Zero identifiers across narrative, figures, references |
| **Classification accuracy** | AO/OTA + region-specific codes used consistently; surgeon confirmation recorded |
| **Honest uncertainty** | Where differentials existed, surfaced; where evidence is contested, surfaced |
| **Educational point clear** | The "why this case is worth reading" is identifiable in the first paragraph and reinforced in the conclusion |
| **No verbatim AO Compendium text** | The reasoning structure is described; for authoritative classification text the reader is directed to AO Foundation publications |
| **No image copyright violations** | All images are either the authors' own (anonymised), licensed, or used with permission; figure captions name the source |
| **No drug-dosing prescriptions** | Local-protocol-dependent items not specified |
| **Citations real** | Every reference verifiable; no fabricated citations |

### Step 5 — Export

If a connected MCP backend is available:

```
orthoclass.export_case_summary({
  case_id: <id>,
  target: <"jbjs_case_connector" | "orthowiki" | "registry_<name>" | "internal_teaching">,
  format: <"markdown" | "docx" | "pdf" | "structured_form">,
  consent_confirmed: true,
  anonymisation_confirmed: true
})
```

Otherwise, produce the structured output in markdown and instruct the user on the submission pathway.

## Output format

A complete case report in markdown, with the structure above. Example skeleton (filled in by the actual case content):

```markdown
# [Title]

**Authors:** [redacted for example]
**Affiliations:** [redacted for example]
**Corresponding author:** [redacted for example]
**Disclosure:** [funding, conflicts of interest]
**Consent:** Patient consented in writing to the publication of this anonymised case report.

## Structured abstract

**Background.** [1–2 sentences on the clinical context.]
**Case.** [The patient and the injury, in 2–3 sentences, anonymised.]
**Outcome.** [The result at the latest defined follow-up.]
**Conclusion.** [The educational point.]

## Introduction

[The clinical context. Why this case. The literature gap or teaching point.]

## Case presentation

[Anonymised history, mechanism, examination, neurovascular status. From skill 01.]

## Imaging and classification

[Imaging available; views; key findings.]

**AO/OTA classification:** [code, e.g. 31-A3.x, with confidence and differentials from skill 04]
**Region-specific classification:** [e.g. not applicable for trochanteric; or Garden/Pauwels for neck fractures]

[Figure with annotations]

## Decision-making

[Differentials (skill 06); treatment options considered (skill 07); implant selection rationale (skill 08).]

## Operative details

[Approach, implant class, intra-operative findings, reduction quality.]

## Post-operative course and aftercare

[Weight-bearing protocol, milestones, physiotherapy, prophylaxis approach generically described.]

## Outcomes

| Timepoint | Union | Function | PROMs | Complications |
|---|---|---|---|---|
| 6 weeks | Early callus | WBAT, mobilising with stick | — | None |
| 3 months | Progressing | Full WB, no aid | OHS 38/48 | None |
| 12 months | United | Returned to baseline | OHS 41/48; NMS unchanged from pre-injury | None |

## Discussion

[Connect to the published literature: skill 09's evidence retrieval output, properly cited.]

## Limitations

[Single case; specific patient factors; follow-up duration.]

## Conclusion

[The take-home, restated.]

## References

1. [Real citation 1]
2. [Real citation 2]
...
```

## Example

**Input:** Case of 78-year-old (anonymised) with confirmed 31-A3 treated by long CMN, 12-month outcome with OHS 41/48, no complications, NMS unchanged. Consent obtained. Target: JBJS Case Connector.

**Skill response:**

I have a complete case record across skills 01–11 for this case. Before drafting, I'm confirming:

- ✅ **Consent:** confirmed by the case record.
- ✅ **Anonymisation:** the case record was kept on case_id, no PHI. I'll do a final pass to ensure no inadvertent identifiers appear in the narrative.
- ✅ **Classification accuracy:** 31-A3 with surgeon confirmation, no remaining differential at the time of treatment.
- ✅ **Outcome timepoint:** 12 months, with structured outcome data from skill 10.

Drafting now in JBJS Case Connector structure:

---

**Title:**
> *Reverse-Obliquity Intertrochanteric Femur Fracture (AO/OTA 31-A3) in an Elderly Patient: Twelve-Month Outcome After Long Cephalomedullary Nail Fixation*

**Structured abstract:**

*Background.* Reverse-obliquity intertrochanteric femur fractures (AO/OTA 31-A3) have distinct biomechanical features that differentiate them from other trochanteric patterns, with implications for implant selection.

*Case.* We present an elderly patient with a 31-A3 fracture sustained in a low-energy fall, managed with long cephalomedullary nail fixation.

*Outcome.* At twelve months the fracture had united, the patient had returned to her pre-injury mobility (community ambulation with a stick), and the Oxford Hip Score was 41/48 with no change in New Mobility Score from baseline.

*Conclusion.* This case illustrates a typical good-outcome trajectory for 31-A3 managed with a long CMN and supports the surgeon's recognition of the A2/A3 distinction in implant choice.

[…full report drafted out in the structure above…]

---

🩺 *Educational reference only — not medical advice. Case reports are educational artefacts; they do not constitute clinical guidance. Patient consent and anonymisation are mandatory prerequisites for any export.*

## Safety guardrails

- **Consent and anonymisation are gate conditions.** If either is unconfirmed, the skill refuses to produce an external-facing report.
- **No fabricated citations.** Every reference must be real and verifiable.
- **No verbatim AO/OTA Compendium reproduction.** The Compendium is © AO Foundation.
- **No identifying images.** Even with consent, images are scrubbed of identifying features.
- **Honest reporting.** A case with a poor outcome is still valuable; the skill never reframes a poor outcome as a success.
- **Local IRB / ethics requirements** vary; the skill recommends checking the institution's specific rules.
- **Not medical advice.**

## Related skills

- All previous skills (01–11) — feed this skill the structured case content
- `ortho-evidence-retrieval` — provides citations
- `ortho-outcome-measurement` — provides the outcome data
