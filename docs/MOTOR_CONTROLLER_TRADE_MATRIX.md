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

Cost guardrails (added for v1.1 budget track):

- Target propulsion electric machines: `<= $10k motor` and `<= $10k generator`
- Stretch target: `<= $20k combined motor + generator`
- Practical near-term target for 120-220 kW class: `<= $30k combined` using mixed new/used supply

Weighted score formula:

`score = sum(criterion_score * criterion_weight)`

## Budget Track: Motor + Generator Candidates (Wide Net)

Purpose: identify candidates that can credibly hit or approach the MAOS cost target while maintaining useful continuous power and manageable integration risk.

| Candidate Pairing | Motor Role | Generator Role | Combined Continuous Power Class | Combined Price Anchor (USD) | Data Confidence | Notes |
|---|---|---|---|---:|---|---|
| Hyper9 + Hyper9 HV (new) | NetGain Hyper9 AC-X1 kit | NetGain Hyper9 HV AC-X144 kit (run as generator) | ~90-120 kW class | **~11,000** (`$5,400 + $5,600`) | High | Closest off-the-shelf match to the `$10k + $10k` goal. Includes controllers in kit pricing. Lower power than HPDM-180 class. |
| Hyper9 + used Hyper9 (mixed) | New Hyper9 kit | Used/refurb Hyper9 kit | ~90-120 kW class | **~8,000-11,000** | Medium | Strong budget option for prototype phase. Requires used-market screening and bench qualification. |
| Tesla Model 3 rear DU + Hyper9 | Tesla M3 rear DU (`220 kW`, `88 kg`) + T-2C VCU | Hyper9 HV kit as generator | 120-220 kW class | **~18,199** (`$9,900 + $2,699 + $5,600`) | High | High propulsion headroom with budget generator. T-2C required for DU control. Heavier than aerospace-targeted motors. |
| Tesla Model 3 rear DU + Tesla M3 rear DU | Tesla M3 rear DU + T-2C VCU | Tesla M3 rear DU + T-2C VCU (generator mode capable in principle) | 180-220+ kW class | **~25,198** (`2× ($9,900 + $2,699)`) | Medium | Attractive cost/power. Two T-2C units required (one per DU). Integration complexity and control strategy risk are high for aviation use. |
| Tesla Model S LDU + Hyper9 HV | Tesla Model S LDU (`400 kW`, `295 lb`) + T-2C VCU | Hyper9 HV | 180-300+ kW class | **~20,199** (`$11,900 + $2,699 + $5,600`) | High | Very high power, but mass penalty is significant. T-2C required for LDU control. Better fit for "go-fast" architecture than efficiency build. |
| AMR-250-90 + Hyper9 HV | AMR 250-90 (`210 hp peak`, `150 lb`) | Hyper9 HV | ~120-180 kW class | **~11,000** (`$5,400 sale + $5,600`) | Medium | Price is currently sale-sensitive. Good near-target cost if inventory remains available. |
| EMRAX 228 + Hyper9 HV | EMRAX 228 (`75 kW cont`, `124 kW peak`) | Hyper9 HV | ~75-120 kW class | **~16,000-24,000** (est.) | Low | Strong mass and efficiency; cost likely above budget target without discount or used channel. |
| HPDM-180R + HPDM-180R | H3X HPDM-180R | H3X HPDM-180R | `180 kW` class | **~40,000-80,000** (est.) | Low | Performance leader; cost out of target for budget track. Keep as premium reference. |

### Budget Track Findings (Current)

- A credible `$10k + $10k` class solution exists today only in EV-conversion ecosystems (Hyper9-family, Tesla salvage channels, Remy/AMR sale channels).
- In the 120-220 kW class, the practical near-term combined target is `~$15k-$30k` unless used inventory and sale pricing are aggressively leveraged.
- If strict mass is prioritized, cost rises quickly toward premium aerospace motor classes.
- If strict cost is prioritized, mass and integration complexity increase (especially Tesla-based solutions).

### Source Anchors (Date: 2026-04-16)

- EV West Hyper9 AC-X1 kit: `$5,400`, rated `120 HP`, `173 lb-ft`, `120 lb`
- EV West Hyper9 HV AC-X144 kit: `$5,600`, peak `88 kW`, rated `120 HP`, `172 lb-ft`, `120 lb`
- EV West Tesla Model 3 rear DU starter kit: `$9,900`, up to `220 kW`, `194 lb`
- EV West Tesla Model S LDU starter kit: `$11,900`, up to `400 kW`, `295 lb`
- EV West AMR 250-90 listing: `$10,900` list / `$5,400` sale, peak `210 HP`, `150 lb`
- EMRAX 228 page: `75 kW` continuous, `124 kW` peak, `12.9-13.5 kg`
- EV Controls T-2C VCU: `$2,699` per unit (EV West, 2026-04-22); one required per Tesla DU — see below

---

### Required Control Element: EV Controls T-2C for All Tesla Drive Units

Any Tesla drive unit option in this matrix requires the **EV Controls T-2C Vehicle Control Unit** to be operable. The Tesla inverter firmware is proprietary and does not expose a standard external command interface without it. The T-2C reflashes the inverter firmware (one-time, locked to that specific DU serial number) and then provides the external control interface.

**What the T-2C provides:**

| Feature | Details |
|---|---|
| Command interface | Analog 0–5 V throttle input per DU — not a CAN torque command |
| CAN telemetry output | `.dbc` file supplied; decodes RPM, power (kW), current, HV bus voltage, inverter temperatures, gear state |
| Drive mode control | Drive / Neutral / Reverse via discrete inputs |
| Accessory outputs | Contactor control, cooling fan, brake/regen lights, reverse light |
| Connectivity | Bluetooth + Wi-Fi; EV-Controls Dash app (iOS) for configuration and data logging |
| Weight | 0.5 kg |
| Unit pricing | $2,699 (EV West, 2026-04-22) |
| Compatibility | Model S/X large and small rear DU; Model 3 rear DU; dual-motor S/X P85/90/100D |

**Critical constraint:** The T-2C firmware reflash is one-time and bound to a specific DU. A replacement inverter board requires a new T-2C purchase. Dual-DU configurations (B4, H-Budget-2) require **two T-2C units**.

**Aviation-specific integration concerns:**

| Concern | Detail | Severity |
|---|---|---|
| Analog command interface | MAOS FCS must drive a DAC (0–5 V) per DU rather than CAN torque commands; closed-loop motor control adds a DAC and ADC round-trip in the latency chain | Medium |
| Command determinism | T-2C is an automotive VCU; state-transition timing and torque response latency are not characterized for flight control use | Medium — bench characterization required before closed-loop integration |
| Firmware lock-to-DU | Replacement inverter board = new T-2C purchase ($2,699); plan accordingly for bench test attrition | Low (cost impact only) |
| CAN telemetry adequacy | RPM, power, temps, HV bus available via `.dbc` — sufficient for MAOS motor telemetry requirements without additional bridge | Positive |
| Fail-state behavior | T-2C fail-state (power loss, watchdog) must be characterized — does it fail to zero torque or hold last command? | Medium — required bench test item |

**Net effect on integration risk:** Tesla options remain rated **High** integration risk until bench characterization of the T-2C analog command interface and fail-state behavior is complete. If bench data confirms deterministic response within MAOS FCS latency budget, risk can be revised to **Medium**. The T-2C makes the interface tractable; it does not make it proven for flight.

All Tesla DU cost entries below have been updated to include `$2,699` T-2C per DU.

## Generator Strategy Notes (Low-Cost Track)

- PMSM traction motors can generally be used in generating mode with appropriate inverter control and DC bus management.
- For low-cost prototype architecture, using the same motor family for propulsion and generation reduces controls heterogeneity.
- Required bench validation before flight use:
	1. Continuous generating duty at thermal steady-state
	2. DC bus regulation stability under load transients
	3. Fault behavior under over-voltage, over-current, and coolant degradation
	4. Controller restart behavior and deterministic state transitions

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

## Budget-Focused Candidate Matrix (Motor + Generator Pairings)

| Pairing ID | Motor Candidate | Generator Candidate | Motor Cost | Generator Cost | Combined Cost | Continuous Class | Mass Risk | Integration Risk | Budget Fit |
|---|---|---|---:|---:|---:|---|---|---|---|
| B1 | Hyper9 AC-X1 | Hyper9 HV AC-X144 | 5,400 | 5,600 | **11,000** | 90-120 kW | Medium | Medium | **Strong** |
| B2 | Hyper9 AC-X1 | Hyper9 AC-X1 (used) | 5,400 | 2,500-5,400 | **7,900-10,800** | 90-120 kW | Medium | Medium | **Strong** |
| B3 | Tesla M3 rear DU + T-2C | Hyper9 HV AC-X144 | 12,599 | 5,600 | **18,199** | 120-220 kW | High | High | Acceptable |
| B4 | Tesla M3 rear DU + T-2C | Tesla M3 rear DU + T-2C | 12,599 | 12,599 | **25,198** | 180-220+ kW | High | High | Weak — cost now approaches premium territory |
| B5 | AMR-250-90 | Hyper9 HV AC-X144 | 5,400-10,900 | 5,600 | **11,000-16,500** | 120-180 kW | High | Medium | Acceptable |
| B6 | HPDM-180R | HPDM-180R | 20,000-40,000 | 20,000-40,000 | **40,000-80,000** | 180 kW | Low | Low | Weak |

### Budget Pairings Quick-Look (`$/kW continuous`)

Assumptions for quick estimate:

- Hyper9-family pairings use `~90 kW` continuous class
- Tesla M3 + Hyper9 uses `~120 kW` continuous class
- Tesla M3 + Tesla M3 uses `~180 kW` continuous class
- AMR-250-90 + Hyper9 uses `~120 kW` continuous class

| Pairing ID | Combined Cost (USD) | Continuous Class (kW) | Approx. `$/kW` |
|---|---:|---:|---:|
| B2 | 7,900-10,800 | 90 | **88-120** |
| B1 | 11,000 | 90 | **122** |
| B5 | 11,000-16,500 | 120 | **92-138** |
| B3 | 18,199 | 120 | **152** |
| B4 | 25,198 | 180 | **140** |
| B6 | 40,000-80,000 | 180 | **222-444** |

## Recommended Budget Shortlist (Current)

For immediate MAOS budget-track investigation:

1. **B1 (Hyper9 + Hyper9 HV)**
	- Best direct alignment with target cost and low procurement friction.
	- Recommended first bench architecture for rapid integration learning.
2. **B3 (Tesla M3 rear DU + T-2C + Hyper9 HV)**
	- Best cost/performance compromise for the 120-220 kW class.
	- Updated cost $18,199 (was $15,500) — T-2C VCU is a required element, not optional.
	- T-2C analog command interface (0–5 V throttle) must be bench-characterized for MAOS FCS latency compatibility before closed-loop integration.
	- Recommended if speed target pushes above 170 KTAS and mass impact is acceptable.
3. **B5 (AMR-250-90 + Hyper9 HV)**
	- Attractive when sale pricing exists; check inventory volatility.
	- Keep as opportunistic path, not baseline, due to price sensitivity.

Reference-only benchmark:

- **B6 (HPDM-180R pair)** remains the performance benchmark but is outside budget-track intent.

## Parallel Path Execution (Turbine Path T and Hayabusa Path H)

This program now proceeds on two simultaneous powerplant tracks.

### Path T (M250 Turbine)

Preferred objective:
- 220-260 KTAS class, high-altitude family-travel mission.

Current motor/generator pairings to run in parallel:

| Path T Option | Generator Candidate | Propulsion Motor Candidate | Cost Anchor | Fit Summary |
|---|---|---|---:|---|
| T-Budget-1 | Hyper9 HV AC-X144 | Tesla Model 3 rear DU + T-2C | **$18,199** | Best immediate budget/power compromise; T-2C adds $2,699 vs. prior estimate |
| T-Budget-2 | Hyper9 HV AC-X144 | Tesla Model S LDU + T-2C | **$20,199** | Max power headroom, high mass; T-2C adds $2,699 |
| T-Budget-3 | Tesla M3 rear DU + T-2C (gen mode) | Tesla M3 rear DU + T-2C | **$25,198** | Symmetric architecture; two T-2C units required; control complexity high |
| T-Premium | HPDM-350 | HPDM-350 | $40k-$80k+ | Best technical fit, high cost |

### Path H (Hayabusa Single/Twin)

Preferred objective:
- 160-200 KTAS class with strongest price-performance and lower fuel burn.

Current motor/generator pairings to run in parallel:

| Path H Option | Generator Candidate | Propulsion Motor Candidate | Cost Anchor | Fit Summary |
|---|---|---|---:|---|
| H-Budget-1 (single ICE) | Hyper9 HV AC-X144 | Hyper9 AC-X1 | **$11,000** | Closest to target economics |
| H-Budget-2 (twin ICE) | 2x Hyper9 HV AC-X144 | Tesla Model 3 rear DU + T-2C | **$23,799** | Redundancy plus speed headroom; T-2C adds $2,699 |
| H-Budget-3 (single/twin ICE) | Hyper9 HV AC-X144 | Tesla Model 3 rear DU + T-2C | **$18,199** | Strong compromise option; T-2C adds $2,699 vs. prior estimate |
| H-Premium | 2x HPDM-180R | HPDM-180R | $60k-$120k | Technical benchmark only |

### Shared vs Path-Specific Work

Shared (execute once, feed both paths):
1. Bench characterization of Hyper9-family generator-mode behavior.
2. Tesla DU control-loop and thermal characterization as propulsion machine.
3. DC bus protection and fault-state logic.

Path-specific:
1. M250 path: part-power SFC mapping and altitude optimization.
2. Hayabusa path: continuous-duty endurance and reduction-drive durability.

Immediate decision aid:
- If budget priority dominates, start with H-Budget-1.
- If speed priority dominates, start with T-Budget-1.
- If dual-track budget allows, run both in parallel and compare `$/NM` and `KTAS per installed kg`.

Interpretation:

- `Strong`: Meets or is near the `$10k + $10k` target.
- `Acceptable`: Above ideal but plausible for prototype and early flight article.
- `Weak`: Out of budget-track intent; retain as high-performance benchmark only.

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
6. Run bench-level generator-mode validation plan for Hyper9 and Tesla DU candidates (continuous thermal and control stability).
7. Add a `$/kW continuous` column for all budget-track pairings.
8. Expand used-market capture process (minimum acceptance criteria for salvage motor/generator purchases).
