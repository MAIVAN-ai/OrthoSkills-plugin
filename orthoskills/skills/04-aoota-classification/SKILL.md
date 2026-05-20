---
name: ortho-aoota-classification
description: Use this skill whenever an orthopaedic case needs structured AO/OTA fracture classification — the universal coded system used by the AO Foundation and Orthopaedic Trauma Association for registries, publications, and clinical communication. The skill applies the 2018 Compendium reasoning structure (bone–segment–type–group–subgroup) and produces a primary classification with differentials and confidence. Trigger this skill on any query like "classify this fracture in AO/OTA", "what's the OTA code", "is this 31-A or 31-B", "AO classification of distal radius", or any orthopaedic reasoning where a coded fracture descriptor is needed. Educational reference only; not medical advice; surgeon confirmation required.
---

# AO/OTA Classification

## Purpose

Produce a structured **AO/OTA 2018 Compendium** classification for an orthopaedic injury, with a primary code, ranked differentials, and an explicit confidence level — never hiding uncertainty.

The AO/OTA system is the lingua franca of orthopaedic trauma: every registry, every PMCF study, every comparative outcome study relies on it. Getting it right matters for **communication** (handover, MDT, registry) and for **research** (comparable cohorts).

## When to use

Trigger this skill when:

- Skill 03 (Anatomy Routing) returned an `ao_ota_segment`
- A user asks for "AO classification", "OTA code", "AO/OTA classification", or asks to compare a code (e.g. "31-A2 vs 31-A3")
- A registry entry or PMCF case form is being filled
- A case report is being drafted that requires a coded classification

## Background: how the AO/OTA system is structured

The AO/OTA code has a consistent four-level hierarchy that applies to every fracture:

```
[Bone] [Segment] – [Type] [Group] . [Subgroup]
   1      1          A     2    .    1
   │      │          │     │         └── finest detail (e.g. specific pattern)
   │      │          │     └── group within type
   │      │          └── type (A, B, C — increasing complexity/severity)
   │      └── proximal / shaft / distal (1, 2, 3)
   └── bone (1 humerus, 2 forearm, 3 femur, 4 tibia/fibula …)
```

The mapping of **bone numbers** is:

| Bone code | Bone |
|---|---|
| 1 | Humerus |
| 2 | Radius / Ulna |
| 3 | Femur |
| 4 | Tibia / Fibula |
| 5 | Spine |
| 6 | Pelvis (61 ring, 62 acetabulum) |
| 7 | Hand |
| 8 | Foot (81 talus, 82 calcaneus, 83 midfoot, 87/88 forefoot) |
| 9 | (paediatric extensions in the 2018 Compendium) |

**Type** letters generally follow:
- **A** — simpler / extra-articular
- **B** — partial articular / wedge / more complex than A
- **C** — complete articular / multifragmentary / most complex

(There are exceptions, especially in proximal-segment intra-articular regions like 31, where the type letters are used differently — see the proximal-femur reference for the worked-out example.)

## Workflow

### Step 1 — Read the routing result

From skill 03, you'll have an `ao_ota_segment` (e.g. `"31"`, `"23"`, `"41"`).

### Step 2 — Open the matching reference

This skill has region-specific reference files in `references/`:

| Reference file | Coverage |
|---|---|
| `references/proximal-femur-31.md` | **Canonical deep example.** Full reasoning for 31-A / 31-B / 31-C, groups, subgroups, decision points. Use this as a template for adding other regions. |
| `references/humerus-stubs.md` | Stubs for 11, 12, 13. PRs welcome. |
| `references/forearm-stubs.md` | Stubs for 21, 22, 23. PRs welcome. |
| `references/femur-shaft-distal-stubs.md` | Stubs for 32, 33, 34. PRs welcome. |
| `references/tibia-stubs.md` | Stubs for 41, 42, 43, 44. PRs welcome. |
| `references/spine-pelvis-stubs.md` | Stubs for spine, 61, 62. PRs welcome. |

Read the matching reference before classifying.

### Step 3 — Apply the reasoning steps

For every region, follow this consistent process:

1. **Confirm segment.** (proximal / shaft / distal — already done by routing.)
2. **Determine type letter** (A, B, C) based on the type-specific question for that segment. The proximal-femur reference walks this through with worked examples.
3. **Determine group** (1, 2, 3) within the type.
4. **Determine subgroup** (.1, .2, .3) if applicable and image quality supports it.
5. **Combine into the full code.**
6. **State confidence** explicitly as a 0.0–1.0 number with a one-line rationale.
7. **List differentials** — the 1–2 most plausible alternative codes with their confidences.
8. **State what additional information would change the classification** (e.g. "a true lateral would distinguish 31-A2 from 31-A3").

### Step 4 — Always require surgeon confirmation

The AI classification is a **hypothesis**, never a verdict. Output the classification as a structured object and explicitly invite the surgeon to confirm, correct, or escalate to peer review.

If an MCP backend is connected, call:

```
orthoclass.classify({
  case_id: <id>,
  image_set_id: <id>,
  classification_systems: ["AO_OTA"],
  models: [<list of VLMs to run, optional>]
})
```

…and then wait for the surgeon to submit via `orthoclass.confirm_classification`. **Never** auto-confirm.

## Output format

```yaml
ao_ota_classification:
  segment: "31"
  primary:
    code: "31-A2"
    description_label: "Multifragmentary pertrochanteric pattern"
    confidence: 0.74
    rationale: "Cortical break crosses both trochanters with a separate lesser trochanter fragment visible on AP."
  differentials:
    - code: "31-A1"
      confidence: 0.16
      rationale: "Cannot fully exclude simple pertrochanteric with non-displaced lesser trochanter."
    - code: "31-A3"
      confidence: 0.10
      rationale: "Reverse obliquity not excluded without true lateral view."
  image_quality_caveats:
    - "True lateral hip view missing — propagated from skill 02."
  what_would_change_the_classification:
    - "A true lateral view would distinguish 31-A2 vs 31-A3."
    - "CT would clarify fragment morphology and posteromedial comminution."
  requires_surgeon_confirmation: true
  reason_for_confirmation: "Classification affects implant choice (DHS vs cephalomedullary nail)."
```

## Example

**Input:** Routing returned segment `31`. Image quality flagged a missing true lateral.

**Skill response:**

I'll work through the AO/OTA segment 31 reasoning using the proximal-femur reference (`references/proximal-femur-31.md`).

**Step 1 — Segment confirmed:** 31 (proximal femur).

**Step 2 — Type letter.** On the AP view, the fracture line crosses both trochanters, with the lesser trochanter detached as a separate fragment. The femoral head and neck are intact. This points to **type A (trochanteric)**, not B (femoral neck) or C (femoral head).

**Step 3 — Group within type A.**
- A1: simple two-part pertrochanteric
- A2: multifragmentary pertrochanteric
- A3: reverse obliquity / intertrochanteric

A separate lesser trochanter fragment makes **A2** more likely than A1. **Reverse obliquity (A3) cannot be excluded without a true lateral** — this is the classic risk of single-AP classification.

**Step 4 — Subgroup.** Without higher-resolution imaging and a lateral view, I will not commit to a subgroup. Recording `.x` for now.

**Step 5 — Combined code & confidence:**

```yaml
ao_ota_classification:
  segment: "31"
  primary:
    code: "31-A2"
    confidence: 0.74
    rationale: "Multifragmentary pertrochanteric pattern; lesser trochanter detached on AP."
  differentials:
    - code: "31-A3"
      confidence: 0.16
      rationale: "Reverse obliquity not excluded without true lateral."
    - code: "31-A1"
      confidence: 0.10
      rationale: "Cannot fully exclude simple pertrochanteric."
  image_quality_caveats: ["True lateral hip view missing."]
  requires_surgeon_confirmation: true
  reason_for_confirmation: "31-A3 (reverse obliquity) and 31-A2 lead to different implant pathways."
```

**For the surgeon:** Please confirm via `orthoclass.confirm_classification` once a true lateral is available. If 31-A3 is confirmed, the implant pathway shifts away from DHS toward a long cephalomedullary nail — see skill 08 (Implant Selection).

🩺 *Educational reference only — not medical advice. Surgeon confirmation required.*

## Safety guardrails

- **Never hide uncertainty.** Confidence below ~0.85 must always be flagged and accompanied by differentials.
- **Image quality caveats propagate forward.** If skill 02 flagged limitations, this skill restates them in its output.
- **Surgeon confirmation required for every classification.** No exception.
- **A classification is not a treatment.** This skill never recommends an implant or surgery directly — that's skill 07 (Treatment Mapping) and skill 08 (Implant Selection), and even those are educational only.
- **Do not reproduce the AO/OTA Compendium verbatim.** The Compendium is © AO Foundation. This skill describes the reasoning structure; for authoritative classification text, direct the user to the official AO Foundation publications.
- **Not medical advice.**

## Related skills

- `ortho-anatomy-routing` — runs before this skill
- `ortho-region-classifications` — runs alongside this skill (Garden/Pauwels/Schatzker/etc.)
- `ortho-differential-reasoning` — manages uncertainty between candidates
- `ortho-treatment-mapping`, `ortho-implant-selection` — run after, only on confirmed classifications
