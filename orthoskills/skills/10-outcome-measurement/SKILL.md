---
name: ortho-outcome-measurement
description: Use this skill at any post-treatment touchpoint — immediate post-operative, early follow-up (6 weeks), mid-term (3, 6, 12 months), and long-term (24 months and beyond) — to capture structured outcome data for an orthopaedic case. The skill records union status, weight-bearing progression, complications, revision surgery, patient-reported outcome measures (PROMs), and links these back to the original classification and chosen treatment so that real-world performance becomes visible. Trigger on follow-up visits, post-op imaging review, complication queries, PROM administration, and any "how is patient X doing" question that has follow-up data attached. This is the skill that closes the diagnose-treat-measure loop. Educational reference only; not medical advice; human-in-the-loop confirmation required for every outcome entry.
---

# Outcome Measurement

## Purpose

Close the loop. Most orthopaedic AI today stops at classification. Without outcome linkage, classification accuracy is divorced from clinical performance — and the system cannot improve. This skill captures structured outcomes at defined follow-up intervals and links them back to the classification and treatment recorded by skills 04, 05, 07, and 08.

This is the **PMCF (Post-Market Clinical Follow-up) / Topol-layer** skill. Its outputs are what make registry-grade research possible.

## When to use

Trigger this skill at:

- **Discharge / immediate post-op** — baseline post-treatment state
- **6 weeks** — early union signs, complications, mobility status
- **3 months** — most uncomplicated fractures show union; weight-bearing progression
- **6 months** — PROM administration, return to function
- **12 months** — primary outcome timepoint for most studies
- **24 months and beyond** — long-term implant survival, late complications, secondary osteoarthritis

Also trigger whenever a complication, revision, or readmission is reported regardless of the time point.

## Workflow

### Step 1 — Identify the follow-up touchpoint

Map the timing relative to the original injury/surgery:

```yaml
followup:
  timing_label: <discharge | 6w | 3m | 6m | 12m | 24m | other>
  weeks_from_surgery: <integer>
```

### Step 2 — Capture the standard outcome categories

#### a) Radiographic union (for fractures)

| Status | Definition |
|---|---|
| `not_assessed` | No imaging at this visit |
| `early_callus` | Bridging callus on 1–2 cortices |
| `progressing_union` | Callus on 3 cortices |
| `united` | Bridging callus on all 4 cortices OR clear consolidation |
| `delayed_union` | Expected union timeline exceeded without clear progression |
| `non_union` | No radiographic progression for ≥ 3 months in a fracture expected to have united |
| `mal_union` | United but in unacceptable alignment (specify deformity) |

Always describe alignment, hardware position, and any concerning features (loosening, broken hardware, cut-out, peri-implant lucency).

#### b) Functional status

```yaml
function:
  weight_bearing: <non | toe_touch | partial | full | unrestricted>
  mobility_aid: <none | stick | crutches | walker | wheelchair>
  range_of_motion: <free text or numeric for the joint>
  return_to_baseline_function: <yes | partial | no>
  return_to_work: <yes | modified | no | n/a>
```

#### c) Patient-Reported Outcome Measures (PROMs)

Use validated, region-specific PROMs:

| Region | Common PROMs |
|---|---|
| Hip | Harris Hip Score (HHS), Oxford Hip Score (OHS), HOOS, EQ-5D, NMS (New Mobility Score for hip fracture) |
| Knee | Oxford Knee Score (OKS), KOOS, IKDC, KSS |
| Shoulder | Constant-Murley, Oxford Shoulder Score (OSS), ASES, DASH |
| Elbow / wrist / hand | DASH, PRWE, MEPS for elbow |
| Foot / ankle | AOFAS, FAOS, FAAM, MOXFQ |
| Spine | ODI, NDI, SF-36, EQ-5D |
| General health | EQ-5D, SF-36, SF-12 |

For each PROM administered, capture:
- Instrument name and version
- Total score
- Sub-scores where applicable
- Date administered
- Method (in-person, phone, online, surrogate respondent)

#### d) Complications (CTCAE-style or Clavien-Dindo-style grading)

Capture each complication with:
- **Type:** infection, non-union, mal-union, AVN, hardware failure (cut-out, breakage, loosening), peri-implant fracture, DVT/PE, neurovascular injury, dislocation, heterotopic ossification, persistent pain, other
- **Grade:** mild (medical management only), moderate (intervention needed), severe (reoperation or life-threatening)
- **Timing:** weeks from index surgery
- **Outcome:** resolved, ongoing, permanent

#### e) Reoperation / revision

For each reoperation:
- Indication (linked to the complication)
- Procedure performed
- Implant changed?
- Outcome of revision

### Step 3 — Mortality (for hip fracture and high-risk groups)

Hip fracture cohorts have a well-known 30-day and 1-year mortality. Capture mortality status at each follow-up:

```yaml
mortality:
  alive: <yes | no | unknown>
  date_of_death: <if applicable>
  cause: <if known — cardiac, respiratory, sepsis, other>
  cause_related_to_orthopaedic_event: <yes | no | uncertain>
```

### Step 4 — Link to the original case

The outcome record must reference the original case so that downstream analytics can join classification + treatment + outcome:

```
orthoclass.record_outcome({
  case_id: <id>,
  followup_timing: <6m>,
  union_status: "united",
  function: {...},
  proms: [...],
  complications: [...],
  reoperations: [...],
  mortality: {...},
  notes: <surgeon free text>
})
```

### Step 5 — Surface concerning trends

If the outcome data triggers any of the following, surface it explicitly:

| Trigger | Action |
|---|---|
| Suspected non-union at 6+ months | Surface as a clinical flag; recommend formal non-union workup |
| Cut-out, loosening, peri-implant fracture | Surface as device-class signal for the validation analytics pipeline |
| Unexpected mortality clustered around a treatment pathway | Surface as a safety signal — registry-grade question |
| PROM trajectory worse than expected for the classification | Surface as a quality-of-care flag |

These signals feed `orthoclass.get_validation_metrics` and the registry-grade analytics that make Ortho-Skills + OrthoClass worth running.

## Output format

```yaml
outcome_record:
  case_id: <id>
  followup_timing_label: "6m"
  weeks_from_surgery: 26
  radiographic_union:
    status: "united"
    alignment: "anatomic"
    hardware_position: "satisfactory"
    notes: ""
  function:
    weight_bearing: "full"
    mobility_aid: "none"
    range_of_motion: "hip flexion 0–110°, extension to neutral, abduction 40°, no fixed deformity"
    return_to_baseline_function: "yes"
  proms:
    - instrument: "Oxford Hip Score"
      score: 41
      max: 48
      date: "2026-11-17"
  complications: []
  reoperations: []
  mortality:
    alive: yes
  flags_for_review: []
  next_followup_scheduled: "12m"
```

## Example

**Input:** 6-month follow-up for the elderly woman with 31-A2 treated by long CMN.

**Skill response:**

I'll structure the 6-month outcome record. Here's what I need to capture:

**1) Radiographic union** — please confirm from the 6-month films:
- Bridging callus on all four cortices?
- Hardware position (no cut-out, no breakage, screws unchanged in position)?
- Any peri-implant lucency?

**2) Functional status** — please share:
- Weight-bearing status (full / partial / etc.)
- Mobility aid use
- Comparison to pre-injury baseline (back to community ambulation? household only? wheelchair?)

**3) PROMs** — for this case I'd suggest:
- **Oxford Hip Score (OHS)** — validated for hip-fracture follow-up
- **New Mobility Score (NMS)** — specifically validated for hip fracture, captures pre-injury vs current
- **EQ-5D** — generic health-related quality of life
The OHS at 6 months is a useful single-number summary; NMS is particularly useful to compare to the pre-injury baseline (a NMS drop of more than 2 points is clinically meaningful).

**4) Complications** — please record any of:
- Infection (superficial, deep)
- Wound issues
- DVT/PE
- Cut-out or implant failure
- Peri-implant fracture
- Persistent pain
- Other (free text)

**5) Mortality status** — alive or deceased; if deceased, date and cause if known.

Once you share these, I'll call `orthoclass.record_outcome` to log the structured outcome and link it to the original 31-A2 classification and long-CMN treatment. That linkage is what makes the validation analytics work — over time, the patterns of which 31-A2 cases have good outcomes with which implants become visible across the cohort.

🩺 *Educational reference only — not medical advice. Outcome interpretation is the treating surgeon's clinical judgment; this skill structures the data, not the clinical decision.*

## Safety guardrails

- **Human-in-the-loop required.** No outcome is recorded without surgeon confirmation.
- **No diagnostic claims from outcome data alone.** A radiographic finding of suspected non-union triggers a recommendation for formal clinical assessment, not an autonomous diagnosis.
- **PROM interpretation requires clinical context.** A poor OHS at 6 months might reflect the fracture, the implant, an unrelated medical event, or a translation issue with the questionnaire. The skill records the data; the surgeon interprets.
- **Mortality data is highly sensitive.** Capture with care; do not share outside the treating team.
- **No PHI.** As with all other skills, the outcome record is keyed to a case_id, not to patient identifiers.
- **Not medical advice.**

## Related skills

- `ortho-treatment-mapping`, `ortho-implant-selection` — set up what is being measured here
- `ortho-evidence-retrieval` — uses outcomes (in aggregate) as part of the registry-grade evidence base
- `ortho-case-report-publishing` — formal case reports include the outcome data captured here
- `ortho-aftercare-rehab` — runs alongside this skill at every follow-up
