---
name: ortho-implant-selection
description: Use this skill after treatment mapping (skill 07) to describe the generic device-class considerations for orthopaedic implants — cephalomedullary nails vs sliding hip screws vs cannulated screws, locking vs non-locking plates, hemi- vs total arthroplasty, intramedullary nails vs plates for long bones, ex-fix vs definitive fixation, and so on. The skill describes device classes (not specific manufacturer products) and the trade-offs surgeons weigh when choosing between them. Trigger this on queries like "DHS vs CMN", "hemi vs total for displaced neck", "long vs short nail", "locking vs conventional plate". Educational reference only; not medical advice; manufacturer-agnostic; surgeon decision required.
---

# Implant Selection

## Purpose

For a chosen treatment pathway, describe the **generic device classes** typically available, the biomechanical and clinical rationale that distinguishes them, and the decision points surgeons weigh in choosing between them.

This skill is deliberately **manufacturer-agnostic**. It does not recommend specific products. It describes the device categories that appear in registries, in implant ontologies, and in the literature.

## When to use

Trigger this skill when:

- Skill 07 (Treatment Mapping) has surfaced a treatment pathway involving an implant choice
- A user asks about a generic device decision ("DHS vs CMN?", "hemi vs total?", "locking plate vs conventional plate?", "long vs short nail?")
- Templating, sizing, or pre-operative planning is being discussed at the device-class level

## Workflow

### Step 1 — Map classification + treatment pathway to candidate device classes

From the case record:
- AO/OTA + region-specific classification (skills 04, 05)
- Treatment pathway chosen by the surgeon (skill 07)

Use the matrix below as a starting point. This is not exhaustive — every region has its specialised devices.

| Pattern | Common device classes (generic) |
|---|---|
| 31-A1 stable pertrochanteric | Cephalomedullary nail (CMN), Dynamic hip screw (DHS) |
| 31-A2 multifragmentary | CMN (commonly), DHS (selected) |
| 31-A3 reverse obliquity | Long CMN (commonly); DHS typically avoided |
| 31-B1/B2 non-displaced/minimally displaced neck (younger or fit older) | Cannulated screws, Dynamic hip screw with anti-rotation, Fully-threaded headless screws |
| 31-B3 displaced neck (elderly) | Hemiarthroplasty (unipolar or bipolar), Total hip arthroplasty (THA) |
| 31-C femoral head | Internal fixation (mini-screws, headless compression screws), arthroplasty in older patients |
| 32 femoral shaft | Antegrade intramedullary nail, retrograde nail (selected), plate-osteosynthesis (selected) |
| 33 distal femur | Retrograde nail, lateral locking plate, dual plating in selected C-type |
| 41 tibial plateau | Lateral locking plate, medial buttress plate, dual plating (V/VI), ex-fix bridging |
| 42 tibial shaft | Intramedullary nail (predominant), plate (selected), ex-fix (open / damage control) |
| 43 distal tibia (pilon) | Staged ex-fix → ORIF with anteromedial / anterolateral plates; intramedullary nail in selected metaphyseal patterns |
| 44 ankle | One-third tubular plate, locking plate (osteoporotic), syndesmotic screw or suture-button, tension band for medial malleolus |
| 11 proximal humerus | Locking proximal humeral plate (PHILOS-class), intramedullary nail, hemiarthroplasty, reverse total shoulder arthroplasty |
| 23 distal radius | Volar locking plate (predominant), dorsal plate, fragment-specific plating, ex-fix |
| 62 acetabulum | Pelvic reconstruction plates, lag screws, percutaneous screws in selected patterns |
| 61 pelvic ring | Sacroiliac screws, anterior plate, INFIX, ex-fix (acute / damage control) |

### Step 2 — Describe each candidate device class

For each candidate, surface the following structure:

**Biomechanical principle.** What construct mechanics does this device achieve? (Compression, neutralisation, buttress, bridging, intramedullary load-sharing, locking-screw fixed-angle, tension-band.)

**Where it shines.** Patterns and patient factors where it is widely supported.

**Where it struggles.** Patterns and patient factors where it is known to fail or to be a poor choice.

**Recognised complications.** The classical failure modes and complications.

**Decision factors for this case.** Patient-specific factors that push toward or away from this device.

### Step 3 — Surface the choice points

After describing the candidates, summarise the actual choice points the surgeon faces:

- Construct biomechanics (compression vs bridging vs buttress)
- Bone quality (locking vs conventional screws; standard vs augmented constructs)
- Length (short vs long nail; standard vs long-stem arthroplasty)
- Approach implications (some implants require specific approaches)
- Cost and availability (in low-resource settings, this is often dominant)
- Surgeon familiarity (an implant the surgeon knows well usually beats an exotic implant they don't)

### Step 4 — Implant ontology pointer

For programmatic case records, record the device class using a controlled ontology. The forthcoming OrthoClass MCP exposes an implant ontology that maps to product master data. For this open repo, use the **generic device-class name** (e.g. `cephalomedullary_nail_long`, `volar_locking_plate`, `hemiarthroplasty_bipolar`).

If a connected MCP backend supports it:

```
orthoclass.detect_implant({ image_id: <intraop_or_postop_image_id> })
```

…can be used to identify the actual implant used from intra-op / post-op imaging.

## Output format

```yaml
implant_selection:
  for_classification: "31-A3"
  treatment_pathway: "intramedullary_fixation"
  candidate_device_classes:
    - device_class: "cephalomedullary_nail_long"
      biomechanical_principle: "Intramedullary load-sharing with cephalic fixation"
      where_it_shines: "Reverse-obliquity intertrochanteric; subtrochanteric extension; osteoporotic bone"
      where_it_struggles: "Patients with very narrow femoral canals; femoral deformity preventing nail passage"
      recognised_complications:
        - "Cut-out of cephalic screw"
        - "Peri-implant fracture (especially with short nails in osteoporotic bone)"
        - "Anterior cortex perforation in patients with bowed femurs"
      decision_factors:
        - "Subtrochanteric extension present?"
        - "Distal bone quality?"
        - "Patient femoral bow / canal diameter?"
    - device_class: "cephalomedullary_nail_short"
      where_it_shines: "Simple A1/A2 patterns in adequate bone, when reverse obliquity excluded"
      where_it_struggles: "Reverse obliquity; subtrochanteric extension; osteoporotic distal femur"
  choice_points:
    - "Long vs short nail (subtrochanteric extension; distal bone quality)"
    - "Cephalic screw vs blade (varies by implant family)"
    - "Single vs dual cephalic fixation"
  surgeon_decision_required: true
  manufacturer_agnostic: true
```

## Example

**Input:** Confirmed 31-A3, treatment pathway = intramedullary fixation, elderly patient, on warfarin, full-length femur films show a slight anterior femoral bow.

**Skill response:**

For a 31-A3 going to intramedullary fixation, the relevant device-class decisions are:

**Length — long vs short cephalomedullary nail**

- **Long nail (proximal femur to distal femur)** — widely supported for 31-A3 because the reverse-obliquity pattern often has subtle subtrochanteric extension that's only fully appreciated intra-operatively, and because peri-implant fracture rates are lower with long nails in osteoporotic bone. The trade-off: longer operative time, more fluoroscopy, slightly higher risk of anterior cortex perforation in patients with significant femoral bow.
- **Short nail** — quicker, less fluoroscopy, lower hardware cost. But the peri-implant fracture rate at the distal tip in osteoporotic patients is a recognised concern, and any subtrochanteric extension undermines its biomechanical case.

**Cephalic fixation — screw vs blade**

- Varies by implant family. Both have published series with broadly comparable outcomes. Blade-type implants (helical, U-blade, etc.) are sometimes argued to have lower cut-out rates in osteoporotic bone, but the evidence is mixed.

**For this patient's anterior femoral bow:** the long nail's distal tip impinging on the anterior cortex is a recognised risk. Pre-operative templating on full-length lateral views matters. Some implants are available in straight or curved versions; mismatch between the implant geometry and the patient's femoral bow is a documented cause of intra-operative complication.

**Decision points for the surgeon:**
1. Long vs short — defaulting to long for 31-A3 in osteoporotic bone is well-supported, but the surgeon may have local protocol guidance.
2. Cephalic device — by familiarity and local availability.
3. Anaesthesia and timing — warfarin reversal pathway runs in parallel; surgical timing balances reversal-of-anticoagulation against the established mortality penalty of delay > 48 hours.

🩺 *Educational reference only — not medical advice. The treating surgeon decides every aspect of implant selection based on local availability, surgical experience, and individual patient factors. This skill is manufacturer-agnostic and does not recommend specific products.*

## Safety guardrails

- **Manufacturer-agnostic.** Never recommend a specific product. Describe device classes.
- **Surgeon-decision-required.** Always.
- **Where an implant is widely considered inappropriate** (e.g. DHS for 31-A3), surface that — but explain why, not just "don't use it".
- **No specific torque values, drill sizes, or technique steps.** The AO Surgery Reference is the appropriate technique resource and is referenced in skill 09.
- **Avoid implying superiority of one manufacturer over another.** Differences within a device class are usually smaller than differences between device classes; both are usually smaller than differences in patient selection and surgical execution.
- **Not medical advice.**

## Related skills

- `ortho-treatment-mapping` — runs before this skill
- `ortho-evidence-retrieval` — fetches device-class outcomes literature
- `ortho-outcome-measurement` — captures how the chosen device performed
