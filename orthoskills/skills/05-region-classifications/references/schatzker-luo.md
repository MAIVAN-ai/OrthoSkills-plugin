# Schatzker + Column Concepts — Tibial Plateau Companion Classifications

**Deep reference. Apply alongside AO/OTA 41** (`../../04-aoota-classification/references/tibial-plateau-41.md`). **Status: draft for surgeon review.** Modelled on `garden-pauwels.md`.

These systems answer different questions about a tibial plateau fracture. Use them together; none is complete on its own.

| System | Question it answers | What it informs |
|---|---|---|
| **Schatzker** (1979) | Which pattern on the AP radiograph? Split or depression; lateral, medial or bicondylar; metaphyseal–diaphyseal dissociation | Energy, soft-tissue risk, shared vocabulary |
| **Revised Schatzker** (Kfuri & Schatzker 2018) | Where is the main fracture plane in three dimensions? Anterior or posterior, in which column | Patient positioning, approach, where hardware goes |
| **Three-column concept** (Luo 2010; definitions per Zhu 2012/2013) | Which columns have a cortical break on axial CT? | Approach and column-specific fixation |
| **Updated three-column concept** (Wang 2016) | Which injury mechanism: varus/valgus, flexion/extension? | Fixation sequence, where the main buttress goes |
| **Revised three-column** (Hoekstra 2017) | Does a lateral-column fracture extend into the posterolateral corner? | Lateral vs posterolateral approach |
| **Moore** (1981) | Does the morphology show a fracture-dislocation pattern? (Kept separate from the screening prompt, section 5) | Ligament and neurovascular injury risk |
| **Ten-segment** (Krause 2016) | Which articular segments are depressed or comminuted? | Articular visualisation and approach |

> **Evaluation hygiene.** The worked examples are synthetic teaching vignettes. Do not add cases that are used to evaluate the workflow; keep test cases held out.

---

## 1. Schatzker classification (6 types)

Described by Schatzker, McBroom and Bruce from the Toronto experience 1968–1975 (published 1979), using **anteroposterior radiographs**. It is a two-dimensional system, a limitation its originator later addressed (section 2).

| Type | Pattern |
|---|---|
| **I** | Lateral plateau split (wedge), no depression |
| **II** | Lateral split combined with depression |
| **III** | Lateral pure depression, no split. Some texts subdivide IIIa (lateral) and IIIb (central depression) (Gahr 2023) |
| **IV** | Medial plateau fracture: split and/or depression |
| **V** | Bicondylar: both plateaus fractured |
| **VI** | Metaphyseal–diaphyseal discontinuity **combined with any type of plateau fracture** |

**Two definitional points that are often misapplied:**
- **Type VI is defined by the metaphyseal–diaphyseal dissociation**, not by the number of plateaus involved. The articular component can be any plateau pattern.
- **Type IV is medial**, whatever its morphology. It is not a "more severe type III".

**What it informs:** a broad gradient of energy and soft-tissue risk from I to VI. Low-energy injuries typically produce unilateral depression-type fractures; high-energy injuries produce comminution with osseous, soft-tissue and neurovascular injury (Gahr 2023). Compartment syndrome was more frequent in types IV–VI, reaching 30.4% in type VI, in a series of 107 fractures (Chang 2000).

**Limitations:**
- Posterior fragments (posterolateral depression, posteromedial coronal split) are poorly represented on the AP view.
- In the originating centre of the three-column concept, 14 of 278 operatively treated plateau fractures could not be assigned a Schatzker type (Zhu 2012).
- Interobserver agreement is moderate at best (section 9).

---

## 2. Revised Schatzker classification (Kfuri & Schatzker 2018)

A CT-based update that keeps the six types and adds the third dimension:

- The plateau has **two columns**, lateral and medial.
- A **virtual coronal "equator"** divides each column into an **anterior (A)** and a **posterior (P)** quadrant.
- **Unicondylar types I–IV** get an **A or P** modifier for the location of the primary fracture plane.
- **Bicondylar types V–VI** get **A/P for the main fracture plane of each column**, plus **L/M** to name the column.
- The **main fracture plane** concept: locating it is what drives positioning, approach and hardware placement.

**How to record it in OrthoSkills.** Use structured fields rather than a free-text string, e.g. `type: II, main_fracture_plane: {lateral: P}`. Check the exact string notation against the original paper before exporting it to a registry or publication.

**Requires CT.** A/P modifiers are not assessable from radiographs alone.

---

## 3. Three-column concept (Luo 2010)

Introduced as a CT-based fixation concept for complex fractures. In the original paper, a "three-column fracture" had at least one separate fragment in the lateral, medial and posterior columns (Schatzker V/VI patterns). These were treated with column-specific fixation through combined posterior and anterolateral approaches (Luo 2010).

### Defining the columns (axial CT)

The following is per the originating group's definitions (Zhu 2013). Use the axial CT slice at the plateau level that first includes the fibular head:

- **O** — midpoint between the two tibial spines
- **A** — most anterior point of the tibial tuberosity
- **B** — posteromedial ridge of the plateau
- **C** — most anterior point of the fibular head

Lines **OA, OB and OC** divide the plateau into:

- **Lateral column:** between OA and OC
- **Medial column:** between OA and OB
- **Posterior column:** between OB and OC

A further line (OD) splits the posterior column into posterolateral and posteromedial parts.

### Counting columns

- A **column fracture** is a **break in that column's cortical wall**, verified on coronal and/or 3D CT.
- Articular depression **with** a break of the column counts as a fracture of that column.
- **Pure articular depression without a cortical break is a zero-column fracture** (typically Schatzker III).
- **Three-column fracture:** at least one independent articular fragment in each column. The commonest is a bicondylar fracture plus a separate posterolateral articular fragment.

Typical patterns (Zhu 2013):

| Pattern | Columns |
|---|---|
| Lateral split or split-depression (most Schatzker I/II) | One (lateral) |
| Anterolateral fracture + separate posterolateral depression with a posterior wall break | Two (lateral + posterior) |
| Posterior-column depression with a posterior wall break | One (posterior). **Not represented by any Schatzker type** |
| Anteromedial fracture + separate posteromedial fragment (traditionally Schatzker IV) | Two (medial + posterior) |

**Requires axial CT.** Never infer column involvement from radiographs alone.

---

## 4. Later refinements of the column concept

### Updated three-column concept (Wang et al. 2016)

Adds the **injury mechanism** to the morphology, in three steps:
1. Identify the injured columns and locate articular depression or comminution.
2. Determine the mechanism: **varus/valgus** and **flexion/extension**.
3. Derive the approach(es), implant placement and fixation sequence.

The mechanism is estimated from the **posterior tibial slope angle** and the **medial tibial plateau angle** (Gahr 2023). Fixation logic (main buttress on the compression side, support plates on the tension side) belongs to skills 07 and 08. This skill only records the inferred mechanism and its confidence.

### Revised three-column approach (Hoekstra et al. 2017)

Places the posterior border of the lateral column **posterior** to the fibula (instead of anterior). This defines **"extended lateral column" fractures**: lateral-column fractures that reach into the **posterolateral corner**, which can be supported from an (antero)lateral approach with variable-angle plates. In Luo's original scheme, the posterolateral corner belongs to the posterior column (Gahr 2023). **State which convention you use** whenever a posterolateral fragment is described.

---

## 5. Moore classification — fracture-dislocation of the knee (1981)

Moore separated **132 fracture-dislocations from more than 1,000 proximal tibial fractures**. He described five types whose common feature is **an unstable joint with frequent serious soft-tissue or neurovascular injury** (Moore 1981). The key message: a fracture-dislocation is a different, more dangerous injury than a plateau fracture.

The type descriptions below follow the review by Gahr et al. (2023):

| Type | Pattern | Typical association |
|---|---|---|
| **I** | Posteromedial (dorsal) split of the medial condyle | Often ACL rupture |
| **II** | Entire condyle, medial (IIa) or lateral (IIb), with a second line separating the intercondylar eminence | Instability |
| **III** | Rim avulsion: capsular avulsions (lateral rim / Segond, eminence) | Often ACL rupture |
| **IV** | Rim compression: depression of the plateau edge with ligament rupture | Ligament injury |
| **V** | Four-part: comminuted, including eminence avulsion | Cruciates may stay attached to the eminence fragment |

### Screening and classification are separate outputs

Moore's work separated unstable fracture-dislocations from ordinary plateau fractures. **A medial plateau fracture is not automatically a fracture-dislocation.** This skill therefore records two different things:

1. **Screening prompt** — `instability_screening`. The fracture pattern warrants checking for instability and for associated neurovascular and ligament injury. Trigger it for:
   - medial or posteromedial plateau fractures (Schatzker IV patterns)
   - rim avulsion or rim compression fragments
   - an eminence fragment together with a condylar fracture
   - any sign of subluxation, or a high-energy mechanism

   It is a prompt to examine, not a diagnosis.
2. **Moore classification** — `moore`. Assign a type **only when the morphology supports that fracture-dislocation pattern**, for example documented subluxation or instability together with the matching fracture morphology. Otherwise record `assigned: false`, the candidate type if one is suggested, and the reason. Typing is not always possible: in a six-centre cohort of 150 isolated medial plateau fractures, 139 could be assigned a Moore type (Cruz 2024).

```yaml
instability_screening:
  triggered: true
  reasons: ["medial plateau fracture", "posteromedial coronal fragment"]
  prompts:
    - "Documented neurovascular examination, repeated over time"
    - "Assess for subluxation and ligament injury"
    - "Vascular testing per the local pathway for suspected knee dislocation or other high-risk injury"
moore:
  assigned: false
  candidate_type: I
  reason: "No subluxation or instability documented"
  requires_surgeon_confirmation: true
```

### Neurovascular assessment

The first step is a **documented neurovascular examination**: pulses and perfusion, plus motor and sensory function including the peroneal nerve. Repeat it over time. Further vascular testing follows the **local pathway for suspected knee dislocation or other high-risk injury**:

- **Knee dislocation.** A prospective study used the ankle–brachial index (ABI): arteriography below 0.90, serial examination at 0.90 or above. No arterial injury was missed (Mills 2004). Reviews emphasise serial vascular examination and selective CT angiography (Hantes 2026).
- **Schatzker IV–VI.** One single-centre series screened all Schatzker IV–VI fractures with symmetric pulses by ABI, with CT angiography at ABI ≤ 0.9. Over 17 years and 437 fractures it missed no vascular injury (Kantor 2025). This shows a structured screen can work; it is one centre's protocol, not a universal pathway.
- **Isolated medial plateau fractures.** In 150 such fractures, 9% presented with neurovascular injury, and no fracture morphology predicted it (Cruz 2024). This supports a careful screening prompt for medial patterns. It does not support an automatic fracture-dislocation label or a single imaging pathway.

CT angiography is tied to clinical findings, ABI results and the applicable protocol. It is not an automatic test for every medial plateau fracture.

---

## 6. Ten-segment classification (Krause et al. 2016)

A CT map of the articular surface: four quadrants with two segments each, plus anterocentral and posterocentral segments for eminence avulsions (Gahr 2023). Abbreviations follow the pattern ALL (anterolaterolateral), ALC (anterolaterocentral), PLL, PLC, PC, and so on.

In 246 knees, posterior segments were the most frequently affected in both B and C fractures. In type B the most frequent segments were PLL 65%, ALL 65% and ALC 61%; in type C they were PLC 86%, PC 85% and ALC 79% (Krause 2016).

**Use it as a descriptive map of where the articular damage is**, not as a primary classification. Its reliability is contested: interobserver κ was 0.08 in one study (Gahlot 2023) but 0.73 on 3D-CT in another (Yao 2022).

---

## 7. How the systems relate — crosswalk and discordance prompts

The systems are recorded **independently**:
- The AO/OTA code follows the continuity assessment in skill 04: is any part of the articular surface still continuous with the shaft?
- Schatzker follows its own definitions.

The table shows typical correspondences. It is useful for spotting discordance, never for converting one code into another.

| Pattern | AO/OTA 41 (typical) | Schatzker | Columns | Moore |
|---|---|---|---|---|
| Lateral split | B1.1 | I | One (lateral) | — |
| Lateral split-depression | B3.1 | II | One (lateral), or two with a posterior wall break | — |
| Lateral pure depression, no cortical break | B2.1 | III | Zero | — |
| Posterior-column depression with posterior wall break | B2.1(u) / B3.1(u) | Not represented (often forced into II/III) | One (posterior) | — |
| Medial split and/or depression | B1.2 / B2.2 / B3.2, or C — by the continuity test | IV | One (medial) or two (+ posterior) | Screen; type only with fracture-dislocation morphology |
| Bicondylar involvement | B or C — by the continuity test | V | Two or three | Screen; type only with fracture-dislocation morphology |
| Any plateau fracture + metaphyseal–diaphyseal discontinuity | B or C — by the continuity test | VI | Per articular columns | — |

Neither bicondylar involvement nor displacement settles B vs C. In one series, 61 of 70 medial plateau fractures coded AO/OTA 41-B1/B3 extended into the lateral articular surface (Vogel 2024).

**Discordance prompts.** Re-check, record and flag; never auto-correct.
1. **The Schatzker type and the AO/OTA code imply different anatomy**, e.g. Schatzker VI with a 41-B code, or Schatzker I–III with 41-C. Re-check both definitions against the images:
   - Is there a metaphyseal–diaphyseal discontinuity? (Schatzker VI)
   - Is any part of the articular surface still continuous with the shaft? (AO/OTA B vs C, skill 04)

   Record both answers, set `consistent: false` with the reason, and flag for surgeon review. Do not label it a coding error, and do not change either code to make them agree.
2. **A bicondylar Schatzker type (V/VI) with any AO/OTA code.** Confirm that the AO/OTA type came from the continuity assessment, not from the number of plateaus involved.
3. **Column counts require a cortical break.** A zero-column fracture should not carry a "column fracture" label in any free-text summary.
4. **Every posterior fragment found on CT must appear in the combined record.** Neither original Schatzker nor the AO/OTA code guarantees it, so record it as a revised-Schatzker P modifier, a column, a qualification, or under `associated_findings`.

---

## 8. Worked examples

*The same synthetic vignettes as in `tibial-plateau-41.md` (examples 1–3), with the CT and clinical details these systems need. Not real patients; not evaluation cases.*

### Example 1 — Lateral split-depression, central depression

**Extra CT detail:**
- The lateral split is a **true split component**: a separate cortical fragment, bounded by a fracture line through the lateral cortex and the articular margin. Its main plane lies **anterior** to the coronal equator.
- The depressed zone is central.
- Only the lateral cortex is broken; there is no posterior wall break.

```yaml
imaging_basis: native_multiplanar_ct
confidence_scale: "ordinal, imaging-limited; not a calibrated probability (provisional caps, section 9)"
region_specific_classifications:
  - system: Schatzker
    primary: { type: II, confidence: 0.72, rationale: "Separate lateral split fragment plus a depressed zone; medial plateau intact." }
    differentials: [{ type: III, confidence: 0.18, rationale: "Only if multiplanar review finds no separate split fragment (lateral cortex intact)." }]
    requires_surgeon_confirmation: true
  - system: Schatzker_revised_2018
    primary: { type: II, main_fracture_plane: { lateral: A }, confidence: 0.62 }
    requires_surgeon_confirmation: true
  - system: Luo_three_column
    primary: { columns: [lateral], count: 1, confidence: 0.70, rationale: "Cortical break in the lateral column only." }
    requires_surgeon_confirmation: true
instability_screening:
  triggered: false
  note: "Routine documented neurovascular examination still applies."
moore:
  assigned: false
  reason: "No fracture-dislocation morphology."
consistency_with_ao_ota:
  ao_ota_code: "41B3.1(x)"
  consistent: true
  notes: ""
```

### Example 2 — Medial split with posteromedial extension

**Extra CT detail:**
- Coronal-plane medial split with a posteromedial extension; no depression.
- Cortical breaks in the medial column and in the posteromedial part of the posterior column.
- An incomplete oblique line runs from the split into the metaphysis but stops short of the lateral cortex. The lateral plateau and its articular surface remain continuous with the shaft.

**Clinical detail:** high-energy varus mechanism. Documented examination shows symmetric foot pulses and an intact peroneal nerve. No subluxation on imaging; ligament status not yet assessed.

```yaml
imaging_basis: native_multiplanar_ct
confidence_scale: "ordinal, imaging-limited; not a calibrated probability (provisional caps, section 9)"
region_specific_classifications:
  - system: Schatzker
    primary: { type: IV, confidence: 0.70, rationale: "Medial plateau split; lateral plateau not fractured." }
    differentials: [{ type: VI, confidence: 0.15, rationale: "Only if the metaphyseal line proves complete (metaphyseal-diaphyseal discontinuity)." }]
    requires_surgeon_confirmation: true
  - system: Schatzker_revised_2018
    primary: { type: IV, main_fracture_plane: { medial: P }, confidence: 0.60 }
    requires_surgeon_confirmation: true
  - system: Luo_three_column
    primary: { columns: [medial, posterior], count: 2, confidence: 0.62 }
    differentials: [{ columns: [posterior], count: 1, confidence: 0.20, rationale: "If the medial cortical break is judged to lie posterior to line OB." }]
    requires_surgeon_confirmation: true
instability_screening:
  triggered: true
  reasons: ["medial plateau fracture", "posteromedial extension", "high-energy varus mechanism"]
  prompts:
    - "Repeat and document the neurovascular examination"
    - "Assess ligament injury and stability"
    - "Vascular testing per the local pathway for suspected knee dislocation or other high-risk injury"
moore:
  assigned: false
  candidate_type: I
  reason: "Morphology resembles a posteromedial split, but no subluxation or instability is documented."
  requires_surgeon_confirmation: true
consistency_with_ao_ota:
  ao_ota_code: "41B1.2"
  consistent: true
  notes: "Lateral plateau continuous with the shaft (skill 04 continuity test)."
```

### Example 3 — Bicondylar, fragmented articular surface, metaphyseal comminution

**Extra CT detail** (after spanning external fixation):
- Lateral plateau: depression with several articular fragments; the main lateral split lies **anterior** to the equator.
- Medial plateau: an anteromedial fracture line plus a separate **posteromedial** coronal fragment.
- Metaphysis: comminution disconnects the plateau from the diaphysis.
- No eminence fragment. No subluxation documented.

```yaml
imaging_basis: native_multiplanar_ct
confidence_scale: "ordinal, imaging-limited; not a calibrated probability (provisional caps, section 9)"
region_specific_classifications:
  - system: Schatzker
    primary: { type: VI, confidence: 0.66, rationale: "Bicondylar articular injury with metaphyseal-diaphyseal discontinuity through comminution." }
    differentials: [{ type: V, confidence: 0.24, rationale: "If the metaphyseal comminution is judged not to disconnect the plateau from the diaphysis." }]
    requires_surgeon_confirmation: true
  - system: Schatzker_revised_2018
    primary: { type: VI, main_fracture_plane: { lateral: A, medial: P }, confidence: 0.55 }
    requires_surgeon_confirmation: true
  - system: Luo_three_column
    primary: { columns: [lateral, medial, posterior], count: 3, confidence: 0.72 }
    requires_surgeon_confirmation: true
instability_screening:
  triggered: true
  reasons: ["high-energy bicondylar fracture", "posteromedial coronal fragment"]
  prompts:
    - "Serial documented neurovascular and compartment examinations"
    - "Vascular testing per the local pathway for high-risk injury"
moore:
  assigned: false
  reason: "No eminence fragment or subluxation documented; re-assess if either is found."
consistency_with_ao_ota:
  ao_ota_code: "41C3.3(e)"
  consistent: true
  notes: "The AO/OTA type comes from the continuity test, not from the Schatzker type. Posteromedial fragment recorded as medial: P and in the posterior column."
```

---

## 9. Inter-observer reliability and confidence ceilings

No tibial plateau classification is reproducible enough to be treated as ground truth. Selected studies:

| Study | Observers / cases | Imaging | Schatzker κ | AO/OTA κ | Column concept κ | Note |
|---|---|---|---|---|---|---|
| Huitema 2022 | 25 (9 trauma surgeons, 16 residents) / 40 | Conventional ± 3D print | 0.51 | 0.36 | — | Reference = consensus of 3 expert surgeons; no system exceeded moderate agreement; self-rated confidence ~7/10 despite moderate or worse accuracy |
| Mellema 2016 | 81 / 15 complex | 2D CT ± 3D CT | 0.32 | — | Luo 0.28 | 3D CT did not improve agreement |
| Yao 2022 | 6 / 90 | 2D / 3D CT | 0.64 / 0.66 | 0.56 / 0.59 | Updated three-column 0.53 / 0.65 | Ten-segment 0.60 / 0.73 |
| Hoekstra 2017 | 5 / 36 | CT | 0.53 | — | Revised three-column 0.67 | — |
| Patange Subba Rao 2014 | 5 / 52 | 2D / 3D CT | 0.54 / 0.55 | — | 0.72 / 0.87 | — |
| Zhu 2012 / 2013 | 4 / 50 | Radiographs (Schatzker, AO) vs CT (columns) | 0.57 | 0.62 | 0.77 | Originators' centre; columns rated on CT, the others on radiographs |
| Gahlot 2023 | 6 (3 experience levels) / 50 | Not stated in abstract | Best group 0.52 | — | — | Ten-segment 0.08; agreement fell with seniority |

The systematic review by Millar et al. (2018) found 38 classification systems. Only five had been tested for reliability. Plain-film reliability was typically moderate (κ 0.40–0.60), CT generally improved it, and only 11 of 32 complete systems had been linked to clinical outcome.

**Reading the evidence.** Figures from the originators' own centres are the most favourable. Independent multi-observer studies (Mellema, Huitema) report fair-to-moderate agreement. These studies measure agreement between observers. They do not show how likely a given code is to be right, and they cannot be converted into probabilities for this skill.

**What the confidence number means.** It is an **ordinal, imaging-limited estimate**: it ranks how strongly the available images support one category over the alternatives, on a 0–1 scale. It is **not a calibrated probability**. No scored reference set exists yet to calibrate it, and the reliability studies above do not establish one. Every output states its `imaging_basis` and carries `confidence_scale: ordinal, imaging-limited; not a calibrated probability`.

**Provisional output caps.** These are maintainer guardrails, neither derived from the literature nor calibrated. They stop the stated confidence from rising above what the imaging can support. Replace them once a panel-scored reference set exists.

| System | Radiographs only | CT as screen photos / selected images | Native multiplanar CT |
|---|---|---|---|
| Schatzker type | ≤ 0.65 | ≤ 0.70 | ≤ 0.80 |
| Revised Schatzker A/P modifiers | Not assessable | ≤ 0.50 | ≤ 0.70 |
| Three-column (which columns) | Not assessable | ≤ 0.55 | ≤ 0.80 |
| Moore type | Screening prompt only | Screening prompt only | ≤ 0.60, only when fracture-dislocation morphology is present |
| Ten-segment | Not assessable | Not assessable | Descriptive list only; no confidence |

---

## 10. Common pitfalls

| Pitfall | Mitigation |
|---|---|
| Calling a unicondylar fracture with metaphyseal–diaphyseal dissociation "Schatzker II/III" | Type VI is defined by the dissociation; the plateau pattern can be anything |
| Calling Schatzker IV "a simple medial split" | Trigger the screening prompt (documented neurovascular examination, stability). Get CT for the posteromedial fragment and for lateral extension: Schatzker IV fractures often extend into the lateral articular surface (Vogel 2024) |
| Turning the screening prompt into a Moore diagnosis | Keep `instability_screening` and `moore` as separate fields; assign a Moore type only when the morphology supports a fracture-dislocation |
| Ordering vascular imaging from the fracture label alone | Neurovascular examination first; vascular testing per the local pathway, driven by findings, ABI and risk |
| Missing the posteromedial coronal fragment in bicondylar fractures | It is common (59% of 111 bicondylar fractures, Higgins 2009) and is not encoded by Schatzker or AO/OTA. Record it explicitly |
| Labelling an isolated posterolateral depression "Schatzker III" without location | Add revised Schatzker P and the column description; note the posterolateral-corner convention (Luo vs Hoekstra) |
| Inferring columns from AP radiographs | Columns are defined on axial CT |
| Counting a pure depression as a column fracture | No cortical break → zero-column |
| Mixing Luo's and Hoekstra's posterolateral boundaries in one record | State the convention used |
| Quoting originators' reliability figures as typical | Use independent multi-observer figures (section 9) |
| Treating a disagreement between systems as noise, or as proof of an error | Re-check both definitions against the images and flag it for review (discordance prompts, section 7). Do not auto-correct either code |

---

## 11. References

Based on articles retrieved from PubMed unless marked otherwise.

- Schatzker J, McBroom R, Bruce D. The tibial plateau fracture. The Toronto experience 1968–1975. *Clin Orthop Relat Res.* 1979;(138):94–104. PMID 445923.
- Kfuri M, Schatzker J. Revisiting the Schatzker classification of tibial plateau fractures. *Injury.* 2018;49(12):2252–2263. doi:[10.1016/j.injury.2018.11.010](https://doi.org/10.1016/j.injury.2018.11.010)
- Luo CF, Sun H, Zhang B, Zeng BF. Three-column fixation for complex tibial plateau fractures. *J Orthop Trauma.* 2010;24(11):683–692. doi:[10.1097/BOT.0b013e3181d436f3](https://doi.org/10.1097/BOT.0b013e3181d436f3)
- Zhu Y, Yang G, Luo CF, et al. Computed tomography-based Three-Column Classification in tibial plateau fractures: introduction of its utility and assessment of its reproducibility. *J Trauma Acute Care Surg.* 2012;73(3):731–737. doi:[10.1097/TA.0b013e31825c17e7](https://doi.org/10.1097/TA.0b013e31825c17e7)
- Zhu Y, Hu CF, Yang G, Cheng D, Luo CF. Inter-observer reliability assessment of the Schatzker, AO/OTA and three-column classification of tibial plateau fractures. *J Trauma Manag Outcomes.* 2013;7:7. doi:[10.1186/1752-2897-7-7](https://doi.org/10.1186/1752-2897-7-7)
- Wang Y, Luo C, Zhu Y, et al. Updated Three-Column Concept in surgical treatment for tibial plateau fractures — a prospective cohort study of 287 patients. *Injury.* 2016;47(7):1488–1496. doi:[10.1016/j.injury.2016.04.026](https://doi.org/10.1016/j.injury.2016.04.026)
- Hoekstra H, Kempenaers K, Nijs S. A revised 3-column classification approach for the surgical planning of extended lateral tibial plateau fractures. *Eur J Trauma Emerg Surg.* 2017;43(5):637–643. doi:[10.1007/s00068-016-0696-z](https://doi.org/10.1007/s00068-016-0696-z)
- Moore TM. Fracture-dislocation of the knee. *Clin Orthop Relat Res.* 1981;(156):128–140. PMID 7226641.
- Krause M, Preiss A, Müller G, et al. Intra-articular tibial plateau fracture characteristics according to the "Ten segment classification". *Injury.* 2016;47(11):2551–2557. doi:[10.1016/j.injury.2016.09.014](https://doi.org/10.1016/j.injury.2016.09.014)
- Gahr P, Kopf S, Pauly S. Current concepts review. Management of proximal tibial fractures. *Front Surg.* 2023;10:1138274. doi:[10.3389/fsurg.2023.1138274](https://doi.org/10.3389/fsurg.2023.1138274)
- Chang YH, Tu YK, Yeh WL, Hsu RW. Tibial plateau fracture with compartment syndrome: a complication of higher incidence in Taiwan. *Chang Gung Med J.* 2000;23(3):149–155. PMID 15641218.
- Higgins TF, Kemper D, Klatt J. Incidence and morphology of the posteromedial fragment in bicondylar tibial plateau fractures. *J Orthop Trauma.* 2009;23(1):45–51. doi:[10.1097/BOT.0b013e31818f8dc1](https://doi.org/10.1097/BOT.0b013e31818f8dc1)
- Huitema JM, van der Gaast N, Brouwers L, et al. Are 3D-printed models of tibial plateau fractures a useful addition to understanding fractures for junior surgeons? *Clin Orthop Relat Res.* 2022;480(6):1170–1177. doi:[10.1097/CORR.0000000000002137](https://doi.org/10.1097/CORR.0000000000002137)
- Mellema JJ, Doornberg JN, Molenaars RJ, Ring D, Kloen P; Traumaplatform Study Collaborative & Science of Variation Group. Interobserver reliability of the Schatzker and Luo classification systems for tibial plateau fractures. *Injury.* 2016;47(4):944–949. doi:[10.1016/j.injury.2015.12.022](https://doi.org/10.1016/j.injury.2015.12.022)
- Yao P, Liu Y, Shan L, et al. Intra- and inter-observer reliability assessment of widely used classifications and the "Ten-segment classification" of tibial plateau fractures. *Knee.* 2022;35:149–156. doi:[10.1016/j.knee.2022.03.002](https://doi.org/10.1016/j.knee.2022.03.002)
- Patange Subba Rao SP, Lewis J, Haddad Z, Paringe V, Mohanty K. Three-column classification and Schatzker classification: a three- and two-dimensional computed tomography characterisation and analysis of tibial plateau fractures. *Eur J Orthop Surg Traumatol.* 2014;24(7):1263–1270. doi:[10.1007/s00590-013-1308-9](https://doi.org/10.1007/s00590-013-1308-9)
- Gahlot N, Kunal K, Elhence A, et al. Ten-segment classification has lowest inter/intra-observer reliability as compared to Schatzker, three-column and AO systems for tibial plateau fractures. *Arch Bone Jt Surg.* 2023;11(4):256–261. doi:[10.22038/ABJS.2022.63442.3061](https://doi.org/10.22038/ABJS.2022.63442.3061)
- Millar SC, Arnold JB, Thewlis D, Fraysse F, Solomon LB. A systematic literature review of tibial plateau fractures: what classifications are used and how reliable and useful are they? *Injury.* 2018;49(3):473–490. doi:[10.1016/j.injury.2018.01.025](https://doi.org/10.1016/j.injury.2018.01.025)
- Cruz JP, Michaud JB, Van Rysselberghe NL, et al. Outcomes of isolated medial tibial plateau fractures by fracture morphology. *Injury.* 2024;55(8):111662. doi:[10.1016/j.injury.2024.111662](https://doi.org/10.1016/j.injury.2024.111662)
- Kantor AH, Thorne TJ, Dong W, et al. Ankle-brachial index is an effective screening tool for vascular injury in Schatzker type-4 to 6 tibial plateau fractures with symmetric pulses. *J Bone Joint Surg Am.* 2025;107(4):408–413. doi:[10.2106/JBJS.24.00545](https://doi.org/10.2106/JBJS.24.00545)
- Mills WJ, Barei DP, McNair P. The value of the ankle-brachial index for diagnosing arterial injury after knee dislocation: a prospective study. *J Trauma.* 2004;56(6):1261–1265. doi:[10.1097/01.ta.0000068995.63201.0b](https://doi.org/10.1097/01.ta.0000068995.63201.0b)
- Hantes M, Raoulis V, Zibis A, et al. Multiligament-injured knee: what the general orthopedic surgeon should know. *EFORT Open Rev.* 2026;11(5):426–436. doi:[10.1530/EOR-2026-0053](https://doi.org/10.1530/EOR-2026-0053)
- Vogel M, Hoffman A, Revak T. Schatzker IV tibial plateau fractures: are they always unicondylar? *OTA Int.* 2024;7(3):e341. doi:[10.1097/OI9.0000000000000341](https://doi.org/10.1097/OI9.0000000000000341)
- Skill 09 (Evidence Retrieval) for live literature queries.

🩺 *Educational reference only — not medical advice. Always confirm with a qualified surgeon and consult primary sources for authoritative system descriptions.*
