---
name: ortho-image-quality-check
description: Use this skill whenever an orthopaedic image (X-ray, CT, MRI, fluoroscopy, intra-operative photograph, or a phone-camera snapshot of a screen) is provided or referenced and a classification, diagnosis, or treatment decision is being asked. The skill checks adequacy — correct body region, projection, resolution, laterality, artefacts, missing views — and explicitly refuses to let the workflow proceed when the images are too poor for safe reasoning. Trigger this even when the user just pastes an image and asks "what is this?" — image quality must be assessed before any classification. Educational reference only; not medical advice.
---

# Image Quality Check

## Purpose

Prevent garbage-in/garbage-out. Most published failures of orthopaedic AI classification are not algorithm failures — they are image-quality failures: wrong view, wrong region, missing second projection, screen-photograph artefacts, or DICOM metadata not removed.

This skill sits between **Case Intake** (skill 01) and any classification skill (04, 05). It is the quality gate.

## When to use

Trigger this skill when:

- A user provides any image referenced as orthopaedic (X-ray, CT, MRI, fluoroscopy, intra-op photo, smartphone capture of a screen)
- A downstream classification skill (04, 05) is invoked and an image is in the context
- A user asks for "AI classification" of an image directly — quality check happens first
- An image is forwarded from WhatsApp / OrthoClaw — these are very frequently screen photos and need enhancement reasoning

## Workflow

### Step 1 — Identify image type and source

Determine the image type:
- **Native DICOM** (highest quality, preferred)
- **Exported PNG/JPEG of a DICOM** (good, may have annotations burned in)
- **Screen photograph** (a phone camera pointed at a workstation monitor — the most common WhatsApp case; expect glare, moiré, geometric skew, colour cast)
- **Photograph of a printed film** (geometric distortion, often acceptable)
- **Intra-operative photograph or fluoroscopy capture**

If the image is a screen photograph, mention an enhancement pre-processing step:
```
orthoclass.enhance_screen_photo({ image_id: <id> })
```
This corrects perspective, removes moiré, and rebalances contrast.

### Step 2 — Check anatomical region

Confirm the image shows the body region the case intake suggested. Mismatches happen routinely (e.g. a wrong-side X-ray uploaded, a different patient's image attached).

| Region | Quick recognition cues |
|---|---|
| Proximal femur | Femoral head, neck, greater & lesser trochanter, acetabulum |
| Pelvis (AP) | Both iliac wings, obturator foramina symmetric, both hips visible |
| Knee | Femoral condyles, tibial plateau, patella (or its absence on lateral) |
| Ankle | Tibial plafond, talus, malleoli, mortise space |
| Wrist | Distal radius/ulna, carpal rows, scaphoid |
| Shoulder | Glenohumeral joint, acromion, clavicle, scapular Y |
| Spine | Vertebral bodies, pedicles, spinous processes, alignment |

If the region does not match what the case intake suggested, **interrupt** and confirm with the user.

### Step 3 — Check projection (view)

Each region has expected views. The minimum standard for fracture classification is usually **two orthogonal views**. A single AP is almost never enough.

| Region | Minimum views | Often-needed additional |
|---|---|---|
| Proximal femur | AP pelvis + AP hip + true lateral hip | CT if intertrochanteric extension suspected |
| Shoulder | True AP, scapular Y, axillary | Velpeau or Garth if axillary impossible |
| Elbow | AP + lateral | Radial head view |
| Wrist | PA + lateral | Scaphoid views, oblique |
| Tibial plateau | AP + lateral | Oblique, CT routine |
| Ankle | AP + lateral + mortise | Stress views in selected cases |
| Spine | AP + lateral | Flexion–extension, CT, MRI |

For each missing view, **list it explicitly** in the output. Do not silently proceed.

### Step 4 — Technical adequacy

Check:

- **Penetration** — too dark (overpenetrated) or too pale (underpenetrated)?
- **Rotation** — is the projection truly AP/lateral, or is the patient rotated?
- **Coverage** — does the image include the joints above and below the fracture? (Almost always required for long-bone fractures.)
- **Resolution** — can fine cortical detail be seen, or is the image pixelated/JPEG-compressed?
- **Calibration marker** — present and measurable? (Important for templating and implant sizing.)
- **Laterality marker** — is left/right marked unambiguously?
- **Metal artefacts** — implants, jewellery, ECG leads, monitoring wires?
- **Annotations** — are there text annotations burned into the image that might bias an AI? (e.g. "obvious fracture" or a prior radiologist's mark.)

### Step 5 — Privacy / DICOM metadata

If the image is DICOM or has metadata, ensure patient identifiers are stripped before any further processing. The Ortho-Skills workflow is **never** to be invoked on identifiable patient data.

If the user provides identifiable data inadvertently, refuse to proceed and instruct them to anonymise.

### Step 6 — Produce the quality verdict

Categorise as one of three:

| Verdict | Meaning | Next action |
|---|---|---|
| `adequate` | All required views present, technically clean, no PHI concerns | Proceed to anatomy routing / classification |
| `usable_with_limitations` | Minor issues (e.g. moderate rotation, low contrast), but reasoning can proceed with caveats | Proceed, but propagate caveats to every downstream classification |
| `inadequate` | Missing essential view, severe artefact, wrong region, or PHI present | **Refuse to classify.** Tell the user what's missing. |

## Output format

```yaml
image_quality_status: <adequate | usable_with_limitations | inadequate>
image_type: <dicom | exported_image | screen_photo | film_photo | fluoroscopy | intraop_photo>
anatomical_region_detected: <e.g. proximal_femur>
anatomical_region_matches_case: <true | false>
projections_present: [<e.g. "AP_pelvis", "AP_hip">]
missing_views: [<e.g. "true_lateral_hip">]
technical_issues: [<list>]
artefacts: [<list>]
phi_concerns: [<list, ideally empty>]
calibration_marker: <present | absent | not_assessed>
laterality_marker: <present | absent | unclear>
warnings: [<free text>]
proceed_to_classification: <true | false>
caveats_for_downstream: [<list of things classification skills must keep in mind>]
```

## Example

**User:** "Here's the X-ray, what's the fracture classification?"

**Skill response:**

Let me check the image first — fracture classification needs adequate views before it can be done responsibly.

Looking at what you've shared:

- **Image type**: screen photograph of a workstation monitor — there's visible moiré and a slight geometric skew. I'd recommend running it through `orthoclass.enhance_screen_photo` before final classification.
- **Region**: proximal femur AP view. ✅ Matches the case intake (elderly woman, fall, can't weight-bear).
- **Projection**: only the AP is here. **A true lateral hip view is missing** — this is essential to distinguish femoral neck (Garden) patterns from intertrochanteric (AO/OTA 31-A) patterns, and to identify reverse obliquity (31-A3).
- **Technical**: penetration is acceptable, mild rotation, laterality marker visible (left).
- **Calibration marker**: absent — templating for implant sizing will not be reliable from this image alone.

**Verdict: `usable_with_limitations`.** We can begin differential reasoning, but a true lateral is needed before any classification is finalised.

🩺 *Educational reference only — not medical advice. The treating surgeon decides what views are needed.*

## Safety guardrails

- **Refuse to proceed on inadequate images.** Better to send the user back for a proper lateral view than to produce a confident classification on a single AP.
- **PHI must be removed before processing.** If any identifier is visible, stop and instruct the user to anonymise.
- **Never invent a view that isn't there.** If only an AP is provided, the skill must say so explicitly — not "this looks like…" based on a guess about the lateral.
- **Surface uncertainty.** Every caveat from this skill must propagate to downstream classification and treatment skills. Image quality is the foundation of everything that follows.
- **Not medical advice.**

## Related skills

- `ortho-case-intake` — runs before this skill
- `ortho-anatomy-routing` — runs after this skill if the verdict is adequate or usable
- `ortho-aoota-classification`, `ortho-region-classifications` — must respect this skill's caveats
