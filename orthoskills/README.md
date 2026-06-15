# orthoskills (plugin)

**Open-source orthopaedic clinical reasoning skills for AI agents.**

This is the bundled `orthoskills` plugin — 12 Anthropic-style "skills" covering the orthopaedic surgical workflow, from diagnosis and AO/OTA fracture classification through treatment mapping, implant selection, outcome measurement, and aftercare.

> 🩺 **Educational reference only.** These skills do not provide medical advice. Every clinical decision must be made by a qualified surgeon with the patient in front of them. Skills emphasise human-in-the-loop confirmation at every step.

---

## What's in this plugin

A complete reasoning chain along the surgical workflow:

| # | Skill | Purpose |
|---|---|---|
| 01 | [Case Intake](skills/01-case-intake/SKILL.md) | Structured history, mechanism, exam, red flags |
| 02 | [Image Quality Check](skills/02-image-quality-check/SKILL.md) | AP/lateral adequacy, projection, artefacts, missing views |
| 03 | [Anatomy Routing](skills/03-anatomy-routing/SKILL.md) | Map anatomy → applicable classification systems |
| 04 | [AO/OTA Classification](skills/04-aoota-classification/SKILL.md) | AO/OTA 2018 structured reasoning (canonical: proximal femur) |
| 05 | [Region-Specific Classifications](skills/05-region-classifications/SKILL.md) | Garden, Pauwels, Schatzker, Neer, Mason, Lauge-Hansen, etc. |
| 06 | [Differential Reasoning](skills/06-differential-reasoning/SKILL.md) | Primary + differentials, confidence calibration, when to escalate |
| 07 | [Treatment Mapping](skills/07-treatment-mapping/SKILL.md) | Classification → treatment options (educational, not advisory) |
| 08 | [Implant Selection](skills/08-implant-selection/SKILL.md) | Generic device class considerations (CMN vs DHS vs plate, etc.) |
| 09 | [Evidence Retrieval](skills/09-evidence-retrieval/SKILL.md) | PubMed / Consensus / AO Surgery Reference query patterns |
| 10 | [Outcome Measurement](skills/10-outcome-measurement/SKILL.md) | PROMs, union status, complications, follow-up schedule |
| 11 | [Aftercare & Rehab](skills/11-aftercare-rehab/SKILL.md) | Weight-bearing progression, physio milestones, red flags |
| 12 | [Case Report Publishing](skills/12-case-report-publishing/SKILL.md) | Structured export (JBJS, OrthoWiki, registry) |

**Canonical deep skill:** `04-aoota-classification` includes a full reference for the **proximal femur** (AO/OTA segment 31). Other anatomical regions are present as stub references for the community to expand.

---

## How to use

### Via the Cowork plugin marketplace (recommended)

From the repo root (one level up from this folder), the marketplace manifest at `.claude-plugin/marketplace.json` lists this plugin. In a compatible client:

```
/plugin marketplace add MAIVAN-ai/Ortho-Skills
/plugin install orthoskills@ortho-skills-marketplace
```

Claude will then auto-discover all 12 skills bundled here and invoke the appropriate one when relevant queries arrive.

### Via direct file use (any AI agent)

Each `SKILL.md` is plain Markdown with YAML frontmatter — copy/paste the body into ChatGPT, Gemini, Claude.ai, or any agent's system prompt. The reasoning patterns work regardless of model.

### As an MCP tool consumer

The skills are designed to call the (forthcoming) **OrthoClass MCP server** for prospective case capture, ground-truth recording, and outcome linkage. See the `orthoclass.*` tool references throughout. When the MCP server is unavailable, skills degrade gracefully to advisory-only mode.

---

## Plugin layout

```
orthoskills/
├── .claude-plugin/
│   └── plugin.json                ← plugin manifest
├── README.md                      ← you are here
└── skills/
    ├── 01-case-intake/SKILL.md
    ├── 02-image-quality-check/SKILL.md
    ├── 03-anatomy-routing/SKILL.md
    ├── 04-aoota-classification/
    │   ├── SKILL.md
    │   └── references/
    │       ├── proximal-femur-31.md       ← canonical, deep
    │       ├── humerus-stubs.md
    │       ├── forearm-stubs.md
    │       ├── femur-shaft-distal-stubs.md
    │       ├── tibia-stubs.md
    │       └── spine-pelvis-stubs.md
    ├── 05-region-classifications/
    │   ├── SKILL.md
    │   └── references/
    │       ├── garden-pauwels.md          ← canonical companion to proximal femur
    │       └── other-systems-stubs.md
    ├── 06-differential-reasoning/SKILL.md
    ├── 07-treatment-mapping/SKILL.md
    ├── 08-implant-selection/SKILL.md
    ├── 09-evidence-retrieval/SKILL.md
    ├── 10-outcome-measurement/SKILL.md
    ├── 11-aftercare-rehab/SKILL.md
    └── 12-case-report-publishing/SKILL.md
```

---

## License

GNU Affero General Public License v3.0 — see [LICENSE](LICENSE).

The AO/OTA Fracture & Dislocation Classification Compendium 2018 is © AO Foundation. This repository **does not reproduce the Compendium**; it describes the *reasoning workflow* a surgeon or AI agent would follow when applying any classification system to a case. Always consult the official AO Foundation publications for authoritative classification text.

                       **NOTICE**

**No Data Rights Granted**

This repository license grants rights only to software, documentation,
schemas, and skill definitions. It grants no rights to collect, export,
sell, transfer, train on, or otherwise monetize patient case data,
clinical images, surgical videos, hospital records, registry data,
or derived clinical evidence.

Any use of case data requires a separate data-processing agreement,
patient consent basis where applicable, hospital authorization,
and, for ORTHO-X Data Commons participation, an ODCC data contribution agreement.

---
