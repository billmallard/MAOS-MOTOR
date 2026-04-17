# MAOS-MOTOR Initial Requirements v0

Status: Draft / Working notes. Intentionally early and incomplete.
Purpose: Seed motor subsystem requirements for iterative refinement.

## Functional Requirements

- MOT-SYS-001: The motor subsystem shall support propulsion operation in the 120-350 kW class through configurable hardware profiles.
- MOT-SYS-002: The subsystem shall support both generator-role and propulsor-role configuration modes.
- MOT-SYS-003: The motor controller shall implement deterministic state transitions for init, ready, run, derate, and fault.
- MOT-SYS-004: Torque/speed command semantics shall be normalized independent of vendor-specific APIs.

## Interface Requirements

- MOT-IF-001: HV bus interface shall define nominal voltage range, current limits, and inrush behavior.
- MOT-IF-002: Mechanical interface shall define shaft speed envelope, torque limits, and coupling assumptions.
- MOT-IF-003: Thermal interface shall define coolant requirements and derating thresholds.
- MOT-IF-004: Telemetry interface shall publish current, voltage, temperature, speed, torque estimate, and fault flags.
- MOT-IF-005: Control interface shall define command/update rates, timeout behavior, and fallback response.

## Safety and Fault Requirements

- MOT-FLT-001: The subsystem shall detect overcurrent, overvoltage, undervoltage, overtemperature, and comms timeout faults.
- MOT-FLT-002: Fault responses shall be deterministic and include bounded torque reduction or controlled disable.
- MOT-FLT-003: Fault behavior shall be role-aware (generator vs propulsor).
- MOT-FLT-004: Fault and derating events shall be logged with reason codes.

## Verification Requirements

- MOT-VER-001: Bench tests shall verify command-response behavior across the defined operating envelope.
- MOT-VER-002: Bench tests shall verify thermal derating behavior against configured thresholds.
- MOT-VER-003: Fault-injection tests shall verify each required protection path.
- MOT-VER-004: Requirement-to-test traceability shall be maintained.
