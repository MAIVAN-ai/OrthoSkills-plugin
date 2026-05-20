---
name: ortho-evidence-retrieval
description: Use this skill any time a case discussion needs current literature, registry evidence, or guideline references — for a classification, a treatment option, an implant comparison, or an outcome question. The skill builds well-formed queries for PubMed, Consensus, AO Surgery Reference, JBJS case literature, and (when available) the ORTHO-X internal evidence base and national orthopaedic registries, using classification codes (AO/OTA + region-specific) as the primary search key. Trigger whenever a "what does the evidence say about X" question arises, when treatment mapping (skill 07) or implant selection (skill 08) needs supporting literature, or when a case report (skill 12) needs citations. Educational reference only; not medical advice.
---

# Evidence Retrieval

## Purpose

Bridge the gap between a structured classification and the published evidence. Most orthopaedic decisions are supported by a meaningful body of literature — but it's scattered, paywalled, and inconsistently retrievable. This skill builds query patterns that surface the relevant evidence efficiently, using the classification codes as the structured search key.

This skill is the **evidence-search composer**, not a replacement for reading the papers.

## When to use

Trigger this skill when:

- A user asks "what does the evidence say about X" — for a classification, treatment, implant, or outcome
- Skill 07 (Treatment Mapping) or skill 08 (Implant Selection) is surfacing options and the user wants current supporting evidence
- Skill 12 (Case Report Publishing) needs citations
- A registry or PMCF question is being asked ("what's the cut-out rate of CMN in 31-A3 in elderly patients?")

## Workflow

### Step 1 — Identify the question type

| Question type | Examples |
|---|---|
| **Classification methodology** | "Inter-observer reliability of Garden classification" |
| **Treatment comparison** | "CMN vs DHS in 31-A2 intertrochanteric fractures" |
| **Implant performance** | "Cut-out rate of cephalomedullary nails in osteoporotic bone" |
| **Prognosis / natural history** | "AVN rate after Garden III femoral neck fixation" |
| **Specific complications** | "Peri-implant fracture rate, short vs long CMN" |
| **Guideline / consensus** | "NICE hip fracture guideline 2023 update", "AAOS clinical practice guideline" |
| **Anatomy / approach** | "Posteromedial approach for tibial plateau posteromedial fragment" |
| **Outcome measures** | "Harris hip score after hemiarthroplasty for displaced femoral neck" |

### Step 2 — Build the search across sources

Different sources answer different questions. Use the appropriate target for the question type.

| Source | Best for | Example query strategy |
|---|---|---|
| **PubMed** | Primary literature, RCTs, meta-analyses | MeSH terms + classification code + outcome term + filters (RCT, last 5 years, English) |
| **Consensus** (consensus.app) | Question-answering across the literature | Plain-English clinical question |
| **Cochrane Library** | Systematic reviews | Topic terms + "systematic review" |
| **AO Surgery Reference** (free) | Surgical technique, approach, fixation | Region + pattern + approach |
| **AO Foundation publications** | Classification (authoritative) | Region + AO/OTA segment |
| **JBJS Case Connector** | Case-level reasoning | Classification + complication or unusual feature |
| **National registries** (Swedish Hip, Norwegian Arthroplasty Registry, AOANJRR, NJR, etc.) | Real-world outcomes at scale | Implant class + procedure + outcome term |
| **NORE / Trauma registries** | European Orthopaedic Research Group, trauma-specific registries | Trauma pattern + outcome |
| **ORTHO-X internal evidence base** (when available) | Curated, classification-keyed summaries | Direct classification lookup |
| **Local protocols / hospital pathways** | Institution-specific guidance | (Outside this skill's scope; surgeon's local knowledge) |

### Step 3 — Compose the queries

**PubMed query pattern (illustrative — adapt with MeSH terms as needed):**
```
("hip fractures"[MeSH] OR "femoral neck fractures"[MeSH])
AND ("Garden classification" OR "displaced femoral neck")
AND ("hemiarthroplasty"[MeSH] OR "total hip replacement")
AND ("randomized controlled trial"[PT] OR "meta-analysis"[PT])
AND English[Language]
AND ("last 10 years"[PDat])
```

**Consensus query pattern:**
```
"In elderly patients with displaced femoral neck fractures (Garden III/IV), how do outcomes compare between hemiarthroplasty and total hip arthroplasty?"
```

**AO Surgery Reference navigation:**
```
Region → Proximal femur → Pertrochanteric fracture → AO/OTA 31-A3 reverse obliquity → CMN technique
```

### Step 4 — Build an evidence summary, not a paper dump

The output is not a list of every paper. It is a structured summary:

- **What the literature broadly supports** (with confidence)
- **Where the literature is contested** (with the leading arguments on each side)
- **What recent / influential papers say** (with brief points)
- **What the registries show in real-world cohorts** (often differs from RCT cohorts)
- **What gaps remain** (the unanswered questions — relevant for PMCF and future work)

Confidence in the evidence itself should be graded:

| Grade | Meaning |
|---|---|
| **High** | Multiple aligned RCTs / strong meta-analyses / large registries |
| **Moderate** | Single RCT or aligned cohort studies |
| **Low** | Mostly retrospective or single-centre series |
| **Very low** | Case reports, expert opinion, mechanism reasoning |

### Step 5 — Call the MCP evidence-retrieval tool

If a connected MCP backend is available:

```
orthoclass.retrieve_evidence({
  case_id: <id>,
  classification_codes: ["31-A3"],
  question_type: "treatment_comparison",
  question: "Long CMN vs short CMN in elderly reverse obliquity",
  sources: ["pubmed", "consensus", "ao_surgery_reference", "registries"],
  recency_years: 10
})
```

Otherwise, return the composed queries to the user and let them search directly.

## Output format

```yaml
evidence_summary:
  question: "Long CMN vs short CMN in 31-A3 in elderly patients"
  what_literature_broadly_supports:
    statement: "Long CMN is associated with lower peri-implant fracture rates than short CMN in osteoporotic bone, especially in reverse-obliquity patterns."
    confidence: "Moderate"
    key_sources: [<list of references>]
  where_contested:
    - issue: "Whether short nails are acceptable when reverse obliquity is excluded and bone quality is adequate"
      positions:
        - "Some series report acceptable peri-implant fracture rates with short nails in selected patients."
        - "Other series and registry data favour long nails across the board for biomechanical and patient-selection reasons."
  recent_or_influential_papers:
    - citation: <author, year, journal>
      summary: <one-line summary>
  registry_findings:
    - registry: <e.g. Norwegian Hip Fracture Registry>
      finding: <one-line summary>
  remaining_gaps:
    - "Direct RCT comparing long vs short CMN in 31-A3 specifically — limited."
    - "Long-term (>2 year) outcomes, peri-implant fracture rates, and revision data — registry-dependent."
  evidence_grade: "Moderate"
  not_medical_advice: true
```

## Example

**Input:** Skill 08 is comparing long vs short CMN in 31-A3.

**Skill response:**

For this question I'd compose searches across three sources:

**1) PubMed** — for primary literature and meta-analyses:
```
("hip fractures"[MeSH] OR "intertrochanteric fracture")
AND ("reverse obliquity" OR "31-A3" OR "AO/OTA 31.A3")
AND ("intramedullary nail" OR "cephalomedullary nail" OR "PFNA" OR "Gamma nail")
AND ("long versus short" OR "long vs short" OR "implant length")
AND English[Language] AND ("last 10 years"[PDat])
```

**2) Consensus** — for the natural-language clinical question:
```
"In elderly patients with reverse-obliquity intertrochanteric fractures (AO/OTA 31-A3), how do long cephalomedullary nails compare to short nails for peri-implant fracture rates and reoperation?"
```

**3) Registries** — for real-world cohorts:
- Norwegian Hip Fracture Registry (long-term implant survival)
- Swedish national datasets where available
- National Joint Registry of England, Wales, NI and Isle of Man (for hip-fracture related data)

**Anticipated evidence summary (template — actual content depends on retrieval):**

```yaml
evidence_summary:
  question: "Long CMN vs short CMN in 31-A3 in elderly patients"
  what_literature_broadly_supports:
    statement: "Long CMN is preferred for 31-A3, with lower peri-implant fracture rates compared to short CMN, especially in osteoporotic bone."
    confidence: "Moderate (mostly cohort + registry; limited RCT)"
  where_contested:
    - issue: "Whether short nails are acceptable for stable A1/A2 in good bone with no subtrochanteric extension"
      positions:
        - "Selected use of short nails: acceptable when patient and pattern are right"
        - "Default long nail: simpler decision, lower peri-implant fracture rate"
  remaining_gaps:
    - "RCT directly addressing length in 31-A3 specifically"
    - "Cost-effectiveness analyses incorporating peri-implant fracture revision costs"
  evidence_grade: "Moderate"
```

🩺 *Educational reference only — not medical advice. The composed queries and the evidence summary are aids to literature review; the treating surgeon evaluates the evidence in the context of their patient and local protocols.*

## Safety guardrails

- **The output is a query composition + evidence summary, not a recommendation.** "The evidence supports X" is not "you should do X".
- **Cite primary sources whenever possible.** Avoid evidence laundering through tertiary summaries.
- **Be honest about evidence quality.** Grading is built in. A "Low" grade is not a failure of the skill — it's information.
- **Cross-check across sources.** If PubMed says one thing and registries say another, surface the discrepancy.
- **Recency matters but is not everything.** A 2010 landmark RCT still matters; "last 10 years" is the default, not a hard cutoff.
- **No fabricated references.** If a source cannot be retrieved, say so. Never make up a citation.
- **Not medical advice.**

## Related skills

- `ortho-treatment-mapping`, `ortho-implant-selection` — consume the evidence summary
- `ortho-case-report-publishing` — uses the citations for the published case
- `ortho-outcome-measurement` — closes the loop by feeding real-world outcome data back into the evidence base (via OrthoClass)
