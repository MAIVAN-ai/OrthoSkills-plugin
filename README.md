# OrthoSkills — Claude Cowork Plugin

**Open-source orthopaedic clinical reasoning skills for Claude — packaged as a Cowork plugin.**

This repository is a [Cowork plugin marketplace](https://docs.claude.com) hosting the **`OrthoSkills`** plugin: a complete, bundled set of 12 Anthropic-style "skills" covering the orthopaedic surgical workflow — from diagnosis and AO/OTA fracture classification through treatment mapping, implant selection, outcome measurement, and aftercare.

> 🩺 **Educational reference only.** These skills do not provide medical advice. Every clinical decision must be made by a qualified surgeon with the patient in front of them. Skills emphasise human-in-the-loop confirmation at every step.
>
> **No Data Rights Granted**

This repository license grants rights only to software, documentation,
schemas, and skill definitions. It grants no rights to collect, export,
sell, transfer, train on, or otherwise monetize patient case data,
clinical images, surgical videos, hospital records, registry data,
or derived clinical evidence.

Any use of case data requires a separate data-processing agreement,
patient consent basis where applicable, hospital authorization,
and, for ORTHO-X Data Commons participation, an ODCC data contribution agreement.

---

## Install

To install:

- In Claude Cowork, click **Customize** > **Browse plugins** > **Personal** > **+** > **Add marketplace** from GitHub

- Enter **MAIVAN-ai/OrthoSkills-plugin** and click Sync

- Click **Install** on the **Orthoskills** card

Alternatively:

In Cowork (or any Claude client that supports the plugin marketplace format):

1. Add this repository as a marketplace source:
   ```
   /plugin marketplace add MAIVAN-ai/OrthoSkills-plugin
   ```
2. Install the plugin:
   ```
   /plugin install orthoskills@ortho-skills-marketplace
   ```

That single install gives you the entire workflow — all 12 skills are bundled in one plugin so the agent can move through case intake → classification → treatment mapping → outcome capture without manual skill juggling.

---

## What's in the plugin

The `orthoskills` plugin contains 12 skills along the orthopaedic surgical workflow:

| # | Skill | Purpose |
|---|---|---|
| 01 | Case Intake | Structured history, mechanism, exam, red flags |
| 02 | Image Quality Check | AP/lateral adequacy, projection, artefacts, missing views |
| 03 | Anatomy Routing | Map anatomy → applicable classification systems |
| 04 | AO/OTA Classification | AO/OTA 2018 structured reasoning (canonical: proximal femur) |
| 05 | Region-Specific Classifications | Garden, Pauwels, Schatzker, Neer, Mason, Lauge-Hansen, etc. |
| 06 | Differential Reasoning | Primary + differentials, confidence calibration, escalation |
| 07 | Treatment Mapping | Classification → educational treatment options |
| 08 | Implant Selection | Generic device class considerations (CMN vs DHS vs plate, etc.) |
| 09 | Evidence Retrieval | PubMed / Consensus / AO Surgery Reference query patterns |
| 10 | Outcome Measurement | PROMs, union status, complications, follow-up schedule |
| 11 | Aftercare & Rehab | Weight-bearing progression, physio milestones, red flags |
| 12 | Case Report Publishing | Structured export (JBJS, OrthoWiki, registry) |

**Canonical deep references** (full reasoning, worked examples, misclassification patterns):
- AO/OTA segment 31 (proximal femur) — `orthoskills/skills/04-aoota-classification/references/proximal-femur-31.md`
- Garden + Pauwels (femoral neck companion) — `orthoskills/skills/05-region-classifications/references/garden-pauwels.md`

Other anatomical regions are present as **stub references** ready for community expansion (see `CONTRIBUTING.md`).

---

## Repository layout

```
OrthoSkills/
├── .claude-plugin/
│   └── marketplace.json          ← lists the orthoskills plugin
├── orthoskills/                  ← the bundled plugin (12 skills)
│   ├── .claude-plugin/
│   │   └── plugin.json           ← plugin manifest
│   ├── README.md                 ← plugin-level README with workflow detail
│   └── skills/
│       ├── 01-case-intake/SKILL.md
│       ├── 02-image-quality-check/SKILL.md
│       ├── 03-anatomy-routing/SKILL.md
│       ├── 04-aoota-classification/
│       │   ├── SKILL.md
│       │   └── references/
│       │       ├── proximal-femur-31.md       ← canonical deep
│       │       ├── humerus-stubs.md
│       │       ├── forearm-stubs.md
│       │       ├── femur-shaft-distal-stubs.md
│       │       ├── tibia-stubs.md
│       │       └── spine-pelvis-stubs.md
│       ├── 05-region-classifications/
│       │   ├── SKILL.md
│       │   └── references/
│       │       ├── garden-pauwels.md          ← canonical companion
│       │       └── other-systems-stubs.md
│       ├── 06-differential-reasoning/SKILL.md
│       ├── 07-treatment-mapping/SKILL.md
│       ├── 08-implant-selection/SKILL.md
│       ├── 09-evidence-retrieval/SKILL.md
│       ├── 10-outcome-measurement/SKILL.md
│       ├── 11-aftercare-rehab/SKILL.md
│       └── 12-case-report-publishing/SKILL.md
├── .github/workflows/validate-skills.yml      ← CI: YAML frontmatter + safety disclaimer linter
├── LICENSE                       ← Apache-2.0
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
└── README.md                     ← you are here
```

---

## Why this exists

Eric Topol has rightly pointed out that medical AI lives or dies by the quality of its **ground truth, prospective validation, and outcome linkage**. Most orthopaedic AI today is trained on retrospective datasets with no surgeon confirmation and no outcome follow-up.

Ortho-Skills is the **public reasoning layer** of a larger ecosystem being built by [MAIVAN.ai](https://maivan.ai) / ORTHO-X:

```
┌────────────────────────────────────────────────────────┐
│  Ortho-Skills  (this repo, public, open-source)        │
│  → How an AI should reason about orthopaedic cases     │
└────────────────────────────────────────────────────────┘
                          │
                          ▼  consumed by
┌────────────────────────────────────────────────────────┐
│  OrthoClaw  (WhatsApp clinical reasoning agent)        │
│  → Surgeon-facing front-end                            │
└────────────────────────────────────────────────────────┘
                          │
                          ▼  validated by
┌────────────────────────────────────────────────────────┐
│  OrthoClass MCP  (registration-only, IP-protected)     │
│  → Prospective ground-truth + outcome linkage engine   │
└────────────────────────────────────────────────────────┘
```

The skills in this repo are **deliberately generic and open**. They encode how to *reason* through orthopaedic cases — not the proprietary case data, validated models, or PMCF infrastructure of OrthoClass. Skills reference `orthoclass.*` MCP tools but degrade gracefully when the backend is unavailable.

---

## Contributing

Pull requests are welcome from orthopaedic surgeons, registrars, residents, AI engineers, and anyone working at the intersection of orthopaedics and machine learning. See [CONTRIBUTING.md](CONTRIBUTING.md).

**Especially wanted:**
- Expanding stub regions in `orthoskills/skills/04-aoota-classification/references/` into full reference files modelled on `proximal-femur-31.md`
- Region-specific classification systems in `orthoskills/skills/05-region-classifications/references/` (Schatzker, Neer, Mason, Lauge-Hansen, Sanders, Hawkins, …)
- Real-world case examples (anonymised, with consent) for skill validation

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

## Maintainers

- [MAIVAN.ai](https://maivan.ai) / ORTHO-X — MAIVAN.ai PBC by Bluenaut Matching Services AG, CH-8802 Kilchberg Zurich, Switzerland
- Contact: coordinator@maivan.ai

---

> *"As opposed to many randomized trials and prospective studies, most medical AI has no ground truth."*
> — Eric Topol
>
> Ortho-Skills + OrthoClass exists to fix that, one fracture at a time.
