# AO/OTA Segment 41 — Proximal Tibia (Tibial Plateau)

**Deep reference. Status: draft for surgeon review.** Modelled on `proximal-femur-31.md`.

This file walks through structured reasoning for segment 41 of the AO/OTA Fracture and Dislocation Classification Compendium 2018 (Meinberg et al., *J Orthop Trauma* 2018;32 Suppl 1, tibia chapter pp. S49–S52). It describes the **structure and the decision points**; it does **not** reproduce the Compendium text or figures. For authoritative wording and illustrations, always consult the official AO Foundation / OTA publication.

Companion systems (Schatzker, the 2018 revised Schatzker, Luo's three-column concept, Moore) live in `../../05-region-classifications/references/schatzker-luo.md`. Run both files together: the AO/OTA code alone misses information that drives treatment, especially posterior fragments.

> **Evaluation hygiene.** The worked examples below are synthetic teaching vignettes. Never add a case to this file that is used to evaluate the classification workflow — keep test cases held out, or the evaluation measures recall of this file rather than reasoning.

---

## 1. Scope of segment 41

Segment 41 is the **proximal end segment of the tibia**: the articular surface of both plateaus, the intercondylar eminence and the metaphysis.

**Where segment 41 ends (Compendium location rules):**

- **Square rule.** An end segment is defined by a square whose side equals the widest part of the epiphysis/metaphysis. Everything between the proximal and distal squares is diaphysis (segment **42**).
- **Centre rule.** A fracture is allocated to the segment that contains its centre. For a wedge fracture the centre is at the widest part of the wedge; for fragmentary-wedge and multifragmentary fractures it can only be judged after (mental) reduction.
- **Articular rule.** A fracture with a **displaced articular component** is classified as an end-segment articular fracture, even if most of it lies in the diaphysis. An **undisplaced fissure** that reaches the joint does not change the allocation; the fracture centre decides. This rule decides the **segment** (42 vs 41). Within segment 41, any fracture line entering the articular surface makes the fracture articular (B or C); see section 2.

**Neighbouring codes:**

- Proximal fibula: coded **separately** since 2018, as **4F1** (4F1A simple, 4F1B multifragmentary, with a qualification for extra- vs intra-articular involvement). Write it as a second code, e.g. `41B3.1, 4F1A`.
- Patella: **34**. Distal femur: **33**. Pure knee dislocations without fracture use the dislocation classification, with direction as a universal modifier.

---

## 2. Type letters in segment 41

| Type | Meaning | Key test |
|---|---|---|
| **41-A** | Extra-articular, including avulsions | Bony avulsion only, or no fracture line into the plateau articular surfaces → A. Tibial spine (cruciate) avulsions are coded here even though they lie inside the joint |
| **41-B** | Partial articular | Part of the joint surface is fractured; **the rest of the articular surface is still continuous with the metaphysis/diaphysis** |
| **41-C** | Complete articular | The joint surface is disrupted **and completely separated from the diaphysis** |

The **B-versus-C question is the most consequential decision in segment 41**, and it is a question about continuity, not about how many plateaus look broken on the AP view:

> **Is any part of the articular surface still attached to the diaphysis through intact bone?** Yes → B. No → C.

Answering it reliably usually needs CT: a metaphyseal fracture line that looks complete on one radiograph may leave a bridge of intact cortex, and vice versa.

Neither displacement nor the number of plateaus involved settles this question. In one series, 61 of 70 medial plateau fractures coded 41-B1/B3 extended into the lateral articular surface (Vogel 2024).

---

## 3. Decision tree

```
START
 │
 ├─ Bony avulsion only (capsule, tubercle, tibial spine / cruciate insertion)? ──► 41-A1
 │
 ├─ Any fracture line into the plateau articular surfaces?
 │     NO ──► 41-A
 │             ├─ Simple metaphyseal fracture (spiral/oblique/transverse) ──► A2
 │             └─ Wedge or multifragmentary metaphyseal fracture ──► A3
 │
 └─ YES ── Any part of the articular surface still continuous with the diaphysis?
         │
         ├─ YES ──► 41-B
         │          ├─ Split only ──────────────► B1
         │          ├─ Depression only ─────────► B2
         │          └─ Split + depression ──────► B3
         │          Subgroup: which plateau (.1 lateral, .2 medial;
         │          .3 = oblique line through the tibial spines and one plateau, B1/B3 only)
         │
         └─ NO ───► 41-C
                    ├─ Articular simple + metaphysis simple ────────────────► C1
                    ├─ Articular simple + metaphysis wedge/multifragmentary ─► C2
                    └─ Articular surface fragmented ────────────────────────► C3
```

---

## 4. Type 41-A — Extra-articular

### Group A1 — Avulsion

Bony avulsion without articular fracture. Subgroups distinguish the attachment: **capsular** attachments (A1.1; the lateral capsular avulsion is the Segond fragment), the **tibial tubercle** (A1.2), and the **tibial spine / cruciate insertion** (A1.3, qualified as anterior or posterior).

**Clinical relevance:** the bone injury is small; the ligament injury may not be. Capsular rim avulsions such as the Segond fragment are frequently associated with ACL rupture (Gahr 2023). Isolated eminence avulsions are commonly subclassified with Meyers–McKeever (Gahr 2023).

### Group A2 — Simple metaphyseal

One fracture line through the metaphysis, subgrouped by its pattern: spiral (A2.1), oblique (A2.2), transverse (A2.3).

### Group A3 — Wedge or multifragmentary metaphyseal

Intact wedge (A3.1), fragmentary wedge (A3.2; the side of the wedge is a qualification), multifragmentary (A3.3).

**Clinical relevance (A2/A3):** alignment and the soft-tissue envelope drive decisions. Proximal tibial fractures that extend towards the shaft carry a particular compartment-syndrome risk and need repeated clinical checks (Gahr 2023).

> ⚠ **Before coding 41-A, check CT for any fracture line reaching the plateau articular surfaces.** If one does, the fracture is articular (B or C), and the continuity test decides which. Displacement does not decide the type.

---

## 5. Type 41-B — Partial articular

### Group B1 — Split

A pure cleavage of one plateau without depression: lateral (B1.1), medial (B1.2), or an oblique split through the tibial spines and one plateau (B1.3, side as qualification).

### Group B2 — Depression

Pure articular depression without a cortical split: lateral (B2.1) or medial (B2.2). Depressions can involve any part of the surface, most often central or lateral (AO Surgery Reference).

### Group B3 — Split-depression

A split fragment plus a depressed articular zone: lateral (B3.1), medial (B3.2), or oblique through the spines and one plateau (B3.3).

### Location qualifications for B (and C) fractures

The 2018 Compendium adds lowercase **qualifications in round brackets** to say where the injury sits:

| Letters | Meaning | Applies to |
|---|---|---|
| **t** / **u** / **x** | anterolateral / posterolateral / central | Lateral depressions: B2.1, B3.1 |
| **v** / **w** / **x** | anteromedial / posteromedial / central | Medial depressions: B2.2, B3.2 |
| **f** / **h** | lateral / medial | Side of an oblique split (B1.3, B3.3) or of a metaphyseal wedge (A3.1–A3.2, C2.1–C2.2) |
| **d** / **e** | simple / multifragmentary metaphysis | C3 subgroups |
| **s** | metadiaphyseal extension | C3 subgroups |
| quadrant letters (t, u, v, w, x) | location of the articular fragmentation | C3 subgroups |

Example: `41B2.1(u)` = lateral pure depression, posterolateral.

> ✅ **Checked.** The letter sets and the subgroups they attach to were confirmed against the printed Compendium (pp. S50–S52) during surgeon review of this reference.

### Clinical relevance

- **Lateral plateau (B1.1, B2.1, B3.1).** The commonest patterns; low-energy injuries typically produce unicondylar depression-type fractures (Gahr 2023). Meniscal and ligament injuries accompany a large proportion of plateau fractures (>70% in some series; Gahr 2023). Document depression depth and plateau widening.
- **Medial plateau (B1.2, B2.2, B3.2).** Rarer, usually higher-energy, with a worse prognosis than lateral fractures (AO Surgery Reference). These patterns warrant a **documented neurovascular examination and an assessment for instability and ligament injury**. In 150 isolated medial plateau fractures, 9% presented with neurovascular injury and no fracture morphology predicted it (Cruz 2024). This is a screening prompt, not a diagnosis of fracture-dislocation; see the screening/classification split in the companion reference.
- **Posterior location matters.** Posterolateral (u) and posteromedial (w) injuries are easily missed on the AP view. In a CT series of 246 knees, posterior segments were the most frequently involved in both B and C fractures (Krause 2016).

> ⚠ **High-value distinctions in 41-B:**
> - **B2 vs B3:** is there a cortical split, or only depression? Read the coronal and axial CT, not the AP radiograph.
> - **Lateral vs medial:** changes the expected energy, the soft-tissue risk and the companion system (Moore).
> - **B vs C:** apply the continuity test in section 2 before finalising any B code when a metaphyseal fracture line is present.

---

## 6. Type 41-C — Complete articular

### Group C1 — Simple articular, simple metaphyseal

One articular disruption (classically a single split separating the condyles) with a simple metaphyseal component. Subgroups: without (C1.1) or with (C1.2) a fracture of the intercondylar eminence.

### Group C2 — Simple articular, wedge or multifragmentary metaphyseal

The articular component is still simple; the metaphysis is an intact wedge (C2.1), a fragmentary wedge (C2.2) or multifragmentary (C2.3). Wedge side is a qualification.

### Group C3 — Fragmented articular surface

More than one articular disruption: fragmentation of the lateral plateau (C3.1), the medial plateau (C3.2) or both (C3.3). The metaphysis may be simple or multifragmentary. In 2018 this is expressed by qualifications for **simple metaphysis**, **multifragmentary metaphysis** and **metadiaphyseal extension**, together with the quadrant letters above (mapping confirmed, section 5).

### Clinical relevance

- **Energy and soft tissues.** Type C fractures are usually high-energy. Soft-tissue condition dictates timing. Staged management (temporary spanning external fixation, then CT and definitive planning) is common practice (Gahr 2023).
- **Compartment syndrome.** In a series of 107 plateau fractures, compartment syndrome occurred in 10.3%, rising to 30.4% in Schatzker VI patterns (Chang 2000). Repeated clinical assessment is mandatory.
- **The posteromedial fragment.** A coronal-plane posteromedial fragment is common in bicondylar fractures. It was present in 59% of 111 bicondylar fractures, covering on average 25% of the plateau (Higgins 2009). Among 57 C-type fractures with medial articular involvement it was present in 42 (Barei 2008). **The AO/OTA code does not capture it.** Barei et al. found six patterns that the AO/OTA system did not describe accurately. Describe the fragment explicitly and run the column analysis in the companion reference.

> ⚠ **High-value distinctions in 41-C:**
> - **C2 vs C3:** is the articular surface one disruption or several? A depressed or comminuted zone on CT makes the articular component fragmented. This cannot be settled on radiographs.
> - **C vs B:** if any part of the articular surface still connects to the diaphysis, it is B, however dramatic the metaphysis looks.

---

## 7. Writing the full code

```
41  B  3  .1  (u)       [ ... ]
│   │  │   │   │          └─ universal modifiers, square brackets, optional
│   │  │   │   └─ qualifications, round brackets, lowercase, optional
│   │  │   └─ subgroup
│   │  └─ group
│   └─ type
└─ bone 4 (tibia) + segment 1 (proximal)
```

**Universal modifiers** (2018; optional, at the surgeon's discretion), in square brackets and comma-separated:

| No. | Modifier | Relevance in segment 41 |
|---|---|---|
| 1 / 2 | Nondisplaced / displaced | Common |
| 3 | Impaction (3a articular, 3b metaphyseal) | Depression patterns |
| 4 | No impaction | — |
| 5 | Dislocation (5a anterior … 5f multidirectional) | Fracture-dislocations (Moore patterns) |
| 6 | Subluxation / ligamentous instability (6a–6f) | Rim and condylar fracture-dislocations |
| 7 | Diaphyseal extension | Metadiaphyseal patterns |
| 8 | Articular cartilage injury (ICRS grade, 8a–8e) | When documented arthroscopically/MRI |
| 9 | Poor bone quality | Older patients, low-energy patterns |
| 12 | Associated with a non-arthroplasty implant | Prior fixation hardware |

(10 replantation, 11 associated amputation, 13 spiral-type, 14 bending-type also exist.)

---

## 8. Worked examples

*Synthetic vignettes, written for teaching. They do not describe real patients and must not be reused as evaluation cases.*

### Example 1 — Lateral split-depression, central

**Vignette:** 71-year-old woman, low-energy fall. AP and lateral radiographs show a lateral plateau split with a depressed zone. CT (native, multiplanar):
- a **true split component**: a separate lateral cortical fragment, bounded by a fracture line through the lateral cortex and the articular margin
- a centrally located depressed segment
- no metaphyseal fracture
- medial plateau intact and continuous with the diaphysis

**Reasoning:**
1. Articular involvement: yes. Medial plateau continuous with diaphysis → **B**.
2. A true split component (a separate cortical fragment) **and** a depressed zone → **B3**. Without a separate split fragment — lateral cortex intact — the same depression would be **B2**.
3. Lateral plateau, split not running through the spines → **B3.1**.
4. Depression central → qualification **(x)**.

```yaml
ao_ota_classification:
  segment: "41"
  imaging_basis: native_multiplanar_ct
  confidence_scale: "ordinal, imaging-limited; not a calibrated probability (provisional caps, section 9)"
  primary:
    code: "41B3.1(x)"
    description_label: "Partial articular, split-depression, lateral plateau, central depression"
    confidence: 0.58
    rationale: "CT shows a separate lateral split fragment and a separate central depressed zone; medial plateau intact."
  differentials:
    - code: "41B2.1(x)"
      confidence: 0.20
      rationale: "Only if multiplanar review shows no separate split fragment (lateral cortex intact): the depression is then the only articular injury."
    - code: "41B3.3"
      confidence: 0.10
      rationale: "If the split line is judged to exit through the tibial spines."
  image_quality_caveats: []
  what_would_change_the_classification:
    - "Coronal and axial CT confirming whether a separate split fragment exists (B3) or the lateral cortex is intact (B2)."
  requires_surgeon_confirmation: true
  reason_for_confirmation: "Split-depression vs pure depression changes the fixation discussion (buttress vs elevation with subchondral support)."
```

### Example 2 — Medial split, incomplete metaphyseal line (B vs C)

**Vignette:** 34-year-old man, high-energy varus injury. Radiographs: displaced medial plateau split. CT:
- a coronal-plane medial split fragment with a posteromedial extension; no depression
- an incomplete oblique line runs from the split into the metaphysis but stops short of the lateral cortex
- the lateral plateau and its articular surface remain continuous with the shaft through intact bone

Documented examination: symmetric foot pulses, peroneal nerve intact; no subluxation on imaging.

**Reasoning:**
1. Articular involvement: medial plateau.
2. Continuity test: the lateral plateau, with its part of the articular surface, is still attached to the shaft through intact bone → **B**. What decides this is the extent of the metaphyseal line, not how displaced it is.
3. True split, no depressed zone → **B1** (a depressed medial zone would make it B3) → medial → **B1.2**.
4. Medial pattern → the companion reference's **screening prompt** applies: examination for instability and neurovascular injury. This is not by itself a fracture-dislocation diagnosis.

```yaml
ao_ota_classification:
  segment: "41"
  imaging_basis: native_multiplanar_ct
  confidence_scale: "ordinal, imaging-limited; not a calibrated probability (provisional caps, section 9)"
  primary:
    code: "41B1.2"
    description_label: "Partial articular, split, medial plateau"
    confidence: 0.58
    rationale: "Medial split; the metaphyseal line is incomplete and the lateral plateau remains continuous with the shaft."
  differentials:
    - code: "41C1.1"
      confidence: 0.25
      rationale: "If multiplanar review shows the metaphyseal line is complete, so that no articular part remains attached to the shaft."
    - code: "41B3.2"
      confidence: 0.12
      rationale: "If a depressed medial zone is present in addition to the split."
  image_quality_caveats: []
  what_would_change_the_classification:
    - "Multiplanar CT review of where the metaphyseal line ends."
  requires_surgeon_confirmation: true
  reason_for_confirmation: "B vs C depends on the metaphyseal line; medial patterns need screening for instability and neurovascular injury."
```

### Example 3 — Bicondylar, fragmented articular surface, multifragmentary metaphysis

**Vignette:** 45-year-old motorcyclist. Radiographs: bicondylar fracture with metaphyseal comminution. Temporary spanning external fixator applied. CT after spanning:
- lateral plateau depression with several articular fragments
- a separate posteromedial coronal fragment
- multifragmentary metaphysis without diaphyseal extension

**Reasoning:**
1. Neither plateau is continuous with the diaphysis → **C**.
2. Articular surface fragmented on both sides (lateral depression with multiple fragments, plus the posteromedial fragment) → **C3**.
3. Both plateaus → **C3.3**. Multifragmentary metaphysis → qualification **(e)**.
4. Posteromedial fragment: describe it separately, because the code does not capture it.

```yaml
ao_ota_classification:
  segment: "41"
  imaging_basis: native_multiplanar_ct
  confidence_scale: "ordinal, imaging-limited; not a calibrated probability (provisional caps, section 9)"
  primary:
    code: "41C3.3(e)"
    description_label: "Complete articular, fragmented articular surface, both plateaus; multifragmentary metaphysis"
    confidence: 0.58
    rationale: "Articular fragmentation of both plateaus on CT; no articular segment continuous with the diaphysis; metaphysis multifragmentary."
  differentials:
    - code: "41C2.3"
      confidence: 0.22
      rationale: "If the articular component is judged a single disruption with the comminution confined to the metaphysis."
  associated_findings_not_captured_by_code:
    - "Posteromedial coronal-plane fragment"
  image_quality_caveats: []
  what_would_change_the_classification:
    - "Consensus reading of the articular CT slices: one vs several articular disruptions."
  requires_surgeon_confirmation: true
  reason_for_confirmation: "C2 vs C3 and the posteromedial fragment change approach planning."
```

---

## 9. Confidence: meaning and provisional caps

Human experts agree only moderately on tibial plateau codes, so the skill must not sound more certain than a panel of surgeons would be. Interobserver agreement for AO/OTA plateau codes has been reported as κ 0.36 (25 observers; Huitema 2022), 0.56–0.59 on CT (Yao 2022), and 0.62 at the three-column originators' centre (Zhu 2013). In Huitema 2022, observers rated their own confidence about 7/10 despite moderate or worse accuracy.

These reliability studies measure agreement between observers. They do not show how likely a given code is to be right, and they cannot be converted into probabilities.

**What the confidence number means.** It is an **ordinal, imaging-limited estimate**: it ranks how strongly the available images support one code over the alternatives, on a 0–1 scale. It is **not a calibrated probability**. No scored reference set exists yet to calibrate it. Every output states its `imaging_basis` and carries `confidence_scale: ordinal, imaging-limited; not a calibrated probability`.

**Provisional output caps.** These are maintainer guardrails, neither derived from the literature nor calibrated. They stop the stated confidence from rising above what the imaging can support. Replace them once a panel-scored reference set exists.

| Evidence available | Type (A/B/C) | Group | Subgroup | Qualifications |
|---|---|---|---|---|
| Radiographs only | ≤ 0.75 | ≤ 0.55 | ≤ 0.40 | Do not assign; state "requires CT" |
| CT as screen photos / selected images only | ≤ 0.80 | ≤ 0.65 | ≤ 0.50 | Provisional only |
| Native multiplanar CT | ≤ 0.90 | ≤ 0.75 | ≤ 0.65 | ≤ 0.60 |

If B vs C or C2 vs C3 is unresolved, say so explicitly and route to skill 06. Do not hide the uncertainty inside a single confident code.

---

## 10. What downstream skills do with a 41-x classification

| Classification | Downstream skill behaviour (educational only) |
|---|---|
| 41-A1 | Skill 07 surfaces the ligament question (MRI, cruciate/collateral injury) before the bony one. |
| 41-A2/A3 | Skill 07 discusses alignment and stability; skill 08 describes device classes for metaphyseal fixation (plates, nails, external fixation). |
| 41-B lateral | Skill 07 surfaces options from non-operative care through arthroscopically assisted, percutaneous and open techniques. Skill 08 describes screws, buttress plates, subchondral (raft) support and void fillers. |
| 41-B medial | Skill 07 surfaces the screening for instability, ligament and neurovascular injury first, then the buttressing of the medial column. |
| 41-C | Skill 07 surfaces staged management, column-specific approaches, external fixation, and — in selected older patients with non-reconstructable surfaces or pre-existing symptomatic arthritis — the primary arthroplasty discussion. Skill 08 describes dual plating, lateral locking plates, ring fixators and nails for the metadiaphyseal component. |

Skills 07 and 08 surface options and the considerations behind them. They do not recommend one over another. The surgeon decides.

---

## 11. Common misclassification patterns

| Mistake | Why it happens | How to avoid |
|---|---|---|
| Coding **B** when the metaphyseal fracture separates the whole articular block (should be **C**) | The articular injury involves one plateau, so it "looks unicondylar" | Apply the continuity test (section 2) on CT before coding any B with a metaphyseal line |
| Coding **C** when one plateau is still attached to the diaphysis (should be **B**) | Dramatic metaphyseal comminution, or fracture lines in both plateaus | Same test: what decides is whether any articular part remains continuous with the shaft, not displacement and not the number of plateaus involved |
| Letting **displacement** decide the type | The Compendium's undisplaced-fissure rule concerns segment allocation (42 vs 41) | Within 41, any line into the articular surface makes it B or C; continuity decides which |
| Coding **C1/C2** when the articular surface is fragmented (should be **C3**) | The AP shows one split; depressions hide on radiographs | Read axial and coronal CT for depressed or separate articular fragments |
| Missing a **posteromedial coronal fragment** | Invisible on the AP; not encoded by AO/OTA | Axial CT; describe it separately; run the column analysis (skill 05) |
| Missing a **posterolateral depression** | Overlaps on the AP; posterior segments are the most often involved | Lateral radiograph and CT; add qualification (u) |
| Treating a **Segond / rim avulsion** as trivial | Small bony fragment | It signals ligament injury; MRI; consider a Moore pattern |
| Folding the **fibula** into the tibial code | Pre-2018 habit | Code the fibula separately (4F) |
| Overlooking a **fracture-dislocation** | Focus on the bony pattern | Screen medial, rim and high-energy patterns for instability (skill 05). Use universal modifiers 5/6 only when dislocation or subluxation is documented |

---

## 12. Image-quality propagation

This reference assumes the case has come through skill 02 (Image Quality Check). If skill 02 flagged any of the following, **the 41 classification must restate it**:

- **No CT** → B vs C, B2 vs B3 and C2 vs C3 cannot be resolved; subgroup and qualifications are provisional.
- **CT only as screen photos or selected key images** → no multiplanar review; posterior fragments and the continuity test are unreliable.
- **No lateral radiograph** → posterior depression and slope cannot be assessed.
- **No full-length tibia** → metadiaphyseal extension cannot be assessed (affects C qualifications and Schatzker VI).
- **Spanning external fixator in place** → generally improves CT readability by restoring length; state whether the images are pre- or post-spanning.
- **Existing implants or arthroplasty** → note universal modifier 12 or a periprosthetic pattern; periprosthetic fractures are classified separately.

---

## 13. References

- Meinberg EG, Agel J, Roberts CS, Karam MD, Kellam JF. Fracture and Dislocation Classification Compendium—2018. *J Orthop Trauma.* 2018;32 Suppl 1:S1–S170. doi:[10.1097/BOT.0000000000001063](https://doi.org/10.1097/BOT.0000000000001063) — tibia pp. S49–S52, fibula pp. S61–S63. Consult directly for authoritative text and figures.
- AO Foundation. *AO/OTA Fracture and Dislocation Classification Compendium 2018 — revisions booklet* (terminology, universal modifiers, qualifications).
- AO Surgery Reference (online, free): proximal tibia, diagnosis pages per AO/OTA group.
- Barei DP, et al. Frequency and fracture morphology of the posteromedial fragment in bicondylar tibial plateau fracture patterns. *J Orthop Trauma.* 2008;22(3):176–182. doi:[10.1097/BOT.0b013e318169ef08](https://doi.org/10.1097/BOT.0b013e318169ef08)
- Higgins TF, Kemper D, Klatt J. Incidence and morphology of the posteromedial fragment in bicondylar tibial plateau fractures. *J Orthop Trauma.* 2009;23(1):45–51. doi:[10.1097/BOT.0b013e31818f8dc1](https://doi.org/10.1097/BOT.0b013e31818f8dc1)
- Krause M, et al. Intra-articular tibial plateau fracture characteristics according to the "Ten segment classification". *Injury.* 2016;47(11):2551–2557. doi:[10.1016/j.injury.2016.09.014](https://doi.org/10.1016/j.injury.2016.09.014)
- Chang YH, Tu YK, Yeh WL, Hsu RW. Tibial plateau fracture with compartment syndrome: a complication of higher incidence in Taiwan. *Chang Gung Med J.* 2000;23(3):149–155. PMID 15641218.
- Huitema JM, et al. Are 3D-printed models of tibial plateau fractures a useful addition to understanding fractures for junior surgeons? *Clin Orthop Relat Res.* 2022;480(6):1170–1177. doi:[10.1097/CORR.0000000000002137](https://doi.org/10.1097/CORR.0000000000002137)
- Yao P, et al. Intra- and inter-observer reliability assessment of widely used classifications and the "Ten-segment classification" of tibial plateau fractures. *Knee.* 2022;35:149–156. doi:[10.1016/j.knee.2022.03.002](https://doi.org/10.1016/j.knee.2022.03.002)
- Zhu Y, et al. Inter-observer reliability assessment of the Schatzker, AO/OTA and three-column classification of tibial plateau fractures. *J Trauma Manag Outcomes.* 2013;7:7. doi:[10.1186/1752-2897-7-7](https://doi.org/10.1186/1752-2897-7-7)
- Gahr P, Kopf S, Pauly S. Current concepts review. Management of proximal tibial fractures. *Front Surg.* 2023;10:1138274. doi:[10.3389/fsurg.2023.1138274](https://doi.org/10.3389/fsurg.2023.1138274)
- Cruz JP, Michaud JB, Van Rysselberghe NL, et al. Outcomes of isolated medial tibial plateau fractures by fracture morphology. *Injury.* 2024;55(8):111662. doi:[10.1016/j.injury.2024.111662](https://doi.org/10.1016/j.injury.2024.111662)
- Vogel M, Hoffman A, Revak T. Schatzker IV tibial plateau fractures: are they always unicondylar? *OTA Int.* 2024;7(3):e341. doi:[10.1097/OI9.0000000000000341](https://doi.org/10.1097/OI9.0000000000000341)
- Skill 09 (Evidence Retrieval) for live literature queries.

🩺 *Educational reference only — not medical advice. Always confirm classification with a qualified surgeon and the official AO Foundation publications.*
