---
name: ortho-anatomy-routing
description: Use this skill to map a suspected anatomical region to the orthopaedic classification systems that apply to it. Different regions need different systems — proximal femur uses AO/OTA 31 plus Garden plus Pauwels; tibial plateau uses AO/OTA 41 plus Schatzker plus Luo's three-column concept; proximal humerus uses AO/OTA 11 plus Neer. Trigger this skill whenever a case has reached the point where "we need to classify this" and before invoking AO/OTA or region-specific classification skills. The skill returns the ordered list of classification systems that should be applied. Educational reference only; not medical advice.
---

# Anatomy Routing

## Purpose

Most orthopaedic fractures benefit from being classified using **more than one system**. AO/OTA gives the universal, coded structure (used for registries and publications), while region-specific eponymous systems (Garden, Pauwels, Schatzker, Neer, Mason, Lauge-Hansen, Sanders, Hawkins…) often map more directly to treatment and prognosis.

This skill takes "the suspected anatomical region" and returns the ordered list of classification systems to apply.

## When to use

Trigger this skill when:

- Skill 02 (Image Quality Check) has returned `adequate` or `usable_with_limitations`
- The case intake has settled on a suspected anatomical region
- A downstream classification skill needs to know **which systems** to invoke

## Workflow

### Step 1 — Confirm the anatomical region

Use the field `suspected_anatomical_region` from the case intake. If it's still ambiguous (e.g. "hip pain — could be intertrochanteric or femoral neck"), enumerate the candidate regions and apply the routing for each.

### Step 2 — Look up the classification system mapping

The mapping below is the canonical reference. Update it via PR if you disagree with the choices for a region.

```yaml
proximal_humerus:
  ao_ota: "11"
  region_specific: [Neer]
  notes: "Neer remains the dominant clinical system; AO/OTA 11 used for registries."

humeral_shaft:
  ao_ota: "12"
  region_specific: []
  notes: "AO/OTA usually sufficient; describe radial nerve risk separately."

distal_humerus:
  ao_ota: "13"
  region_specific: []
  notes: "AO/OTA 13 captures supracondylar, intra-articular, and partial articular patterns."

olecranon_proximal_ulna:
  ao_ota: "21 (proximal forearm)"
  region_specific: [Mayo, Schatzker_olecranon]

radial_head:
  ao_ota: "21 (proximal forearm)"
  region_specific: [Mason]
  notes: "Mason is the standard for radial head; consider Hotchkiss modification."

forearm_shaft:
  ao_ota: "22"
  region_specific: []
  notes: "Capture both bones; distinguish Monteggia and Galeazzi patterns separately."

distal_radius:
  ao_ota: "23"
  region_specific: [Frykman, Fernandez, Melone_for_intraarticular]
  notes: "AO/OTA 23 is the registry standard; Fernandez is mechanism-based."

pelvic_ring:
  ao_ota: "61"
  region_specific: [Tile, Young_and_Burgess]
  notes: "Young & Burgess is mechanism-based; Tile maps to stability."

acetabulum:
  ao_ota: "62"
  region_specific: [Letournel_Judet]
  notes: "Letournel & Judet remains the dominant clinical system."

proximal_femur:
  ao_ota: "31"
  region_specific: [Garden, Pauwels]
  notes: "Garden + Pauwels for femoral neck; AO/OTA 31-A subdivides intertrochanteric; 31-B femoral neck; 31-C femoral head. Canonical deep reference in this repo."

femoral_shaft:
  ao_ota: "32"
  region_specific: [Winquist_Hansen_for_comminution]
  notes: "Capture comminution grade; describe open vs closed."

distal_femur:
  ao_ota: "33"
  region_specific: []
  notes: "AO/OTA 33 captures supracondylar, partial articular, and complete articular."

patella:
  ao_ota: "34"
  region_specific: []
  notes: "Describe extensor mechanism integrity separately."

tibial_plateau:
  ao_ota: "41"
  region_specific: [Schatzker, Luo_three_column]
  notes: "Schatzker is the dominant clinical system; Luo's three-column concept aids posterior approach planning."

tibial_shaft:
  ao_ota: "42"
  region_specific: []
  notes: "Open injuries: add Gustilo–Anderson grade."

distal_tibia_pilon:
  ao_ota: "43"
  region_specific: [Ruedi_Allgower]
  notes: "Pilon fractures: soft tissue grading critical."

ankle:
  ao_ota: "44"
  region_specific: [Lauge_Hansen, Weber_Danis]
  notes: "Weber is anatomic; Lauge-Hansen is mechanism-based — both have prognostic value."

talus:
  ao_ota: "81"
  region_specific: [Hawkins_for_talar_neck]
  notes: "Hawkins grade predicts AVN risk."

calcaneus:
  ao_ota: "82"
  region_specific: [Sanders, Essex_Lopresti]
  notes: "Sanders requires CT; Essex-Lopresti is older but still referenced."

cervical_spine:
  ao_ota: "Spine — AOSpine subaxial / upper cervical systems"
  region_specific: [SLIC, AOSpine_Subaxial, Anderson_DAlonzo_for_C2]

thoracolumbar_spine:
  ao_ota: "Spine — AOSpine TL system"
  region_specific: [TLICS]
```

### Step 3 — Handle ambiguous or compound regions

Some injuries cross regions (e.g. a femoral neck fracture with subtrochanteric extension). In those cases, **return multiple system sets** and flag the ambiguity:

```yaml
routing_decision:
  primary_region: proximal_femur
  systems: [AO/OTA_31, Garden, Pauwels]
  secondary_region: femoral_shaft_proximal
  secondary_systems: [AO/OTA_32]
  ambiguity_note: "Subtrochanteric extension visible — confirm with lateral view; classification approach may need to include reverse-obliquity intertrochanteric considerations."
```

### Step 4 — Hand off

Pass the routing decision to:
- Skill 04 (AO/OTA Classification) — for the AO/OTA coded result
- Skill 05 (Region-Specific Classifications) — for the eponymous systems

## Output format

```yaml
suspected_anatomical_region: <e.g. proximal_femur>
ao_ota_segment: <e.g. "31">
region_specific_systems: [<e.g. Garden, Pauwels>]
ambiguity_notes: <free text, empty if clear>
ready_for_classification: <true | false>
```

## Example

**Input from case intake:** `suspected_anatomical_region: proximal_femur` (elderly woman, fall, non-weight-bearing).

**Skill response:**

```yaml
suspected_anatomical_region: proximal_femur
ao_ota_segment: "31"
region_specific_systems:
  - Garden     # for femoral neck (31-B) — 4-stage system
  - Pauwels    # for femoral neck — fracture-line angle, biomechanics
ambiguity_notes: "If lateral view shows the line extending below the lesser trochanter, also consider 31-A reverse obliquity (intertrochanteric) — different implant pathway. Confirm lateral view per skill 02."
ready_for_classification: true
```

Recommended next steps:
- Apply **AO/OTA 31** via skill 04 → determines 31-A / 31-B / 31-C
- Apply **Garden + Pauwels** via skill 05 → only if the fracture turns out to be 31-B (femoral neck)

🩺 *Educational reference only — not medical advice.*

## Safety guardrails

- **Do not assume a region from a single AP view.** If image quality (skill 02) flagged missing views, the routing must include the caveat that classification may need to be revised when the missing view arrives.
- **List all applicable systems**, even if one looks dominant. Surgeons in different traditions prefer different systems.
- **Not medical advice.** Classification is for structured communication and prognostic estimation — treatment is the surgeon's decision.

## Related skills

- `ortho-case-intake`, `ortho-image-quality-check` — both run before this skill
- `ortho-aoota-classification`, `ortho-region-classifications` — both run after
