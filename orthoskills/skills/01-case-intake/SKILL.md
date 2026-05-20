---
name: ortho-case-intake
description: Use this skill whenever a user presents a new orthopaedic case — a patient story, a referral, a query that mentions a fracture, dislocation, joint pain, trauma mechanism, X-ray, or any musculoskeletal injury and asks for orthopaedic reasoning. The skill captures a structured history, mechanism of injury, focused examination, neurovascular status, and red flags before any classification or treatment discussion can proceed. Trigger this skill even when the user jumps straight to "what is this fracture" without giving history — the skill will guide elicitation of the missing facts. Educational reference only; not medical advice.
---

# Orthopaedic Case Intake

## Purpose

Capture a structured, complete orthopaedic case before any classification, treatment, or implant reasoning happens. Most diagnostic errors in orthopaedics are not classification failures — they are intake failures: a missed mechanism, an unasked-about anticoagulant, a neurovascular exam that was never documented.

This skill is the **front door** of the Ortho-Skills workflow. Every other skill in this repository assumes the intake produced by this one.

## When to use

Trigger this skill when:

- A user describes a new patient case ("60-year-old fell on the stairs", "skier hit a tree, knee pain", "elderly woman with hip pain after fall")
- A user uploads or describes an X-ray, CT, or MRI without giving clinical context
- A user asks "what is this?" or "how do I classify this?" about an injury, without history
- A user starts a case-based discussion in WhatsApp, OrthoClaw, or any orthopaedic-AI front-end
- A referral letter, ED note, or hospital handover is shared

If any structured intake fields are missing when downstream skills (classification, treatment mapping, implant selection) are invoked, route back to this skill to fill them in.

## Workflow

### Step 1 — Open the case

If a clinical-AI front-end with an MCP backend is connected, create a case record:

```
orthoclass.create_case({
  case_context: {
    anatomical_region: "<best guess from user input>",
    patient_age_group: "<paediatric | adult | elderly | unknown>",
    trauma_mechanism: "<high_energy | low_energy | pathological | unknown>",
    clinical_question: "<verbatim user question>"
  }
})
```

If no MCP server is available, hold the same fields in conversational memory and proceed.

### Step 2 — Elicit the structured history

Ask for or extract the following, in order. Do not all-at-once: ask in small batches of 2–4 items, with the most important first.

**Demographics & context**
- Age (or age group: paediatric / adult / elderly)
- Sex (relevant for some patterns — e.g. osteoporotic risk)
- Hand or leg dominance (for upper limb / weight-bearing injuries)
- Occupation and functional baseline (sedentary, active, manual labour, athlete)

**Mechanism of injury**
- When did it happen (hours, days, weeks ago)?
- High-energy or low-energy?
- Direct blow, indirect (twisting/torsion), axial load, fall from standing, fall from height?
- If a fall: forwards/backwards, onto outstretched hand, onto greater trochanter, etc.
- Witnessed loss of consciousness, head strike, polytrauma context?

**Symptoms now**
- Pain location and severity
- Deformity, swelling, bruising
- Weight-bearing or use of the limb possible?
- Neurological symptoms (numbness, weakness, paraesthesia)
- Vascular symptoms (coolness, pallor, capillary refill change)

**Past medical & medication history (do not skip)**
- Osteoporosis, previous fragility fractures
- Diabetes, peripheral vascular disease, smoking
- **Anticoagulants / antiplatelets** (always ask — affects timing and surgical planning)
- Steroids or immunosuppression
- Prior surgery on the affected limb (especially prior arthroplasty, prior osteosynthesis)
- Allergies (especially to metals and antibiotics)

**Functional and social context**
- Living situation (independent, assisted, nursing home)
- Mobility before injury (community ambulator, household ambulator, wheelchair)
- Support at home

### Step 3 — Focused examination findings

If the user has examined the patient, capture:

- **Look**: deformity, shortening, rotation, skin (closed vs. open — Gustilo–Anderson grade if open)
- **Feel**: tenderness localisation, crepitus, joint effusion
- **Move**: active and passive range, pain on motion
- **Neurovascular status** (mandatory):
  - Pulses distal to injury
  - Capillary refill
  - Sensation in named nerve distributions
  - Motor function in named nerve distributions
- **Compartments**: any signs of compartment syndrome (pain out of proportion, pain on passive stretch, tense compartments, paraesthesia)

### Step 4 — Red flag screening

Before any further reasoning, explicitly check for these and surface them prominently if present:

| Red flag | Action |
|---|---|
| Open fracture | Urgent antibiotics, tetanus, theatre — do not wait |
| Neurovascular compromise | Urgent reduction and reassessment |
| Compartment syndrome | Surgical emergency — fasciotomy |
| Suspected pathological fracture | Imaging beyond plain film, biopsy pathway |
| Polytrauma (ATLS context) | ATLS primary survey takes precedence |
| Suspected non-accidental injury (paediatric) | Safeguarding pathway, not just orthopaedic |
| Septic joint / infected implant | Aspirate and surgical washout pathway |
| Cauda equina (spinal context) | Urgent MRI, surgical decompression |

If any red flag is present, **interrupt the workflow** and tell the user the red flag explicitly before continuing with classification.

### Step 5 — Imaging inventory

What imaging exists?
- Plain radiographs — which views (AP, lateral, oblique, mortise, scapular Y, judet, etc.)?
- CT — was it done, is it available, with or without 3D reconstruction?
- MRI — done? indication?
- Ultrasound, bone scan, DXA?

If the answer is "only an AP X-ray" for an injury that needs more views, **note this as a limitation** and pass it to the Image Quality Check skill (02).

### Step 6 — Hand off to downstream skills

Once the intake is complete, summarise it as a structured case object and hand off:

- → Skill 02 (Image Quality Check) if images are available
- → Skill 03 (Anatomy Routing) to determine which classification systems apply
- → Skill 04 (AO/OTA Classification) and Skill 05 (Region-Specific Classifications) for diagnostic reasoning

## Output format

Always produce a structured case summary at the end of intake:

```yaml
case_id: <from MCP, or local stub>
demographics:
  age_group: <paediatric | adult | elderly>
  sex: <m | f | unspecified>
  dominance: <right | left | n/a>
  baseline_function: <free text>
mechanism:
  timing: <e.g. "6 hours ago">
  energy: <high | low | pathological | unknown>
  description: <free text>
symptoms:
  pain_severity: <0-10>
  deformity: <yes | no | unknown>
  weight_bearing: <able | unable | not_assessed>
  neurovascular_symptoms: <none | listed>
past_medical:
  osteoporosis: <yes | no | unknown>
  anticoagulants: <none | named drug>
  prior_surgery: <none | description>
  comorbidities: <list>
examination:
  look: <free text>
  feel: <free text>
  move: <free text>
  neurovascular: <intact | deficit described>
  compartments: <soft | concern described>
red_flags:
  - <any flagged from Step 4>
imaging_available:
  - <list of views/modalities>
imaging_missing:
  - <list of recommended views not yet obtained>
suspected_anatomical_region: <e.g. proximal_femur>
ready_for_classification: <true | false>
notes: <free text, including limitations of intake>
```

## Example

**User:** "60-year-old woman, fell at home, can't weight-bear on the left leg. AP pelvis X-ray attached."

**Skill response (abbreviated):**

I want to make sure we have the full picture before classifying. A few quick questions:

1. **When did the fall happen, and from what height?** (Fall from standing, or higher?)
2. **Any anticoagulants?** (Especially warfarin, DOACs, antiplatelets — this affects timing.)
3. **Is the leg shortened or externally rotated?** Any obvious deformity?
4. **Neurovascular status of the foot** — pulses, sensation, motor?
5. **Any other injuries?** Did she hit her head?

While you reply, a couple of things I'm noting from what you've shared:

- Elderly woman + fall + non-weight-bearing → high suspicion of proximal femur fracture. This will need to be classified using **AO/OTA segment 31**, plus **Garden** and/or **Pauwels** if it's a femoral neck pattern.
- Only an AP pelvis is mentioned — for proximal femur fractures, a **dedicated AP and lateral of the affected hip** is strongly preferred. I'll flag this to the Image Quality Check skill once we have a structured case.

🩺 *Educational reference only — not medical advice. All clinical decisions are made by the treating surgeon.*

## Safety guardrails

- **Not medical advice.** This skill helps structure thinking. The treating surgeon decides everything.
- **Surgeon decision required** for every downstream step.
- **Never invent missing history.** If the user has not given an anticoagulation history, the skill must ask, not assume.
- **Red flags interrupt the workflow.** If an open fracture, neurovascular compromise, compartment syndrome, polytrauma, or septic joint is mentioned, surface it immediately — do not bury it inside a classification discussion.
- **No PHI.** The skill must never request and never display a patient's name, date of birth, address, or any other identifier.

## Related skills

- `ortho-image-quality-check` — follows this skill once images are inventoried
- `ortho-anatomy-routing` — maps the suspected region to applicable classification systems
- `ortho-differential-reasoning` — once classification is in progress, manages uncertainty
