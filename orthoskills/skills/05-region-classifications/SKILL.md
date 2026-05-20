---
name: ortho-region-classifications
description: Use this skill in parallel with AO/OTA classification (skill 04) to apply region-specific eponymous classification systems — Garden and Pauwels for femoral neck fractures, Schatzker and Luo for tibial plateau, Neer for proximal humerus, Mason for radial head, Lauge-Hansen and Weber for ankle, Sanders for calcaneus, Hawkins for talar neck, Letournel-Judet for acetabulum, Tile and Young-Burgess for pelvic ring, and others. These systems often map more directly to treatment decisions than AO/OTA codes. Trigger this skill whenever a region-specific system is named or implied, or whenever skill 03 (anatomy routing) returned region-specific systems. Educational reference only; not medical advice; surgeon confirmation required.
---

# Region-Specific Classifications

## Purpose

Apply the eponymous, region-specific classification systems that complement AO/OTA. These systems often pre-date AO/OTA and remain in active clinical use because they map directly to treatment and prognostic questions surgeons actually ask.

This skill runs **alongside** skill 04 (AO/OTA Classification) — not in place of it. The output of both skills is combined in the case record.

## When to use

Trigger this skill when:

- Skill 03 (Anatomy Routing) returned `region_specific_systems` for the case
- A user explicitly names a system ("Garden grade?", "Schatzker classification?", "is this a Neer 3-part?")
- A treatment-mapping question implicitly needs the region-specific input ("should this femoral neck go to ORIF or arthroplasty?" needs Garden)

## Workflow

### Step 1 — Identify the systems to apply

From skill 03's `region_specific_systems` list, look up each in the reference files:

| Region | System | Reference file |
|---|---|---|
| Proximal femur (neck) | **Garden + Pauwels** | `references/garden-pauwels.md` (canonical deep) |
| Proximal humerus | Neer | `references/other-systems-stubs.md` |
| Radial head | Mason | `references/other-systems-stubs.md` |
| Tibial plateau | Schatzker, Luo three-column | `references/other-systems-stubs.md` |
| Ankle | Lauge-Hansen, Weber | `references/other-systems-stubs.md` |
| Talar neck | Hawkins | `references/other-systems-stubs.md` |
| Calcaneus | Sanders | `references/other-systems-stubs.md` |
| Acetabulum | Letournel-Judet | `references/other-systems-stubs.md` |
| Pelvic ring | Tile, Young-Burgess | `references/other-systems-stubs.md` |
| Distal radius | Frykman, Fernandez, Melone | `references/other-systems-stubs.md` |

### Step 2 — Apply each system

For each system, follow the same reasoning pattern as skill 04:

1. State the system and its purpose.
2. Walk through the decision points.
3. Produce a primary classification with explicit confidence.
4. List differentials.
5. State what additional info would change the classification.
6. Surgeon confirmation required.

### Step 3 — Combine outputs

The final case record carries both:
- AO/OTA code (from skill 04)
- Region-specific classification(s) (from this skill)

These should be **internally consistent**. If they contradict each other, surface the contradiction explicitly — it usually means one of them is wrong, or the case sits on a boundary.

### Step 4 — Hand off

The combined classification then drives:
- Skill 06 (Differential Reasoning) — manages remaining uncertainty
- Skill 07 (Treatment Mapping) — surfaces educational treatment options
- Skill 09 (Evidence Retrieval) — uses the codes as search keys

## Output format

```yaml
region_specific_classifications:
  - system: Garden
    primary:
      grade: III
      description_label: "Complete fracture, partially displaced"
      confidence: 0.78
      rationale: "Trabecular pattern interrupted but heads remain partially aligned with the neck on AP."
    differentials:
      - grade: IV
        confidence: 0.18
        rationale: "Cannot fully exclude complete displacement without true lateral."
    requires_surgeon_confirmation: true

  - system: Pauwels
    primary:
      type: II
      angle_degrees: ~50
      confidence: 0.70
      rationale: "Fracture line angle approximately 50° from horizontal — intermediate shear forces."
    differentials:
      - type: III
        confidence: 0.20
    requires_surgeon_confirmation: true

consistency_with_ao_ota:
  ao_ota_code: "31-B2"
  consistent: true
  notes: ""
```

## Example

**Context:** Skill 04 returned a primary classification of 31-B2 (transcervical femoral neck) for an elderly woman's fracture. Skill 03 had routed `region_specific_systems: [Garden, Pauwels]`.

**Skill response:**

I'll apply **Garden** and **Pauwels** in parallel — both are standard for femoral neck (31-B) and they answer different questions: Garden predicts AVN risk based on displacement, Pauwels predicts mechanical failure of fixation based on the fracture line angle.

Using `references/garden-pauwels.md` for full reasoning:

**Garden classification:**
- Grade I: incomplete (impacted valgus)
- Grade II: complete, non-displaced
- Grade III: complete, partially displaced — trabecular pattern disrupted but the head fragment maintains partial alignment with the acetabulum
- Grade IV: complete, fully displaced — head fragment realigned with acetabulum (the "double-density sign" disappears)

The AP shows a complete fracture line with the trabecular pattern of the head no longer aligning with the neck, but the head has not fully realigned with the acetabulum. → **Garden III** (confidence ~0.78). Garden IV cannot be excluded without a true lateral.

**Pauwels classification:**
- Type I: < 30° (more horizontal — primarily compressive forces)
- Type II: 30–50° (intermediate)
- Type III: > 50° (more vertical — primarily shear forces — highest failure rate of fixation)

The fracture line angle measures ~50° from horizontal. → **Pauwels II** (confidence ~0.70), Pauwels III on the differential.

**Combined output:**

```yaml
region_specific_classifications:
  - system: Garden
    primary: { grade: III, confidence: 0.78 }
    differentials: [{ grade: IV, confidence: 0.18 }]
  - system: Pauwels
    primary: { type: II, angle_degrees: 50, confidence: 0.70 }
    differentials: [{ type: III, confidence: 0.20 }]
consistency_with_ao_ota:
  ao_ota_code: "31-B2"
  consistent: true
```

**For the surgeon:** Please confirm. Treatment-relevant considerations from these classifications (educational, surfaced by skill 07):
- Garden III–IV in an elderly patient classically raises the question of arthroplasty vs fixation.
- Pauwels II–III raise the question of fixation stability if fixation is chosen.
- The combination influences cannulated screw vs sliding hip screw vs arthroplasty discussion in skill 08.

🩺 *Educational reference only — not medical advice.*

## Safety guardrails

- **Apply systems that fit the anatomy.** Don't apply Schatzker to a humerus.
- **Surgeon confirmation required.** Same rule as skill 04.
- **Internal consistency matters.** If Garden says one thing and AO/OTA says another, surface it.
- **Some systems require views or modalities that may not be present.** Sanders, for example, requires CT. If the imaging is inadequate for the system, say so and don't fake a grade.
- **Not medical advice.**

## Related skills

- `ortho-anatomy-routing` — selects which systems apply
- `ortho-aoota-classification` — runs in parallel
- `ortho-differential-reasoning` — handles remaining uncertainty
- `ortho-treatment-mapping`, `ortho-implant-selection` — consume the combined classifications
