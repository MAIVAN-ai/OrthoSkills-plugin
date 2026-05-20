---
name: ortho-treatment-mapping
description: Use this skill after a fracture has been classified (skills 04, 05) and differential reasoning (skill 06) has cleared the workflow to proceed. The skill surfaces the standard educational treatment options that map to the confirmed classification — what surgeons typically consider, the supporting rationale, and the trade-offs — without making autonomous treatment recommendations. Trigger this on queries like "what are the treatment options for 31-A3", "how is a Garden IV typically treated", "what would you do with this Schatzker V". Educational reference only; not medical advice; surgeon decision required for every case.
---

# Treatment Mapping

## Purpose

For a given classification, surface the treatment options that are commonly considered in the orthopaedic literature and in standard practice — with the rationale for each, and the relevant trade-offs. This is an **educational decision-support layer**, not a recommendation engine.

The treating surgeon decides. This skill helps the surgeon think.

## When to use

Trigger this skill when:

- Skill 06 (Differential Reasoning) returned `proceed_to_treatment_mapping: true`
- A user asks about treatment options for a named classification ("what are the treatment options for 31-A3?", "Schatzker VI management?")
- A case discussion has reached the post-classification stage

## Workflow

### Step 1 — Read the confirmed classification

Pull the primary classification (AO/OTA + region-specific) from the case record. If the classification is still uncertain, **route back to skill 06** rather than producing treatment options for an unsettled diagnosis.

### Step 2 — Open the treatment-pathway summary

For each major fracture pattern, treatment is shaped by:
- **The fracture's intrinsic stability** (calcar support, articular step-off, fragmentation)
- **The patient's age and physiological reserve** (the "physiological 60-year-old" matters more than the chronological number)
- **The patient's functional baseline and goals** (community ambulator vs nursing-home resident)
- **The bone quality** (osteoporosis dramatically changes implant choice)
- **The soft-tissue envelope** (open injuries, skin compromise, infection risk)
- **The patient's comorbidities and surgical risk** (cardiac, anticoagulation, frailty)

### Step 3 — Surface the standard options

For each plausible treatment, present:
- The option name (e.g. "cephalomedullary nail", "hemiarthroplasty", "non-operative functional brace")
- The clinical context where it's typically considered
- The main supporting rationale
- The recognised risks and trade-offs
- A pointer to relevant evidence (skill 09 will fetch it)

**Frame everything as options, not recommendations.** Use language like:
- "Widely considered for…"
- "Typically discussed in…"
- "Often preferred when…"
- "The literature supports…"

Avoid:
- "You should…"
- "This patient needs…"
- "The best treatment is…"

### Step 4 — Highlight decision points

Identify the specific clinical questions the surgeon must answer to choose among the options. Examples:

- "Garden III/IV in a 78-year-old with good function and good bone — fixation or arthroplasty? If arthroplasty, hemi or total?"
- "31-A3 with a long subtrochanteric component — short or long cephalomedullary nail?"
- "Schatzker VI with compromised soft tissue — staged ex-fix-then-ORIF or definitive plating now?"

### Step 5 — Capture the decision (if MCP available)

When the surgeon decides, capture it:

```
orthoclass.record_treatment({
  case_id: <id>,
  treatment_type: <e.g. "ORIF_cephalomedullary_nail">,
  implant: <generic device class from skill 08>,
  surgical_approach: <e.g. "lateral_decubitus_traction_table">,
  decision_rationale: <surgeon's free text>
})
```

This feeds the outcome-linkage pipeline (skill 10).

## Output format

```yaml
treatment_mapping:
  for_classification: "31-A2"
  patient_factors_to_consider:
    - "Age and physiological reserve"
    - "Bone quality"
    - "Pre-injury mobility"
    - "Comorbidities affecting surgical risk"
  options:
    - name: "Cephalomedullary nail (CMN)"
      typically_considered_for: "Multifragmentary pertrochanteric, especially with calcar compromise"
      rationale: "Load-sharing intramedullary construct, less abductor disruption than DHS"
      trade_offs: "Implant cost; learning curve; reported complications include cut-out, peri-implant fracture"
    - name: "Dynamic hip screw (DHS)"
      typically_considered_for: "Stable patterns with intact calcar; long historical track record"
      rationale: "Allows controlled fracture compression and impaction"
      trade_offs: "Less effective in calcar-deficient or reverse-obliquity patterns; lateral wall fracture is a recognised complication"
  decision_points:
    - "Is the calcar adequately supported?"
    - "Is there subtrochanteric extension (favouring long-nail considerations)?"
    - "Patient bone quality?"
  not_medical_advice: true
  surgeon_decision_required: true
```

## Example

**Input:** Confirmed 31-A3 (reverse obliquity intertrochanteric), elderly patient, good baseline mobility, on warfarin.

**Skill response:**

For a confirmed AO/OTA 31-A3 (reverse obliquity intertrochanteric), here are the options that are commonly considered, framed educationally:

**Option A — Cephalomedullary nail (CMN)**
- *Typically considered for:* the dominant pathway in published series for 31-A3. The biomechanical argument — the proximal fragment wants to displace medially under load — favours an intramedullary device that controls this displacement.
- *Rationale:* the nail body acts as a buttress; reverse-obliquity patterns specifically have been shown in cohort and registry studies to do better with intramedullary fixation than with sliding plate-based constructs.
- *Trade-offs:* implant cost; technique-sensitive entry point; learning curve; recognised complications include cut-out, peri-implant fracture (especially with short nails in osteoporotic bone), and lateral hip irritation.

**Option B — Long CMN vs short CMN**
- *Decision point:* if there is any subtrochanteric extension or if the patient has poor distal bone, a long nail bridging to the distal femur is widely preferred. Short nails are simpler and quicker but carry a higher rate of peri-implant fracture in osteoporotic bone.

**Option C — DHS (sliding hip screw) — historically poor for A3**
- *Typically considered for:* generally **not** chosen for 31-A3 in modern practice. The DHS construct allows the lateral fragment to slide along the screw — in reverse obliquity, this exacerbates rather than corrects the natural displacement.
- *Why it's surfaced anyway:* because surgeons should be explicit that this is the canonical reason A2 vs A3 distinction matters in skill 06.

**Decision points for this case:**
1. **Long vs short CMN** — assess for subtrochanteric extension on full femur imaging; consider patient's distal bone quality.
2. **Timing** — patient is on warfarin. Standard pathways involve reversal/bridging strategies. Most centres aim for surgery within 24–48 hours of admission for hip fractures (and there is strong evidence that delay > 48 hours worsens mortality).
3. **Theatre setup** — fracture table vs flat-top with traction; lateral decubitus vs supine; supine is the predominant choice for CMN.
4. **Anaesthetic** — spinal vs general; recent literature suggests no strong outcome difference, with patient preference and anaesthetist judgment dominating.

**Pointers for further evidence:** skill 09 (Evidence Retrieval) can pull current literature on:
- Long vs short CMN in elderly intertrochanteric fractures
- Time-to-surgery and mortality in hip fracture
- Anticoagulation reversal protocols

🩺 *Educational reference only — not medical advice. The treating surgeon decides every aspect of treatment based on the patient in front of them. Local protocols, available implants, surgeon experience, and individual patient factors take precedence over generic literature summaries.*

## Safety guardrails

- **Options, never recommendations.** Every treatment is presented as "considered in the literature for X", not "do Y".
- **Surgeon decision required.** Always.
- **Highlight when something is the *opposite* of best practice** (e.g. DHS for A3) — surgeons should know what to avoid as well as what to do.
- **Patient factors dominate.** A "textbook 31-A3" in a community-ambulating fit 65-year-old and a "textbook 31-A3" in a non-ambulatory nursing-home resident with severe dementia call for different conversations; this skill surfaces that.
- **No drug doses, no specific anticoagulation reversal protocols.** These are local-protocol-dependent and outside this skill's scope.
- **Not medical advice.**

## Related skills

- `ortho-differential-reasoning` — must clear the workflow before this skill runs
- `ortho-implant-selection` — gives more device-level detail
- `ortho-evidence-retrieval` — fetches current evidence for the options surfaced here
- `ortho-outcome-measurement` — captures what happened after treatment
