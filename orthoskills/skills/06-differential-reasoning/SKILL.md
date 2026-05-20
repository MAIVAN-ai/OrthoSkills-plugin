---
name: ortho-differential-reasoning
description: Use this skill whenever orthopaedic classification (skill 04 or 05) returns a primary candidate with non-trivial differentials, or when image quality, missing views, or borderline findings make the classification uncertain. The skill structures the differential, calibrates confidence, decides whether peer review or additional imaging is needed, and decides whether the workflow may safely proceed to treatment mapping. Trigger this whenever a confidence below ~0.85, a missing essential view, or a clinically meaningful alternative classification is on the table. Educational reference only; not medical advice.
---

# Differential Reasoning

## Purpose

Orthopaedic classification is often genuinely uncertain — borderline patterns, missing views, low image resolution. The wrong response to uncertainty is **false confidence**. The right response is to structure the differential, surface what would change it, and decide whether to escalate (peer review, additional imaging, senior input) before treatment reasoning proceeds.

This skill is the **uncertainty manager**.

## When to use

Trigger this skill when:

- Skill 04 or 05 returned a primary classification with confidence < 0.85
- Image quality (skill 02) flagged caveats that propagated forward
- A differential code or grade exists with confidence > 0.10
- The differentials map to **different treatment pathways** (this matters most — e.g. 31-A2 vs 31-A3, Garden II vs IV)
- A user explicitly asks "are you sure?" or "what else could this be?"

## Workflow

### Step 1 — Gather all candidate classifications

Pull together every classification output from skills 04 and 05:

```yaml
candidates:
  - { system: AO_OTA, code: "31-A2", confidence: 0.74 }
  - { system: AO_OTA, code: "31-A3", confidence: 0.16 }
  - { system: AO_OTA, code: "31-A1", confidence: 0.10 }
```

### Step 2 — Calibrate confidence

For each candidate, check:

| Check | Question |
|---|---|
| Image-quality consistency | Does the confidence reflect the image quality caveats from skill 02? If a true lateral is missing and the differential depends on the lateral, the primary's confidence should be tempered. |
| Pattern-recognition consistency | If the same VLM produced this and is known to overconfide on certain patterns (e.g. confusing valgus-impacted neck with non-displaced), is the confidence inflated? |
| Cross-system consistency | Does the AO/OTA code agree with the region-specific system? Disagreement is a yellow flag. |
| Clinical-context consistency | Does the classification fit the mechanism? A high-energy injury producing only a "simple A1" pattern is unusual — surface this. |

### Step 3 — Decide on the differential-handling response

| Situation | Response |
|---|---|
| Primary confidence ≥ 0.85, differentials < 0.15 each, differentials map to the **same treatment pathway** | Proceed. Note the differential briefly. |
| Primary confidence 0.6–0.85, **or** any differential ≥ 0.15 mapping to a **different treatment pathway** | Surface explicitly. Recommend either additional imaging (true lateral, CT) or peer review. Do not yet proceed to treatment mapping with full confidence. |
| Primary confidence < 0.6 | **Recommend peer review or senior input.** State the open differentials. Do not proceed to treatment mapping. |
| Image quality `inadequate` from skill 02 | **Refuse to classify.** Send back to skill 02 for re-imaging. |
| AO/OTA and region-specific systems disagree | Surface the disagreement explicitly. Ask which is more likely given the case context. |

### Step 4 — State what would resolve the uncertainty

Be concrete:
- "A true lateral hip view would distinguish 31-A2 vs 31-A3."
- "CT with sagittal reconstruction would clarify the posteromedial fragment."
- "A traction view would help if articular impaction is the open question."
- "Peer review from two additional orthopaedic surgeons via `orthoclass.request_peer_review` would address the inter-observer variance."

### Step 5 — Hand off

If the response is "proceed" → skill 07 (Treatment Mapping) with the primary classification.
If the response is "escalate" → hold the workflow; tell the user what's needed; offer to create a peer review request if MCP is available:

```
orthoclass.request_peer_review({
  case_id: <id>,
  review_question: "Is this 31-A2 or 31-A3? Reverse obliquity excluded?",
  share_channel: "whatsapp"
})
```

## Output format

```yaml
differential_summary:
  primary: { code: "31-A2", confidence: 0.74 }
  meaningful_differentials:
    - { code: "31-A3", confidence: 0.16, treatment_implication: "different — DHS typically avoided" }
  consistency_flags: []
  image_quality_caveats:
    - "True lateral hip view missing"
recommendation:
  action: <proceed | obtain_imaging | request_peer_review | escalate_to_senior | refuse_to_classify>
  rationale: <free text>
  what_would_resolve:
    - "True lateral hip view"
    - "CT if reverse obliquity confirmed on lateral"
  proceed_to_treatment_mapping: <true | false>
```

## Example

**Input:** AO/OTA primary 31-A2 confidence 0.74; differential 31-A3 confidence 0.16; image quality caveat "true lateral missing".

**Skill response:**

The primary classification is 31-A2 with confidence 0.74. That's below the threshold where I would proceed to treatment mapping without comment, for one specific reason: **31-A3 (reverse obliquity) is on the differential at confidence 0.16, and 31-A3 has a clinically meaningful different treatment pathway** — cephalomedullary nailing is widely preferred, and the DHS construct that would be reasonable for A2 has a well-described failure mode in A3.

```yaml
recommendation:
  action: obtain_imaging
  rationale: "A2 vs A3 distinction depends on a view we don't have. Treatment pathways differ meaningfully."
  what_would_resolve:
    - "True lateral hip view — primary tool to identify reverse obliquity"
    - "CT (sagittal reconstruction) if the lateral is equivocal"
  proceed_to_treatment_mapping: false
```

**For the surgeon:** before I move to treatment options, please obtain a true lateral hip view (or confirm one is already available that I haven't seen). If A3 is excluded, I'll proceed with the A2 pathway. If A3 is confirmed, the treatment-mapping discussion shifts.

🩺 *Educational reference only — not medical advice.*

## Safety guardrails

- **Never hide a meaningful differential.** Even if the primary is comfortably ahead, if the differential maps to a different treatment, surface it.
- **The threshold for escalation is lower when the alternatives diverge clinically.** Two differentials that both go to the same implant pathway are less worrying than two that diverge.
- **Do not produce false certainty under pressure.** If the user says "just give me the answer", the answer is the structured differential, not a hardened guess.
- **Peer review is a feature, not an admission of failure.** Recommending peer review is part of the workflow's value, not a sign that the skill has under-performed.
- **Not medical advice.**

## Related skills

- `ortho-aoota-classification`, `ortho-region-classifications` — feed this skill
- `ortho-image-quality-check` — caveats from this skill must be visible here
- `ortho-treatment-mapping` — only invoked when this skill says `proceed_to_treatment_mapping: true`
