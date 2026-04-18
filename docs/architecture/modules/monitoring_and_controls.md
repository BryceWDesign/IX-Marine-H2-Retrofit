# Monitoring & Controls Module

## Purpose

This file defines the Monitoring & Controls Module for IX-Marine-H2-Retrofit.

This module exists to make the entire retrofit architecture observable,
permissive-driven, fault-aware, and operationally understandable.

It is responsible for:

- state supervision across all major modules
- permissive-based startup and shutdown logic
- lockout enforcement
- alarm generation and prioritization
- event logging and trend retention
- degraded-mode coordination
- operator visibility
- black-start and recovery sequencing support

Without this module, the rest of the architecture is just hardware with
unclear behavior.

## Module role in the full architecture

This module interfaces directly with:

- the **Intake & Water Treatment Module**
- the **Hydrogen Generation Module**
- the **Gas Conditioning & Storage Module**
- the **Fuel Cell / Power Conversion Module**
- the **Safety & Ventilation Module**
- the **Housekeeping Energy Module**
- berth-side power and emergency interface signals
- operator HMI / dashboards
- maintenance-state controls and service indicators

It receives:

- process-state signals
- fault-state signals
- detector and ventilation status
- valve and contactor state
- water-quality state
- bus and battery state
- compressor and fuel-cell state
- maintenance and override state
- emergency stop state

It provides:

- run / inhibit / lockout decisions
- alarm state
- event logs
- operator status pages
- degraded dispatch classification
- restart permissives
- sequence control for startup, shutdown, and recovery
- maintenance visibility

This module does **not**:

- replace the need for good physical arrangement
- overrule safety lockouts for convenience
- turn uncertain data into certainty
- hide energy penalties or unresolved faults

## Requirements traceability

This module directly supports:

- **R-041** controlled recovery from bus loss
- **R-042** precharge, isolation, and no-backfeed logic at concept level
- **R-050** hydrogen-specific gas detection integration visibility
- **R-051** ventilation proving visibility
- **R-053** layered emergency shutdown states
- **R-070** define when hydrogen is made onboard versus loaded onboard
- **R-080** monitoring and controls concept with process, safety, and
  maintenance visibility
- **R-081** alarm prioritization
- **R-082** lockouts for bad water quality, failed ventilation proof,
  unresolved gas alarms, and maintenance-state conflicts
- **R-083** preserve event logs across blackout or restart events

It also operates under:

- **A-009** maintenance access is first-order
- **A-011** hazard visibility over simplicity theater
- **C-004** no hidden energy accounting
- **C-008** no single-point safety philosophy
- **C-010** later files may not silently contradict this control basis

## Locked control philosophy

The Monitoring & Controls Module is locked to the following philosophy:

- permissives before action
- visibility before restart
- trip first where hazard requires it
- degrade explicitly instead of failing ambiguously
- log what happened, not what the system wishes happened
- separate advisory states from dispatch-blocking states
- preserve critical safety visibility during degraded power states
- never allow an override to masquerade as normal operation

## Control architecture concept

The baseline control architecture is split conceptually into two layers:

### Layer C-1 — Safety-critical supervision layer

This layer handles:

- gas alarm ingestion
- ventilation proving
- ESD state control
- hard interlock decisions
- restart inhibit reasons
- emergency stop handling
- critical shutdown paths

### Layer C-2 — Process and operational supervision layer

This layer handles:

- process sequencing
- operator interface
- trend logging
- dispatch status
- maintenance countdown logic
- advisory and optimization-style visibility
- berth replenishment session logic
- energy accounting and reporting

### Why the split matters

The repo is not allowed to treat convenience controls and safety logic as the
same thing.

Safety-critical functions must remain conceptually separable from general
operational supervision.

## Submodule breakdown

The Monitoring & Controls Module is divided into ten submodules:

1. State Model and Mode Manager Submodule
2. Startup Permissives and Lockout Submodule
3. Shutdown and Trip Orchestration Submodule
4. Alarm Management Submodule
5. Event Logging and Sequence-of-Events Submodule
6. Trend and Performance Analytics Submodule
7. Dashboard / HMI Submodule
8. Maintenance Countdown and Service State Submodule
9. Dispatch Classification and Degraded-Mode Manager Submodule
10. Black-Start and Recovery Sequencer Submodule

---

## 1) State Model and Mode Manager Submodule

### Function

Define the system's current operating mode and make it visible.

### Locked philosophy

The vessel should never be in a mystery state.

### Required system states

The controls architecture shall recognize at minimum these top-level states:

1. cold / secured
2. housekeeping alive
3. berth readiness
4. water treatment active
5. electrolysis active
6. hydrogen replenishment complete / standby
7. operational on fuel-cell plus battery
8. battery-dominant degraded mode
9. hydrogen process lockout
10. maintenance state
11. emergency shutdown state

### Required behavior

The controls layer shall make the current state explicit and must not allow the
system to appear "normal" when actually in degraded or inhibited condition.

### Why it matters

State ambiguity is one of the fastest ways to create operator error.

---

## 2) Startup Permissives and Lockout Submodule

### Function

Determine whether a requested function may start.

### Locked philosophy

No major process start shall occur unless required permissives are true.

### Required lockout categories

The controls layer shall support lockouts for at minimum:

- bad water quality
- low clean-water reserve
- ventilation not proven
- unresolved gas trip
- emergency stop active
- purge incomplete
- compressor fault blocking charge path
- manifold state mismatch
- maintenance lockout
- unresolved battery / bus state conflict
- cooling failure affecting startup
- critical detector fault in affected zone

### Startup examples

#### Electrolysis startup requires at minimum:
- berth power healthy
- clean water in spec
- clean-water reserve sufficient
- downstream gas path available
- ventilation proven
- no active gas trip
- no maintenance lockout
- no emergency stop
- required valves confirmed

#### Fuel-cell startup requires at minimum:
- supply path healthy
- purge complete
- no active leak trip in affected supply zone
- bus and battery state acceptable
- cooling healthy
- maintenance state clear
- no emergency shutdown prohibition

#### Dispatch release requires at minimum:
- mission hydrogen threshold or bounded reduced mission threshold met
- battery SOC adequate
- no unresolved trip requiring berth hold
- operator-visible dispatch classification generated

### Lockout philosophy

A lockout reason must be visible, specific, and logged.

---

## 3) Shutdown and Trip Orchestration Submodule

### Function

Coordinate orderly stop or forced isolate behavior.

### Locked philosophy

Trip behavior must be structured, not improvised.

### Required stop categories

The controls architecture shall support at minimum:

- normal controlled stop
- process isolate stop
- hydrogen isolate stop
- major event stop

These align with the ESD philosophy defined elsewhere in the repo.

### Required behavior

The controls layer should coordinate:

- electrolysis stop
- compressor stop
- storage isolation
- fuel-cell unload / trip
- nonessential load shedding
- alarm escalation
- persistence of safety visibility
- event logging

### Restart rule

Major safety trip restart must remain inhibited until the cause is cleared and
a deliberate reset / re-enable path is satisfied.

---

## 4) Alarm Management Submodule

### Function

Present abnormal conditions in a way that supports action instead of noise.

### Locked philosophy

Not every abnormal event deserves the same urgency, but critical events must be
impossible to miss.

### Alarm classes

At minimum, the repo shall use:

#### A-1 — Advisory
Use for:
- trend drift
- nearing maintenance threshold
- minor helper-source loss
- noncritical diagnostic irregularity

#### A-2 — Action Required
Use for:
- reduced dispatch condition
- water-treatment degradation needing service
- partial subsystem loss
- reserve depletion warning
- ventilation warning prior to hard trip threshold where applicable

#### A-3 — Trip / Immediate Safety Action
Use for:
- severe gas alarm
- ventilation failure in required zone
- ignited release detection
- emergency stop
- critical battery protection trip
- severe compressor fault that forces isolate
- purge failure blocking safe startup
- unresolved major lockout condition

### Alarm management rules

The controls layer should support:

- alarm latching where hazard or trip consequence requires it
- acknowledgement state
- active versus historical distinction
- suppression only under controlled maintenance or approved service states
- no silent auto-clear for serious safety events

---

## 5) Event Logging and Sequence-of-Events Submodule

### Function

Preserve a traceable record of what happened and in what order.

### Locked philosophy

If the system trips, degrades, or blocks dispatch, the operator and reviewer
must be able to reconstruct why.

### Required event coverage

The event log shall capture at minimum:

- state transitions
- start / stop events
- lockout assertions and clears
- ESD transitions
- gas alarm transitions
- ventilation proof loss and restore
- purge start / complete / fail
- compressor fault events
- water-quality out-of-spec events
- battery reserve threshold crossings
- dispatch classification changes
- load-shed events
- blackout / bus loss events
- black-start attempts and outcomes
- maintenance mode entry / exit

### Sequence-of-events expectations

The architecture should preserve event ordering tightly enough that a reviewer
can see what happened first during a complex event.

### Persistence rule

Event history should survive power interruption as far as the architecture
reasonably allows.

---

## 6) Trend and Performance Analytics Submodule

### Function

Turn repeated operating data into maintainable insight.

### Locked philosophy

The repo should not stop at raw alarms. It should show operating drift where the
drift matters.

### Required trends

The controls architecture should support trend visibility for at minimum:

- hydrogen produced per berth session
- energy consumed per hydrogen-production session
- estimated kWh per kg hydrogen
- clean-water conductivity trend
- pretreatment differential pressure trend
- storage pressure trend
- compressor temperature / fault frequency trend
- fuel-cell operating hours and availability
- battery SOC trend
- battery reserve encroachment count
- ventilation failure count
- gas alarm history
- helper-source contribution time if installed

### Why this matters

Trend visibility supports:

- maintenance timing
- operator trust
- proof-of-concept review
- failure pattern recognition
- decision-grade rather than presentation-grade insight

---

## 7) Dashboard / HMI Submodule

### Function

Provide the operator and reviewer with coherent visibility into the system.

### Locked philosophy

The HMI should answer operational questions, not just display data.

### Required dashboard pages

The concept should include at minimum:

#### Page 1 — Overview
- current system state
- hydrogen inventory estimate
- battery SOC
- fuel-cell output
- electrolysis state
- dispatch classification
- active alarms summary

#### Page 2 — Water and Process
- intake / treatment status
- pretreatment differential pressure
- water-quality in-spec / out-of-spec
- clean-water reserve
- electrolyzer run / inhibit status
- session production estimate

#### Page 3 — Gas and Storage
- compressor state
- storage pressure
- charge / discharge path status
- isolation state
- vent / relief event flag
- gas-related alarms

#### Page 4 — Power
- Fuel Cell A state
- Fuel Cell B state
- battery charge / discharge
- main bus healthy / faulted
- converter availability
- load-shed status

#### Page 5 — Safety
- gas detector map summary
- ventilation proof state
- ESD state
- purge status
- ingress alarm state
- maintenance lockout state

#### Page 6 — Maintenance and Trends
- next service countdowns
- operating hours
- bump-test due status
- filter / membrane service due status
- compressor service due status
- trend summaries

### HMI rule

A blocked dispatch or blocked startup must be explained in plain operational
terms, not only by obscure internal code.

---

## 8) Maintenance Countdown and Service State Submodule

### Function

Track and expose service burden so it cannot hide until failure.

### Locked philosophy

If the architecture has consumables, service intervals, and test requirements,
the controls layer should surface them.

### Required tracked items

The concept should support countdown or due-state visibility for at minimum:

- primary strainer service
- pretreatment element service
- RO / polishing service
- gas detector bump test
- compressor service
- fuel-cell module operating-hour milestone
- battery inspection milestone
- ventilation equipment inspection
- relief / vent-path inspection
- calibration intervals for critical sensors where applicable

### Maintenance state handling

When maintenance mode is entered, the controls layer should:

- record the event
- show which subsystem is intentionally disabled
- block unsafe restart paths
- distinguish maintenance isolation from fault trip

---

## 9) Dispatch Classification and Degraded-Mode Manager Submodule

### Function

Translate subsystem health into operational release guidance.

### Locked philosophy

Dispatch should not be binary when the system actually has bounded partial
capability.

### Required dispatch classes

The controls architecture shall support at minimum:

#### Green dispatch
- planned mission permitted

#### Amber dispatch
- reduced mission, reduced endurance, or conditional release only

#### Red dispatch
- departure blocked

### Inputs to dispatch classification

Dispatch logic should consider at minimum:

- usable hydrogen inventory
- battery SOC and reserve margin
- fuel-cell module availability
- active process lockouts affecting future mission support
- unresolved safety alarms
- maintenance locks affecting mission-critical equipment
- degraded cooling or power-conversion state
- berth replenishment success / failure state

### Degraded-mode visibility

If the vessel is in degraded return mode, the controls layer must make that
state unmistakable.

---

## 10) Black-Start and Recovery Sequencer Submodule

### Function

Coordinate recovery from dead-bus or near-dead-bus conditions.

### Locked philosophy

Recovery must be staged and safety-aware.

### Required sequence logic

The sequence should conceptually support:

1. restore housekeeping bus
2. restore safety PLC / controls
3. restore gas detection and event logging
4. prove required ventilation paths
5. check maintenance and trip states
6. restore main battery bus
7. evaluate fuel-cell start permissives
8. perform required purge
9. start one fuel-cell module if allowed
10. restore additional loads in stages
11. restore second fuel-cell module if needed and allowed

### Failure behavior

If recovery stalls at any stage:
- the failure reason must be visible
- unsafe auto-advance must be blocked
- the operator must be shown the blocking condition clearly

### Why it matters

A black-start sequence is where weak architectures reveal themselves.

---

## Operating principles

### Principle M-001 — Safety beats convenience
The controls layer must never override a hard safety lockout merely to preserve
appearance of continuity.

### Principle M-002 — Specific reasons beat generic faults
A user should see *why* startup is blocked, not just "system unavailable."

### Principle M-003 — Degraded mode is a defined state
Partial operation must be named and bounded.

### Principle M-004 — Trends matter
Maintenance and process drift must be visible before failure where possible.

### Principle M-005 — Logs are part of the architecture
If a system trips but cannot explain itself afterward, it is weaker than it
looks.

## Footprint and arrangement allowances

### Controls hardware allowance

Allow approximately:

- **8 ft × 4 ft** concept envelope for central controls, safety I/O, data
  logging, and HMI-support hardware cluster
- distributed local I/O where arrangement requires it
- protected access for maintenance and inspection

### Placement philosophy

The core controls hardware should be arranged:

- away from obvious damage and spray pathways
- with clear wiring segregation
- with access to service indicators and removable modules
- with protection against casual environmental abuse

### Power continuity requirement

The controls cluster shall be aligned with the Housekeeping Energy Module so
critical visibility survives through startup, shutdown, and degraded states.

---

## Failure modes this module must expect

This module must already assume the following can happen:

- stale or missing sensor data
- detector disagreement
- false lockout trigger
- missing permissive due to instrumentation fault
- event logger continuity challenge during blackout
- HMI alive but process unavailable
- maintenance override left active
- communication loss between distributed control segments
- sequence stall during startup
- black-start reserve insufficient
- conflicting operator command during active trip state

The module must be designed to expose and contain these issues rather than
hide them.

## Maintainability requirements

The controls architecture should support access to at minimum:

- controller modules
- safety I/O modules
- power-conditioning for controls
- removable storage or service interfaces where needed
- network / communications diagnostics points
- HMI service access
- local status indicators
- protected manual reset or acknowledgement points

Maintainability applies to software-visible systems too.

## Monitoring and controls interface summary

Because this file defines the integrating module, it consumes the interface
signals defined in the other module files and transforms them into:

- explicit system state
- startup allowed / blocked status
- trip reason code
- dispatch class
- active alarm set
- service due status
- trend summaries
- black-start readiness
- degraded-mode visibility

## Proof-of-concept expectations

Later proof-of-concept artifacts for this module should make it possible to
inspect:

- whether startup permissives are coherent
- whether shutdown escalation is understandable
- whether alarms are prioritized correctly
- whether the dashboard answers real operator questions
- whether event logging preserves sequence clarity
- whether degraded dispatch logic is bounded
- whether black-start sequencing avoids unsafe shortcuts

## Explicit non-claims

This module does **not** claim:

- final PLC vendor selection
- final software implementation
- cybersecurity completion
- final class acceptance of control hardware
- elimination of operator error
- perfect sensor truth in all cases

It defines the control discipline the repo must obey.

## Summary

The Monitoring & Controls Module is the coordination brain of
IX-Marine-H2-Retrofit.

Its job is to convert raw subsystem status into explicit operating state,
permissive-driven action, prioritized alarms, logged events, degraded-mode
guidance, and staged recovery logic so the vessel architecture remains
understandable, reviewable, and honest even when faults occur.
