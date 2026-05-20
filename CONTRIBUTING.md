# Contributing to Ortho-Skills

Thanks for considering a contribution. This repo is meant to be expanded by the community — orthopaedic surgeons, registrars, residents, AI engineers, and anyone working at the intersection of orthopaedic surgery and clinical AI.

---

## What kinds of contributions are welcome?

### 1. Expand stub regions into full reference files

The canonical deep example is `orthoskills/skills/04-aoota-classification/references/proximal-femur-31.md`. Most other AO/OTA segments are present as stubs. Pick a region you know well and expand its reference file using the proximal-femur file as a template.

Particularly wanted (in rough priority order):
- Distal radius (AO/OTA 23) — high case volume, well-studied
- Tibial plateau (AO/OTA 41) — Schatzker companion already exists as a stub
- Proximal humerus (AO/OTA 11) — Neer system companion needed
- Ankle (AO/OTA 44) — Lauge-Hansen + Weber classification
- Distal femur (AO/OTA 33)
- Calcaneus (AO/OTA 82) — Sanders system

### 2. Add region-specific classification systems

`orthoskills/skills/05-region-classifications/references/` is where complementary systems live. The Garden + Pauwels combination for proximal femur is the canonical example. Wanted:
- Schatzker (tibial plateau)
- Neer (proximal humerus)
- Mason (radial head)
- Lauge-Hansen + Weber (ankle)
- Sanders (calcaneus)
- Hawkins (talar neck)
- Frykman / Fernandez (distal radius)
- Letournel / Judet (acetabulum)
- Tile (pelvic ring)

### 3. Anonymised case examples for skill validation

If you can contribute anonymised cases (with appropriate patient consent and IRB/ethics approval where required) that demonstrate the reasoning workflow end-to-end, please open an issue first to discuss the data governance and consent model.

### 4. Improvements to existing skills

Tighter reasoning, better triggering descriptions, clearer red-flag logic, sharper differentials — all welcome.

---

## How to contribute

1. **Open an issue first** for substantial changes — it's much easier to align before you spend the time writing.
2. **Fork → branch → PR.** Use branch names like `add-schatzker-reference` or `improve-image-quality-skill`.
3. **Follow the SKILL.md format** (see below).
4. **Sign your commits** if you can (`git commit -s`) — implies you accept the [Developer Certificate of Origin](https://developercertificate.org/).
5. **CI must pass.** The workflow in `.github/workflows/validate-skills.yml` checks that every SKILL.md has valid YAML frontmatter.

---

## SKILL.md format

Every skill is a single Markdown file with YAML frontmatter at the top:

```markdown
---
name: skill-name-in-kebab-case
description: One or two sentences describing when this skill triggers AND what it does. The triggering language matters — include phrases a real user would say. Be a little "pushy" so the skill triggers when relevant.
---

# Human-readable title

## Purpose

What this skill helps the AI do.

## When to use

Concrete triggers, user phrases, contexts.

## Workflow

Step-by-step reasoning instructions in the imperative form.

## Output format

If structured output is expected, show the exact template.

## Examples

At least one realistic example.

## Safety guardrails

What this skill must NOT do. (For Ortho-Skills, every skill includes "not medical advice / surgeon decision required".)
```

Keep skills focused. A skill that tries to do too much triggers unreliably. If you find yourself writing more than ~500 lines, split it into a parent skill that references separate detail files in a `references/` subfolder.

---

## Clinical safety rules

Every skill in this repository must follow these rules:

1. **Educational reference only.** Skills must explicitly state they do not provide medical advice.
2. **Surgeon decision required.** All clinical decisions are made by a qualified surgeon with the patient in front of them. The AI is a reasoning aid, never an autonomous decision-maker.
3. **Human-in-the-loop confirmation.** Skills that produce a classification, differential, or treatment option must explicitly require human confirmation before downstream actions.
4. **No PHI in examples.** Anonymise everything. No real patient identifiers, no real institution names without consent.
5. **No verbatim AO/OTA Compendium text.** The Compendium is © AO Foundation. Describe the *reasoning workflow* and *the structure* of the classification, not the verbatim text. Always direct users to the official AO Foundation publications for authoritative reference.

PRs that violate these rules will be asked for revision before merge.

---

## Code of Conduct

See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md). Be kind. We are all here because we want orthopaedic AI to be better, safer, and more useful for patients and surgeons.

---

## Questions?

Open a GitHub issue or reach out to the maintainers listed in the README.
