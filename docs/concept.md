---
title: asymtrack — Concept v0.1
author: Egon Leitner
type: wissen
keywords: [asymtrack, Symptomtagebuch, ePRO, MDR, DiGA, Konzept]
status: entwurf
created: 2026-09-02
modified: 2026-09-02
frontmatter_version: 5
description: Erste Konzeptfassung für asymtrack, inklusive regulatorischer Abgrenzung, Evidenzlage und offener Entscheidungen.
---

# asymtrack — Concept (v0.1)

> **Status:** first draft, 2026-09-02. Nothing here is decided. The technology stack is
> deliberately left open. Sections marked *UNVERIFIED* contain third-party input that has
> not been checked against primary sources.

## 1. Idea in one paragraph

A patient (or a not-yet-patient) records symptoms, measurements and general wellbeing on
their own phone or tablet. The record is structured so that it is useful to a physician. In
a later stage, a physician may hand the patient a question set derived from a diagnosis or a
suspected diagnosis. The name is a contraction: **A**nother **Sym**ptom **Track**er.

## 2. Why this might be worth building

- Symptom diaries are anchored in German clinical guidelines. The headache diary appears in
  AWMF 030/057 and in the corresponding patient guideline; blood pressure self-measurement
  is established in the NVL Hypertonie and in the ESC guidelines.
- Existing apps score poorly. Stiftung Warentest rated no headache app better than
  "befriedigend" (best: 2.6 for M-sense and Kopfschmerzwissen). The main criticisms were
  insufficient capture of medical history and missing evidence of benefit.
- Structured self-documentation has a measurable effect on care processes even where it has
  no effect on mortality (see section 3).

## 3. Evidence base, stated honestly

| Claim | Confidence | Source |
|---|---|---|
| ePRO monitoring improves symptom control, quality of life and reduces emergency visits | high | PRO-TECT secondary endpoints, HR 0.84 for time to first emergency visit |
| ePRO monitoring improves survival | **not established** | Basch et al. JAMA 2017 (single centre, n=766) was positive; PRO-TECT (52 practices, n=1191), powered for overall survival, was null: HR 0.99, 95% CI 0.83 to 1.17, p=0.86 |
| Patient education on self-measurement improves adherence and BP control | very low certainty | NVL Hypertonie: evidence carries unclear or high risk of bias |

**Consequence for positioning:** do not market a survival or outcome claim. Claim what is
defensible: better documentation, better conversations, earlier detection of medication
overuse.

## 4. Regulatory boundary, the decisive constraint

Under MDCG 2019-11 (Rev. 1, June 2025), software that only records, stores and displays
information is generally **not** a medical device. The guidance names diaries recording
insulin doses as an example. A medical purpose arises once the software derives an
assessment from the data. Classification then follows MDR Annex VIII, Rule 11.

MDCG explicitly permits a **modular approach**: a product may consist of medical-device and
non-medical-device modules.

This yields a clear line for the project:

| Stays outside MDR | Crosses into MDR |
|---|---|
| Patient records freely chosen items | App derives a risk, score or recommendation |
| App displays and exports what was entered | App triages, alerts or interprets |
| Physician composes a question set as a free form | Question set is bound to a diagnosis and the result feeds a clinical decision |

Additional regimes that apply regardless of MDR status:

- **GDPR Art. 9** — health data, special category. The highest-risk asset in the project.
- **EU AI Act** — relevant only if a model contributes to assessment. A knowledge base
  exists at `50.20.40.EU-AI-Act`.
- **DiGA route (SGB V 33a, 139e)** — reimbursement path via the BfArM fast track, three
  months after complete submission, risk classes I, IIa, IIb. Requires proof of positive
  care effects, and BSI TR-03161 certification has been mandatory since 2025-01-01. From
  2026-01-01 at least 20 percent of the permanent reimbursement amount is
  success-dependent, and the accompanying success measurement (AbEM) started on the same
  date. **Out of scope for any early version.**

## 5. Interoperability: "useful to the physician" is an integration problem

Physicians do not read apps. They read their practice management system. In Germany the path
there is the ePA with MIOs based on FHIR; since ePA 3.0 there is a data-based FHIR component
alongside the document-based one. The first MIO, the electronic medication plan, is intended
to be usable from 2026. **There is no MIO for symptom diaries.**

Practical consequence: a v1 cannot integrate. The cheapest honest channel is an export that
the patient carries to the appointment, as PDF or print.

## 6. Open decisions

1. **Product or exercise?** Whether this pursues revenue changes the answer to nearly
   everything below.
2. **One indication or indication-agnostic?** Indication-agnostic multiplies validated
   question sets, professional societies and competitors. Recommendation from the critical
   review: start with exactly one.
3. **Technology stack.** Deliberately open. Options considered: PHP/SQLite PWA following the
   existing MioDato pattern; local-first PWA with IndexedDB; native app.
4. **Does the physician get an account in v1?** The critical review argues no: the physician
   is not the user but the bottleneck. There is no EBM billing code for assigning a question
   set in an app.

## 7. Recommended shape of a first version

Derived from sections 4 and 6, chosen to stay demonstrably outside MDR:

- One indication.
- Patient-side capture only, no physician account.
- No scoring, no interpretation, no recommendation.
- Output is an export the patient brings to the appointment.
- Data stays on the device unless the patient exports it.

## 8. Candidate indications, UNVERIFIED

The following list was supplied by a third-party AI and is recorded as raw input. It has not
been checked against guidelines, market density or data complexity, and it is **not** a
prioritisation.

**Cardiovascular and metabolic:** diabetes mellitus (type 1 and 2), arterial hypertension,
heart failure.

**Neurological and psychiatric:** migraine and chronic headache, epilepsy, depression and
bipolar disorder.

**Respiratory:** asthma bronchiale, COPD.

**Gastroenterology and allergology:** irritable bowel syndrome, inflammatory bowel disease
(Crohn's disease, ulcerative colitis), food allergies and intolerances.

**Rheumatology and chronic pain:** rheumatoid arthritis, fibromyalgia.

Partially corroborated during research: the headache diary (AWMF 030/057; DGN MOH guideline
2022, valid to 2026-11-30) and blood pressure self-measurement (NVL Hypertonie, ESC).
Everything else in this list remains unchecked.

## 9. Known competitors

| Product | Indication | Note |
|---|---|---|
| M-sense (Newsenselab, Berlin) | migraine | Warentest 2.6, best in test; free basic tier, paid therapy tier |
| Migräne App (Schmerzklinik Kiel) | migraine | built with Schmerzklinik Kiel and TK; free |
| DMKG app | headache | free, ad-free, published by the professional society itself |
| Kopfschmerzwissen | headache | Warentest 2.6 |

Not researched: Cara Care (IBS) and Kalmeda (tinnitus), both DiGA.

## 10. Sources

- MDCG 2019-11 Rev. 1, qualification and classification of software under MDR and IVDR
- MDR Annex VIII, Rule 11
- BfArM DiGA-Leitfaden v3.5; SGB V 33a and 139e; DiGAV
- Basch et al., JAMA 2017;318(2):197-198
- PRO-TECT cluster-randomised trial, Nature Medicine 2025
- Stiftung Warentest, headache and migraine apps
- AWMF 030/057 (migraine); DGN MOH guideline 2022; NVL Hypertonie (AWMF nvl-009)
- KBV MIO and gematik INA; ePA 3.0 FHIR

## 11. Research limitations

Cara Care and Kalmeda were not researched. The G-BA DMP requirements on peak-flow and blood
glucose self-documentation were not checked against primary sources. TR-03161 and the DiGAV
details rest on secondary sources only.
