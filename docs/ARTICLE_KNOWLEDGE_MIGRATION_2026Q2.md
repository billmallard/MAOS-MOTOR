# MAOS-MOTOR Article Knowledge Migration (2026 Q2)

Purpose: Capture propulsion and motor decisions developed in aerocommons articles and convert them into actionable MAOS-MOTOR project context.

Scope note: This is R&D guidance for Experimental Amateur-Built development. It is not a certification claim.

## Source Articles

- 2026-03-24-voltage-decision-400vdc.md
- 2026-03-25-donut-labs-motors-rim-drive-propulsion.md
- 2026-03-26-motor-demagnetization-silent-killer.md
- 2026-04-05-maos-generator-selection.md
- 2026-04-05-maos-propulsion-redundancy-battery.md
- 2026-04-05-maos-1g1b2m-architecture-decision.md

## Imported Decisions and Working Baseline

- Electrical baseline remains 400 VDC for MAOS Phase 1 integration simplicity and component availability.
- Propulsion redundancy baseline is dual electric propulsion channels (2M) on a common thrust axis to avoid asymmetric-thrust handling burden while preserving degraded-flight capability after one motor-channel loss.
- Power architecture guidance from system studies should be treated as upstream constraints for motor/controller sizing.
- Thermal behavior at sustained high load is a first-order design driver, not a secondary packaging issue.

## Motor Technical Guidance to Carry Into This Repo

- Demagnetization risk must be treated as a monitored hazard state.
- Controller thermal margin and winding temperature margin need explicit operating limits and telemetry.
- Cooling architecture must be validated for low-density air operation at altitude where convective cooling is reduced.
- Candidate motor trade studies should preserve a phased path:
  - Phase 1: lower integration risk and known components.
  - Phase 2: higher-specific-power options when thermal and controls confidence is proven.

## Battery and Bus Coupling Implications for MAOS-MOTOR

- Emergency reserve assumptions from propulsion studies imply sustained motor operation at reduced but controlled power for contingency segments.
- Motor efficiency maps, controller efficiency, and thermal derating curves are required inputs to system-level reserve validation.
- The motor team should publish envelope boundaries that upstream flight/energy planning can consume directly.

## Open Decisions Assigned to MAOS-MOTOR

- Finalize motor candidate shortlist with weighted criteria (mass, continuous kW, peak kW, thermal path, supplier maturity).
- Add and evaluate magniX powertrain family as a formal candidate in the motor trade matrix.
- Define controller redundancy strategy at motor-channel level (independent vs shared failure domains).
- Establish measurable thermal derating policy and fault thresholds for SIL/HIL use.
- Confirm altitude cooling requirements and required test instrumentation.

## Immediate Work Items

1. Create a motor-controller trade matrix document in this repo with weighted scoring. (Done: `docs/MOTOR_CONTROLLER_TRADE_MATRIX.md`)
2. Draft motor thermal limits and telemetry interface contract for MAOS-FCS and MAOS-ECS integration.
3. Define bench test profile set: continuous cruise-equivalent load, repeated boost bursts, and fault-injection thermal recovery.
4. Publish a v0 motor operating envelope artifact for system integration.

## Suggested Deliverables to Add Next

- docs/MOTOR_CONTROLLER_TRADE_MATRIX.md
- docs/MOTOR_THERMAL_LIMITS_AND_FDIR_SIGNALS.md
- docs/MOTOR_OPERATING_ENVELOPE_V0.md
