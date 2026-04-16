# MAOS-MOTOR Controller and Motor Trade Matrix (v1)

Purpose: maintain a formal, versioned shortlist of motor/powertrain candidates for MAOS-MOTOR evaluation.

Scope note: This matrix is R&D guidance for Experimental Amateur-Built development and is not a certification claim.

## Decision Framework

## Source Baseline

This matrix is seeded from existing MAOS article analysis and then maintained in-repo as the formal shortlist.

- `aerocommons/content/articles/2026-04-05-maos-generator-selection.md`
- `aerocommons/content/articles/2026-03-24-understanding-aircraft-voltage.md`
- `docs/ARTICLE_KNOWLEDGE_MIGRATION_2026Q2.md`

## Name Disambiguation (Important)

- `magniX` (https://www.magnix.aero/) is an electric aviation powertrain company.
- `Magnax` (AXF series) is a different axial-flux machine vendor.

Both are included as separate candidates.

Scoring scale (per criterion):

- `0` no data / not acceptable
- `1` weak
- `2` limited
- `3` acceptable baseline
- `4` strong
- `5` leading

Primary weighted criteria (initial):

- Continuous power capability (`weight 0.20`)
- Peak power capability (`weight 0.10`)
- Specific power and mass impact (`weight 0.15`)
- Thermal path maturity (`weight 0.15`)
- Integration risk (controls + mechanical) (`weight 0.15`)
- Supplier maturity and supportability (`weight 0.15`)
- Aviation precedent / field evidence (`weight 0.10`)

Weighted score formula:

`score = sum(criterion_score * criterion_weight)`

## Candidate Matrix

| Candidate | Architecture | Continuous kW | Peak kW | Weight (kg) | Voltage Class | Max RPM | Supplier Maturity | Aviation Precedent | Current Evaluation State | Link |
|---|---|---:|---:|---:|---|---:|---|---|---|---|
| Emrax 268 | Axial flux PM | 80 | 160 | 20.4 | Up to 700V | 5000 | High | Good (experimental) | Baseline reference candidate | https://emrax.com/ |
| Emrax 228 | Axial flux PM | 50 | 100 | 12.3 | Up to 700V | 6000 | High | Good (experimental) | Undersized for some mission points; keep as lower-power reference | https://emrax.com/ |
| Beyond Aviation / Evolito AXM3 | Axial flux PM | ~100 (est.) | ~200 (est.) | ~15 (est.) | Unknown (likely HV class) | TBD | Medium | Strong signal from public aerospace programs | High-interest candidate pending direct datasheet | https://www.evolito.aero/ |
| Donut Labs Rim Motor | Rim-drive / ring motor | TBD | TBD | TBD | TBD | TBD | Medium | Limited public flight data | Active candidate, data collection | https://www.donutlab.com/ |
| **magniX Powertrain Family** | Electric aviation powertrain (motor + inverter family) | TBD | TBD | TBD | High-voltage class (public program references include 800V architectures) | TBD | High | Strong electric-flight precedent | **Added to formal shortlist; perform MAOS fit and integration-risk assessment** | https://www.magnix.aero/ |
| Magnax AXF225 | Axial flux PM | 75 | 175 | 29 | TBD | 3500 | Medium | Limited aviation evidence | RPM mismatch risk for direct-coupled high-speed ICE interfaces | https://www.magnax.com/ |
| YASA P400-R | Axial flux PM | TBD | TBD | TBD | TBD | TBD | High | Primarily automotive | Inquiry candidate pending aerospace-fit data | https://www.yasa.com/ |
| Infinitum Electric | Air-core axial flux family | TBD | TBD | TBD | TBD | TBD | Medium | Early aviation relevance, stronger industrial history | Watchlist candidate, data collection | https://infinitumelectric.com/ |

## Weighted Scoring Worksheet (Populate as Data Matures)

| Candidate | Continuous Power (0.20) | Peak Power (0.10) | Specific Power/Mass (0.15) | Thermal Maturity (0.15) | Integration Risk (0.15) | Supplier Maturity (0.15) | Aviation Precedent (0.10) | Weighted Total |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Emrax 268 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |
| Emrax 228 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |
| Beyond Aviation / Evolito AXM3 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |
| Donut Labs Rim Motor | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |
| **magniX Powertrain Family** | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |
| Magnax AXF225 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |
| YASA P400-R | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |
| Infinitum Electric | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00 |

## Minimum Evidence Required Before Downselect

1. Datasheet-backed continuous and peak operating points at relevant thermal boundary conditions.
2. Controller and bus compatibility assumptions mapped to MAOS voltage and redundancy architecture.
3. Thermal derating behavior and sensor coverage for fault detection and health monitoring.
4. Integration notes for mechanical mounting, cooling, and control interface semantics.
5. Supplier support and lead-time assumptions documented with date-stamped source references.

## Next Actions

1. Replace `TBD` values with source-backed data (datasheet or direct vendor response).
2. Record explicit assumptions for missing data fields and assign owner/date.
3. Run first-pass weighted scoring review at S1-C trade closure board.
4. Request direct technical data from magniX on model family fit for MAOS voltage and redundancy architecture.
5. Publish deltas as revisioned updates in this document.
