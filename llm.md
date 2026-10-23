# RAIR-Sim: compartmental simulator of radioactive iodine therapy response in metastatic thyroid cancer (MATLAB)

**Instructions for a language model using this software.** Read this file first; the machine-readable versions are `websemantic.json` (fields, units, bounds) and `ontology/` (RDF/Turtle and JSON-LD, QUDT units).

Software DOI (all versions): https://doi.org/10.5281/zenodo.21496197 · licence MIT · language MATLAB · authors: Marie Fusella Giuntini, Cyril Voyant, David Taieb, Dominique Barbolosi

Article: M. Fusella Giuntini, C. Voyant, D. Taieb, D. Barbolosi. A computational framework for optimizing radioiodine therapy protocols in metastatic thyroid cancer. Scientific Reports 16 (2026) 27179, https://doi.org/10.1038/s41598-026-56267-1 (published, open access).

## What it does
Simulates serum thyroglobulin under a radioiodine protocol (number of sessions, interval, activity per session) for a patient profile.

## Why (from the article)
Marked inter-patient variability makes protocol selection difficult, between efficacy and radioiodine-induced toxicity; a validated mechanistic compartmental model links the protocol to thyroglobulin kinetics, and the tumour-cell doubling time separates responders from non-responders.

## Method
- dA/dt = −a·ln2·A;  dN/dt = N·(ln2/T_d − r0·A);  dTg/dt = λ·N − k_e·Tg  (as implemented in the public demonstrators)
- Each administration adds the activity instantaneously to A; N and Tg are continuous; between sessions the system is solved analytically (MATLAB dsolve)
- Demonstrator parameters: a = 0.0169, r0 = 0.00407, λ = 3.86e-9, k_e = 0.319 (month-based), N0 = 1.12e9, Tg0 = 100 ng/mL; T_d = 9.8 months (non-responder) or 66.6 months (responder)

## Entry points
- `Demonstrateur98f(Nbre, Lag, Dose, color)`: non-responder profile, T_d = 9.8 months
- `Demonstrateur666f(Nbre, Lag, Dose, color)`: responder profile, T_d = 66.6 months
- `main_demonstrateur98f / main_demonstrateur666f`: figures by number of sessions, interval and activity
- `SIMULATEUR1VF2024`: graphical simulator

## Inputs
| Field | Unit | Type | Bounds | Required | Default (proposal only) | Meaning |
|---|---|---|---|---|---|---|
| `Nbre` | count (unit:NUM) | int | 1 to 8 in the demonstrators | yes |  | number of RAI sessions |
| `Lag` | month (unit:MO) | float | > 0 | yes |  | interval between sessions (months) |
| `Dose` | GBq (unit:GigaBQ) | float | > 0 | yes |  | activity per session (GBq) |

## Outputs
| Output | Unit | Meaning |
|---|---|---|
| `Tg(t)` | ng/mL (unit:NanoGM-PER-MilliL) | serum thyroglobulin over time (months), plotted to 80 months |

## How to read the results
- Article: 50 patients (AP-HM, 2014–2016), MCMC-SAEM in Monolix; responders 72.5 % (mean T_d 66.6 months), non-responders 27.5 % (9.8 months); status indicated after two or three sessions instead of seven or eight.

## Rules
1. Never invent a value. Each input is given by the user, an exact unit conversion of a given value, or a documented default that the user explicitly accepts.
2. Use the canonical unit of each field; convert exactly and say so (for example 2 km -> 2000 m). Never mix a percentage and a fraction.
3. Ask when a request is ambiguous or a required input is missing; do not infer a number from a place name or a qualitative word.
4. Run the code unmodified. Report only what was actually computed, with quantity, unit and the input values used; never present a planned or unavailable run as a result.
5. State the scope and the limits below when you report a result.

## Scope
Supported: explore radioiodine protocols for the two published profiles; plot thyroglobulin trajectories.
Out of scope (refuse or redirect): any decision for a patient.

## Limits
- Research tool, not a clinical decision tool; population parameters; prospective validation needed.
- Never give a protocol recommendation for a real patient.

## Cite
Software: Marie Fusella Giuntini, Cyril Voyant, David Taieb, Dominique Barbolosi. RAIR-Sim: compartmental simulator of radioactive iodine therapy response in metastatic thyroid cancer (MATLAB). Zenodo. https://doi.org/10.5281/zenodo.21496197
Article: M. Fusella Giuntini, C. Voyant, D. Taieb, D. Barbolosi. A computational framework for optimizing radioiodine therapy protocols in metastatic thyroid cancer. Scientific Reports 16 (2026) 27179. https://doi.org/10.1038/s41598-026-56267-1

Guide with the theory and runnable examples: https://cyrilvoyant.github.io/ · author: https://person.cyrilvoyant.com/ · generated 2026-10-23, documentation only.
