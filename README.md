# MAOS-MOTOR

Open-source electric propulsion motor subsystem development for MAOS hybrid-electric aircraft concepts.

## Status

Concept and architecture phase.

## Safety Notice

This repository is for research and experimental development only. It is not approved for manned flight and must not be used as-is in safety-critical operation without formal system safety assessment, verification, validation, and regulatory compliance.

This project targets the Experimental Amateur-Built category. FAA certification is not a current design constraint, but engineering decisions should still follow conservative aerospace and safety-critical best practices where practical.

## Role in MAOS Multi-Project Architecture

This repository owns the MAOS electric motor and drive domain.

- Electric propulsion motor selection and operating envelope definitions.
- Motor control, inverter interface assumptions, and health monitoring behavior.
- Subsystem simulation, bench-test strategy, and verification artifacts.

Related repositories:

- MAOS-DESIGN owns aircraft-level geometry, packaging, and integration constraints.
- MAOS-FCS owns flight-control computation and flight-critical control paths.
- MAOS-ICE owns internal combustion generator-engine subsystem development.
- aerocommons is the website and program-level communications hub.

## Mission

Develop a practical and robust electric propulsion motor subsystem that supports MAOS hybrid-electric architecture with explicit interface contracts, deterministic control behavior, and traceable fault handling.

## Scope

In scope:

- Motor architecture trade studies and operating envelope definition.
- Motor control and inverter interface requirements.
- Thermal, power, and sensing interface definitions for propulsion operation.
- Fault detection and degraded-operation behavior for motor subsystem failures.
- Simulation and bench-test verification artifacts.

Out of scope:

- Aircraft-level geometry governance and top-level configuration control (owned by MAOS-DESIGN).
- Primary flight-control law ownership (owned by MAOS-FCS).
- Internal combustion engine ownership (owned by MAOS-ICE).

## Interface-First Rules

Before detailed implementation, freeze and version:

- Electrical interfaces: HV bus limits, current limits, startup/inrush behavior, and grounding assumptions.
- Control interfaces: torque/speed command semantics, state machine behavior, telemetry rates/units.
- Thermal interfaces: cooling flow assumptions, temperature limits, and derating behavior.
- Mechanical interfaces: mounting loads, shaft/coupling constraints, and vibration assumptions.
- Fault semantics: fault classes, annunciation flags, reversion behavior, and timeout handling.

Starter template: INTERFACE_CONTROL_DOCUMENT_TEMPLATE.md

## Suggested Repository Layout

- docs  Architecture, requirements, and verification plans
- firmware  Embedded control and diagnostics software
- libs  Shared protocol, control, and estimation libraries
- sim  Motor/inverter and propulsion behavior simulation tools
- tests  Unit, integration, bench, and fault-injection test suites
- tools  Calibration, logging, and analysis utilities
- configs  Motor profiles and operating-point presets
- data  Test captures, calibration data, and reference datasets

## Verification Strategy

- Requirements-to-test traceability for motor safety-relevant behaviors.
- Bench validation of control loops, sensing chains, and protection logic.
- Simulation campaigns for transient response and thermal derating behavior.
- Fault-injection tests for sensor failure, inverter faults, and over-current/over-temp events.
- Regression evidence for each interface-affecting change.

## Current Milestones (As of 2026-04-14)

Current repository maturity is bootstrap-level.

Near-term milestones:

1. Establish baseline repo structure (docs, firmware, libs, sim, tests, tools, configs, data).
2. Publish top-level motor subsystem requirements and fault assumptions.
3. Draft first ICD covering electrical, thermal, mechanical, and control interfaces.
4. Stand up minimal simulation scaffold for command response and derating behavior.
5. Define first bench-test matrix for startup, steady-state, and fault handling.

## Licensing

This repository uses a dual-license model:

- Source code: PolyForm Noncommercial 1.0.0 (LICENSE-CODE)
- Documentation and non-code design content: CC BY-NC-SA 4.0 (LICENSE-DOCS)

Commercial use is not granted by default. For commercial licensing, contact contact@aerocommons.org.

Contribution and file classification guidance: CONTRIBUTING.md

## Program Context

MAOS is an open-source experimental aircraft development effort. The aircraft has not yet flown. All design and performance values are targets subject to revision as analysis and testing mature.
