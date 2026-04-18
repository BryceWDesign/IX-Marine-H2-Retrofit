# Berth Replenishment and Port Interface

## Purpose

This file defines the berth-side operating concept and port interface basis for
IX-Marine-H2-Retrofit.

The reference architecture only makes sense if berth operations are treated as
part of the vessel system rather than an invisible assumption.

This file exists to answer the practical questions that appear the moment a
reader asks:

- when is hydrogen made onboard versus loaded onboard
- how much berth-side electrical demand is required
- how long does replenishment take
- what port assumptions are being made
- how does the vessel interface with shore during normal and abnormal operation

## Scope

This file covers concept-stage treatment of:

- onboard hydrogen generation while berthed
- backup shore hydrogen loading concept
- berth-side electrical demand
- berth time required for replenishment
- port ventilation and exclusion assumptions
- storage replenishment strategy
- offload / defuel concept
- emergency response interfaces
- operational dependencies on berth infrastructure

This file does **not** claim final port approval, terminal design, or final
bunkering procedure approval for a real vessel.

## Requirements traceability

This file directly supports:

- **R-070** define when hydrogen is generated onboard versus loaded from shore
- **R-071** define berth-side electrical demand and expected berth time
- **R-072** include a concept for emergency response interfaces between vessel
  and shore
- **R-073** strong dependency on port procedures and shore-side coordination
- **R-100** present operating dependency as a decision variable
- **R-102** make strategic and operational justification visible rather than
  hiding behind universal payback claims

It also operates under:

- **A-001** berth availability is part of the concept
- **A-004** onboard electrolysis is mainly a berth activity
- **A-008** operator values local emissions reduction and strategic benefit
- **A-011** hazard visibility matters more than simplicity theater
- **C-005** no strong green claim without source-boundary clarity
- **C-006** no fake class or port certainty
- **C-009** no fake economic certainty

## Locked berth-operating philosophy

The berth-operating philosophy for the reference vessel is:

- **make hydrogen onboard primarily while berthed**
- **use external electrical power as the normal replenishment energy source**
- **treat loaded hydrogen as a backup or schedule-support path**
- **treat the port as part of the system**
- **never pretend the vessel is infrastructure independent**

This means the vessel concept is explicitly dependent on berth conditions,
electrical availability, and port coordination.

## Normal replenishment strategy

The baseline replenishment strategy is a hybrid two-path approach.

### Path A — Normal replenishment by onboard electrolysis at berth

This is the default concept path.

Use this path when:

- the vessel has a planned berth window
- berth power is available
- the electrolyzer and water-treatment train are healthy
- the operator wants to replenish routine daily hydrogen demand without relying
  entirely on delivered compressed hydrogen

### Path B — Backup or schedule-support hydrogen loading from shore

This is the support path.

Use this path when:

- turnaround is too short for meaningful onboard electrolysis
- berth power is constrained
- the onboard electrolyzer is unavailable
- the vessel needs schedule recovery
- the operator wants resilience against berth-energy constraints

### Why both paths exist

The architecture is stronger with both because:

- onboard electrolysis alone can be too berth-time dependent
- delivered hydrogen alone can undermine the point of onboard generation
- the combination allows the vessel to remain conceptually credible under more
  realistic port conditions

## When hydrogen is made onboard versus loaded onboard

### Onboard generation should be used when:

- berth stay is long enough to justify operation
- overnight or extended layover is available
- shore power is stable and permitted
- local emissions and noise reduction at berth are valued
- the onboard production system is healthy
- schedule pressure is moderate

### Loaded hydrogen should be used when:

- berth window is short
- departure schedule cannot wait for full onboard generation
- the electrolyzer is faulted or in maintenance
- electricity cost or carbon intensity makes onboard generation temporarily less
  attractive
- contingency replenishment is needed for mission assurance

### Decision rule

The controls and operations concept should treat onboard generation as the
**primary routine replenishment path** and loaded hydrogen as the **contingency
or short-turnaround support path**.

This avoids false all-or-nothing framing.

## Locked berth-side electrical demand

### Reference concept electrical demand

For the locked reference concept, the berth-side electrical demand for active
hydrogen generation is:

- **450 kW class electrolyzer**
- plus supporting electrical loads for:
  - compression
  - drying / conditioning
  - water treatment
  - controls
  - ventilation

### Locked design allowance

Use a berth-side design demand allowance of:

**500 to 550 kW**

for active replenishment sessions.

### Why this number matters

This figure is large enough that the port interface cannot be treated as a
casual shore-power plug-in detail.

The berth must be able to support:

- sustained electrical demand
- safe connection
- operating procedure discipline
- coordination with port electrical infrastructure

## Locked berth-time expectations

### Reference replenishment expectations

Using the reference concept:

- **about 60 kg hydrogen top-up** should be treated as roughly an
  **8-hour practical berth session**
- **about 80 kg hydrogen top-up** should be treated as roughly a
  **10 to 11 hour practical berth session**

These are concept-stage planning values, not vendor guarantees.

### Why practical time is longer than raw production math

Practical berth time includes more than stack-only production time.

It must account for:

- startup and permissive checks
- process stabilization
- water-treatment readiness
- compression and storage-path realities
- stop and safe-secure actions
- operating margin rather than best-case brochure timing

### Operational implication

This concept is naturally aligned with:

- overnight berth windows
- extended service layovers
- vessels that return to a predictable home berth

It is not naturally aligned with high-frequency rapid-turnaround duty unless
backup loading is available.

## Port ventilation and exclusion assumptions

### Honest boundary

Final berth exclusion distances and vent interaction rules require real hazard
review, dispersion study, and port / class approval.

### What is locked at concept level

For layout and operating discipline, the repo assumes:

- no enclosed berth shed around active hydrogen vent or replenishment interface
- no deliberate vent outlet toward gangways, crane positions, air intakes, or
  routine personnel congregation points
- active replenishment or vent-related operations create a controlled
  keep-clear zone
- berth crews must know when the vessel is in active hydrogen-generation or
  hydrogen-service state

### Placeholder discipline values

For concept operations only, maintain:

- about **10 ft horizontal keep-clear** around active vent or service-point
  concept
- about **20 ft vertical keep-clear** above vent outlet concept

These values are placeholders for discipline only.
They are not port-approved stand-off distances.

## Storage replenishment strategy

### Locked strategy

The reference vessel uses a **hybrid replenishment strategy**:

1. onboard generation for normal daily-cycle recovery
2. backup delivered hydrogen path for schedule resilience

### Why this is the best configuration

This strategy is stronger than pure single-path dependence because it:

- acknowledges berth-power dependency
- acknowledges electrolyzer downtime possibility
- supports realistic port operations
- keeps the vessel useful during maintenance or schedule compression
- avoids pretending a concept demo vessel never faces logistics friction

### Inventory philosophy

The vessel should not be operated as if storage must always be brought from
empty to full in one session.

More realistic strategy is:

- recover normal daily use routinely
- keep bounded reserve margin
- use backup loading only when required by mission or disruption

## Offload / defuel concept

### Honest boundary

Routine offload / defuel procedures for a real vessel require approved hardware,
approved receiving method, and approved emergency rules.

### Concept-stage locked philosophy

The repo assumes:

- routine atmosphere venting is **not** the preferred normal defuel method
- preferred offload path is to a controlled shore receiver or service trailer
  if planned offload is required
- isolated small-volume depressurization may be used only as a bounded service
  action under approved maintenance logic
- emergency venting is a distinct abnormal event path, not a convenience method

### Why this matters

If the repo treats venting as casual, it weakens the whole safety framing.

## Emergency response interfaces

### Locked emergency-interface philosophy

The vessel must present a clear shore-facing emergency interface.

### Required concept elements

The berth and vessel interface should support at minimum:

- remote or berth-recognizable emergency stop relationship
- visible vessel hydrogen-system status indication
- clearly identifiable isolation concept
- clear emergency information pack or equivalent concept
- contact / response path between vessel crew and berth emergency responders
- known vent / relief outlet locations
- known restricted zones during active hydrogen operations

### Minimum information that should be available to shore responders

The concept assumes responders need access to at least:

- where hydrogen is stored
- where venting / relief exits are located
- what ESD state the vessel is in
- how to identify the hydrogen process status
- what spaces should be avoided
- who onboard has command authority during the event

## Berth operating sequence

The reference vessel's berth-side replenishment sequence is conceptually:

1. vessel arrives and secures
2. vessel enters housekeeping-alive state
3. berth power interface is inspected and connected if planned
4. emergency-stop coordination state is known
5. ventilation, detectors, and controls prove healthy
6. water-treatment path is prepared
7. clean-water reserve is validated
8. electrolysis starts when permissives are true
9. hydrogen is conditioned, compressed, and stored
10. session ends by controlled stop
11. storage is secured
12. departure readiness is assessed

This sequence is intentionally procedure-heavy because that is the honest nature
of the system.

## Backup hydrogen loading concept sequence

Where backup delivered hydrogen is used, the concept sequence is:

1. vessel secured and system in controlled berth state
2. relevant process segments isolated from onboard generation path as required
3. detector and safety systems live
4. service-point readiness confirmed
5. temporary restricted zone enforced
6. controlled loading proceeds under approved interface logic
7. post-transfer verification completed
8. transfer hardware disconnected and secured
9. dispatch readiness re-evaluated

This repo does not finalize nozzle standards or final transfer equipment.
It defines the operational expectation that the transfer path is deliberate and
highly controlled.

## Port dependency statement

The reference concept has **high port dependency**.

The architecture depends on the port or home berth providing, directly or
through coordinated support:

- electrical capacity
- controlled operating window
- emergency coordination
- safe berth geometry
- procedural discipline
- trained personnel or trainable response structure

This dependency is not a flaw in the repo.
It is part of the truth of the concept.

## Operational limitations the repo must keep visible

The berth and port concept should always keep the following limitations visible:

- short berth windows reduce onboard generation value
- unreliable shore power weakens the default replenishment path
- electrolyzer downtime increases dependence on delivered hydrogen
- electricity source carbon intensity changes the emissions case
- port procedures and emergency readiness matter
- berth configuration can make or break safe vent routing and restricted zones

## Monitoring and controls interface

The Monitoring & Controls Module should expose at minimum:

- berth power available / unavailable
- berth power healthy / unhealthy
- onboard generation selected / blocked / active
- backup loading mode selected / not selected
- replenishment session active / complete / faulted
- estimated session completion time
- hydrogen inventory before / after session
- berth-side emergency interface active / inactive
- active restricted-zone / caution state
- dispatch release after replenishment

## Proof-of-concept expectations

Later proof-of-concept artifacts for this file should make it possible to
inspect:

- whether berth electrical demand is clearly stated
- whether session time expectations are believable
- whether the hybrid replenishment strategy is coherent
- whether port dependency is visible instead of hidden
- whether emergency interface expectations are visible
- whether offload / defuel is treated safely instead of casually

## Explicit non-claims

This file does **not** claim:

- universal port readiness
- final berth electrical design approval
- final bunkering standard selection
- final vent-exclusion approval
- universal overnight replenishment feasibility at every port
- guaranteed low-carbon electricity supply
- final responder doctrine for a specific authority

## Summary

IX-Marine-H2-Retrofit is a berth-dependent marine hydrogen retrofit concept.

Its normal operating rhythm is to make hydrogen onboard while berthed using
external electrical power, use delivered hydrogen only as a backup or schedule-
support path, and rely on explicit port coordination, emergency interfaces, and
controlled berth procedures rather than pretending the vessel can operate as a
hydrogen island.
