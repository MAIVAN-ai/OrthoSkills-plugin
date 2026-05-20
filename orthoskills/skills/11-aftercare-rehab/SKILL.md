---
name: ortho-aftercare-rehab
description: Use this skill to outline aftercare and rehabilitation considerations after orthopaedic treatment — weight-bearing progression, physiotherapy milestones, wound and DVT prophylaxis touchpoints, region-specific protocols, and the red flags that should escalate care back to the treating surgeon. The skill surfaces typical pathways at an educational level; it does not replace the surgeon's specific post-operative protocol for an individual patient. Trigger on queries like "post-op protocol for a tibial nail", "when can the patient weight-bear after a fixed Garden III hip", "what should physio focus on at 6 weeks", and similar. Educational reference only; not medical advice; surgeon's specific protocol always takes precedence.
---

# Aftercare & Rehabilitation

## Purpose

Describe typical post-operative pathways for the major orthopaedic patterns covered by this repository, at an educational level. The skill surfaces standard milestones and the red flags that should prompt escalation back to the treating surgeon.

This is the day-to-day skill for the people closest to the patient — physiotherapists, ward staff, primary care, and the patient themselves.

## When to use

Trigger this skill when:

- Skill 07 (Treatment Mapping) has settled and the user is asking about post-operative course
- A user asks "when can the patient weight-bear", "what should physio focus on", "what's normal at week X"
- A follow-up touchpoint is being prepared (alongside skill 10)
- A specific complication concern is being raised (the skill should escalate, not manage)

## Workflow

### Step 1 — Anchor to the treatment

Pull the recorded treatment from skill 07 + skill 08:
- Pattern (AO/OTA + region-specific)
- Procedure performed
- Implant class
- Surgeon's specified weight-bearing instructions (if recorded)

**The surgeon's specific instructions always take precedence over any generic pathway described here.**

### Step 2 — Surface the typical post-operative milestones

Generic pathways by region (educational only):

#### Proximal femur (31-A trochanteric)

| Time | Typical focus |
|---|---|
| Day 0–1 | Early mobilisation, often weight-bearing as tolerated (WBAT) for CMN constructs; sit out of bed, stand with assistance |
| Day 1–7 | Mobilise with frame / crutches; DVT prophylaxis per local protocol; wound check |
| 2 weeks | Wound review, suture removal if non-absorbable; continue physio |
| 6 weeks | X-ray review; physio progression; expect to be largely mobile with one stick or unaided |
| 3 months | Most united; full weight-bearing well-established; return to baseline mobility goal |
| 6, 12 months | PROM administration (skill 10); long-term implant survival |

#### Proximal femur (31-B neck, fixation)

| Time | Typical focus |
|---|---|
| Day 0–1 | Often protected weight-bearing (varies by surgeon and construct) |
| 2–6 weeks | Strict adherence to weight-bearing protocol; monitor for early AVN signs |
| 6 weeks | X-ray to check screw position, head sphericity |
| 3, 6, 9, 12 months | Monitor for AVN (clinical and radiographic — MRI if suspicion) |
| 12, 24 months | Long-term AVN surveillance; PROMs |

#### Proximal femur (31-B neck, arthroplasty)

| Time | Typical focus |
|---|---|
| Day 0–1 | Weight-bearing as tolerated; hip precautions per local protocol (posterior approach) |
| 2 weeks | Wound check |
| 6 weeks | Physio progression; resume most activities of daily living |
| 3 months | Most return to baseline function |
| 12 months | PROM, long-term implant survival, dislocation surveillance |

#### Tibial shaft (42, intramedullary nail)

| Time | Typical focus |
|---|---|
| Day 0–1 | Often WBAT for stable nail constructs; compartment monitoring |
| 2 weeks | Wound check; suture removal |
| 6 weeks | X-ray for callus; progress to full weight-bearing if not already |
| 3 months | Most show clear callus; some still callus-dependent |
| 6 months | Expected union timeline reached for most |
| 9–12 months | Non-union threshold if no progression |

#### Distal radius (23, volar locking plate)

| Time | Typical focus |
|---|---|
| Day 0 | Splint; elevation; finger and shoulder ROM from day 1 |
| 1–2 weeks | Wound check; transition to removable wrist splint |
| 2–6 weeks | Active and passive wrist ROM; pronation/supination |
| 6 weeks | X-ray; usually discontinue splint; grip strengthening |
| 3 months | Full ROM goal; return to most activities |
| 12 months | PROM (PRWE, DASH); plate removal in selected cases |

#### Ankle (44, ORIF)

| Time | Typical focus |
|---|---|
| Day 0–14 | Backslab / boot; non-weight-bearing typically |
| 2 weeks | Wound check; transition to walking boot |
| 6 weeks | X-ray; progress weight-bearing per protocol; ankle ROM |
| 3 months | Full weight-bearing; return to normal footwear |
| 6 months | Return to sport / running goal for younger patients |

These are **educational templates**, not prescriptions. Local protocols, surgeon preference, patient factors, and the specific construct used all modify the actual pathway.

### Step 3 — Surface region-specific red flags

For any post-op patient, escalate to the surgeon urgently if:

| Red flag | Action |
|---|---|
| Sudden severe pain | Implant failure? Re-fracture? — urgent clinical review and imaging |
| Wound erythema, discharge, dehiscence | Suspected infection — surgeon review, often urgent |
| Fever, sepsis features | Suspected deep infection — urgent referral |
| Calf swelling, chest symptoms | Suspected DVT/PE — urgent investigation |
| New neurological deficit | Possible nerve injury or compartment syndrome — urgent surgical review |
| Loss of weight-bearing capacity | Implant failure, non-union, re-fracture — urgent imaging |
| Hip dislocation symptoms (after arthroplasty) | Urgent referral |
| Wound non-healing at 3+ weeks | Surgeon review |
| Pain on full weight-bearing not improving by expected milestone | Surgeon review; consider non-union workup |

### Step 4 — DVT prophylaxis, pain management

These are **local-protocol-dependent**. The skill does not specify drug names, doses, or duration. It surfaces:
- DVT prophylaxis is standard practice after most major orthopaedic surgery
- Pain management typically multimodal (paracetamol + NSAID where not contraindicated + short-course opioid + regional anaesthesia where appropriate)
- The surgeon and pharmacy team configure the actual regimen

### Step 5 — Coordinate with skill 10 (Outcome Measurement)

At each follow-up touchpoint, this skill and skill 10 run together. This skill describes what should be happening at the milestone; skill 10 captures what actually happened.

## Output format

```yaml
aftercare_summary:
  for_treatment: "Long CMN for 31-A3 intertrochanteric, elderly patient"
  early_post_op:
    weight_bearing: "WBAT (weight-bearing as tolerated) — confirm with surgeon"
    mobility_goal: "Stand and pivot day 1, mobilise with frame day 1–2"
    dvt_prophylaxis: "Per local protocol"
  six_weeks:
    expected: "Mobile with frame or one stick; x-ray for early callus and hardware position"
    physio_focus: "Strengthening, gait re-education, stair training where appropriate"
  three_months:
    expected: "Most return to pre-injury mobility for community ambulators"
  red_flags_to_watch_for:
    - "Sudden severe pain (implant failure, peri-implant fracture)"
    - "Wound infection signs"
    - "Calf swelling / chest symptoms (DVT/PE)"
    - "Loss of weight-bearing capacity"
  surgeon_specific_protocol_overrides_this_template: true
```

## Example

**Input:** Long CMN for 31-A3 in an elderly woman, day 2 post-op.

**Skill response:**

For a long cephalomedullary nail in a 31-A3 reverse-obliquity intertrochanteric fracture, the typical early pathway:

**Day 0–2 (now):**
- Weight-bearing usually as tolerated for stable CMN constructs in reverse-obliquity patterns. **Confirm with the operating surgeon** — some surgeons specify partial weight-bearing for the first 2 weeks depending on reduction quality and bone.
- Out of bed day 1; stand and pivot; first steps with frame.
- DVT prophylaxis per local protocol (the team's choice of agent and duration).
- Multimodal analgesia; aim to mobilise rather than over-sedate.
- Wound check before discharge.

**Week 1–6:**
- Progressive mobilisation. Most patients move from frame → two crutches → one stick over 4–6 weeks.
- DVT prophylaxis typically continues for the full standard duration per local protocol (varies — your team will specify).
- Physio focus: hip and knee range of motion, abductor strengthening (the lateral approach disrupts gluteus medius — recovery of abductor function is a major focus).
- Wound: 2-week check; suture or staple removal if non-absorbable.

**6-week review:**
- X-ray to assess early callus and hardware position. Look for: cephalic screw maintained position, no varus collapse, no early cut-out signs.
- Mobility goal at this point: indoors unaided or with a stick; outdoors with a stick.
- If pain on weight-bearing is not improving, surgeon review.

**3 months:**
- Most united or progressing union. Most return to community ambulation if that was the baseline.

**Red flags during the post-op course — escalate to the operating surgeon urgently:**
- Sudden severe hip or thigh pain (implant cut-out, peri-implant fracture)
- Inability to weight-bear after previously being able
- Wound discharge, erythema, breakdown
- Fever or sepsis features
- Calf swelling, chest pain, breathlessness (DVT/PE)
- Falls

**For the next follow-up appointment (6 weeks), skill 10 will capture the structured outcome data — union status, function, PROMs, any complications.**

🩺 *Educational reference only — not medical advice. The operating surgeon's specific instructions for this patient take precedence over any generic pathway described here.*

## Safety guardrails

- **The surgeon's specific protocol overrides this skill always.** This skill is a generic template, not a prescription.
- **No drug names, doses, or specific durations** for DVT prophylaxis, antibiotics, or analgesia. These are local-protocol decisions.
- **Red flags escalate — they don't get managed by this skill.** The skill's job is to recognise and refer, not to manage complications.
- **No region-specific advice for regions not yet covered** in detail — refer back to the surgeon.
- **Patient-facing information needs different tone and detail.** If this skill is being used to brief a patient directly, use plain language and confirm with the surgical team first.
- **Not medical advice.**

## Related skills

- `ortho-treatment-mapping`, `ortho-implant-selection` — provide the inputs that shape aftercare
- `ortho-outcome-measurement` — runs at the structured follow-up touchpoints alongside this skill
- `ortho-case-report-publishing` — the eventual case report draws on the aftercare course
