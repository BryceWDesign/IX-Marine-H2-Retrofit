# Hydrogen Generation Module

## Purpose

This file defines the Hydrogen Generation Module for IX-Marine-H2-Retrofit.

This module is responsible for converting treated process water and external
electrical input into hydrogen in a way that is physically honest, inspectable,
and bounded by clear permissives.

It exists to solve the following problems:

- generate hydrogen onboard without pretending the vessel is a perpetual-motion
  machine
- make berth-oriented hydrogen replenishment practical for the reference vessel
- protect the electrolyzer from bad water, bad ventilation state, and bad
  startup conditions
- separate production logic from downstream gas conditioning and storage logic
- expose the actual operating dependencies instead of hiding them

## Module role in the full architecture

This module sits between:

- the **Intake & Water Treatment Module**
- the **Gas Conditioning & Storage Module**
- the **Monitoring & Controls Module**
- the **Safety & Ventilation Module**
- the berth-side electrical interface

It takes in:

- treated process water
- external electrical power
- permissive / lockout status from controls and safety systems

It produces:

- raw hydrogen stream for downstream separation and conditioning
- oxygen byproduct stream that must be handled safely
- heat and operating-state data
- production metrics for energy-truth accounting

This module does **not**:

- store hydrogen
- deliver propulsion directly
- bypass water-quality protection
- claim net-positive propulsion energy from seawater or vessel motion

## Requirements traceability

This module directly supports:

- **R-012** onboard hydrogen generation framed primarily as berth-oriented
  process using external electrical energy
- **R-022** treated water suitable for selected electrolyzer path
- **R-023** electrolyzer blocked on unacceptable water quality
- **R-030** treated-water baseline, not raw seawater direct feed
- **R-031** include gas drying and pressure-management support functions
- **R-041** controlled recovery from bus loss
- **R-050** hydrogen-specific gas detection integration
- **R-051** ventilation proving for hydrogen-bearing spaces
- **R-052** safe state on loss of required ventilation
- **R-053** layered emergency shutdown states
- **R-082** lockouts for water quality, ventilation proof, unresolved gas alarm,
  and maintenance conflicts
- **R-090** proof-of-concept inspectability

It also operates under:

- **A-004** onboard electrolysis is mainly a berth activity
- **A-005** seawater is feedstock, not the primary energy source
- **A-007** treated water is mandatory for the baseline electrolyzer path
- **A-011** hazard visibility over simplicity theater
- **C-001** no perpetual-motion framing
- **C-004** no hidden energy accounting
- **C-006** no fake class certainty

## Locked baseline technology choice

The baseline electrolyzer choice for this repository is:

**PEM electrolyzer architecture**

### Why PEM is the locked baseline here

PEM is chosen at concept stage because it fits the repo's needs better than a
casual alternative for the selected reference vessel:

- fast response compared with slower industrial-only assumptions
- more believable integration with berth-side electrical operation
- compactness relative to some other approaches
- clear treated-water requirement, which reinforces the repo's honesty about
  upstream water handling
- a strong match to modular skid-based architecture

This file does **not** claim PEM is the best answer for every marine case.
It is the baseline answer for this repo.

## Locked reference sizing

The Hydrogen Generation Module is locked to the following concept-stage sizing
for the reference vessel:

- **electrolyzer nameplate:** 450 kW class
- **production focus:** berth-oriented replenishment
- **daily hydrogen target basis:** approximately 60 to 80 kg/day for the
  reference vessel mission envelope
- **nominal operating window:** overnight or extended berth layover
- **operating energy basis:** this module is expected to dominate the berth
  electrical load during hydrogen-generation sessions

These are concept anchors, not final vendor purchase commitments.

## Core design philosophy

The module is locked to the following design philosophy:

- no hydrogen generation without treated water proof
- no hydrogen generation without ventilation proof
- no hydrogen generation without clear power-path validity
- no hydrogen generation during unresolved gas alarm state
- no casual restart after fault
- no hidden process energy penalty
- no claim that the electrolyzer is a background accessory

This module is one of the main reasons the vessel becomes a berth-dependent
architecture.

## Submodule breakdown

The Hydrogen Generation Module is divided into seven submodules:

1. Electrical Input and Power Conditioning Submodule
2. Process Water Feed and Quality Gate Submodule
3. Electrolyzer Core Stack Submodule
4. Gas/Liquid Separation Interface Submodule
5. Oxygen Handling Interface Submodule
6. Thermal Management Interface Submodule
7. Production Supervisory Logic Submodule

---

## 1) Electrical Input and Power Conditioning Submodule

### Function

Receive external electrical power and condition it for electrolyzer operation.

### Locked operating assumption

The electrolyzer is expected to run mainly while the vessel is berthed and
connected to external electrical supply.

### Required functions

This submodule shall support:

- berth power acceptance logic
- input quality verification
- controlled energization
- precharge / controlled startup behavior where relevant
- power-use metering for energy-truth accounting
- graceful stop on loss of permitted conditions

### Design expectations

The submodule should expose at minimum:

- berth power available / unavailable
- input power healthy / unhealthy
- active power draw
- cumulative energy consumed
- emergency stop state
- commanded start / stop state

### Non-claim

This module does not assume the vessel can always obtain cheap or clean shore
power. It only assumes that berth power is the normal replenishment path for
the reference concept.

---

## 2) Process Water Feed and Quality Gate Submodule

### Function

Admit treated process water to the electrolyzer only when quality and quantity
conditions are acceptable.

### Locked philosophy

The electrolyzer must be treated as downstream of a **hard water-quality gate**.

### Required inputs

This submodule shall consume at minimum:

- clean-water day tank level status
- product-water in-spec / out-of-spec signal
- active maintenance bypass status
- water-feed flow confirmation
- leak or drain abnormality status where available

### Startup permissives

Electrolyzer start shall require all of the following:

- clean-water reserve above startup threshold
- water quality in acceptable range
- no active maintenance state on the feed system
- no unresolved severe upstream blockage condition
- no controller mismatch on process-water supply state

### Failure behavior

If water quality goes out of bounds during operation:

- electrolyzer production shall stop or ramp to safe stop
- fault shall be logged
- automatic restart shall remain blocked until acceptable conditions return and
  operator or logic permissives are satisfied

### Design consequence

This makes the water path operationally visible instead of turning water into
an invisible assumption.

---

## 3) Electrolyzer Core Stack Submodule

### Function

Convert treated water and electrical energy into hydrogen and oxygen streams.

### Locked concept

Use a modular PEM electrolyzer skid concept sized to the 450 kW class for the
reference vessel.

### Core operating intent

The electrolyzer core stack is expected to:

- run while berthed
- replenish onboard hydrogen inventory
- produce trendable output metrics
- stop safely when key permissives are lost
- avoid restart under unresolved fault conditions

### Expected operating visibility

The module should make at least the following visible to controls and operator:

- run state
- commanded load or production state
- stack current and voltage summary
- cumulative operating hours
- start count
- hydrogen production estimate
- fault state
- inhibited / ready / running / stopping status

### Design consequence

Because this is a marine retrofit context, the stack cannot be treated like a
sealed black box that the repo ignores. The system must show how the stack is
allowed to run and how it is forced to stop.

### Non-claim

This repo does not claim stack life, replacement interval, or vendor
performance beyond concept-stage reference assumptions.

---

## 4) Gas/Liquid Separation Interface Submodule

### Function

Transition the raw electrolyzer output toward downstream gas conditioning.

### Why this matters

The electrolyzer does not magically hand off perfect storage-ready hydrogen.
There is an interface step between the stack and the downstream gas path.

### Required concept functions

This interface shall support:

- gas/liquid separation
- flow-state confirmation
- downstream readiness awareness
- startup/shutdown coordination
- fault propagation to controls

### Core logic

Hydrogen generation shall not continue normally if:

- downstream gas path is unavailable
- separation function is unhealthy
- drainage or carryover state is abnormal
- gas-conditioning permissive is lost

### Design consequence

The stack cannot be treated as independent from what happens next.
Upstream production and downstream gas handling are coupled.

---

## 5) Oxygen Handling Interface Submodule

### Function

Address the oxygen byproduct path explicitly rather than pretending it does not
exist.

### Locked concept

The baseline repository concept is:

- oxygen is **not** treated as a monetized product
- oxygen handling is treated as a safety and routing concern
- oxygen is vented or managed through a dedicated, intentionally designed path

### Required design principles

The oxygen path should:

- avoid cross-coupling with hydrogen-bearing vent systems
- avoid trapped oxidizer pockets in occupied or ignition-sensitive areas
- remain visible in the process diagram and hazard review
- support safe shutdown and isolation logic

### Non-claim

This repo does not claim commercial oxygen use or onboard oxygen-product
optimization.

The oxygen stream is a process consequence that must be routed safely.

---

## 6) Thermal Management Interface Submodule

### Function

Handle heat rejection and operating thermal stability for hydrogen generation.

### Why it exists

Electrolysis is not electrically demanding only.
It is also thermally real.

### Required concept functions

The module should account for:

- stack thermal monitoring
- cooling interface state
- overtemperature fault path
- startup thermal permissives where relevant
- controlled stop on thermal anomaly

### Design consequence

The repository must not treat heat as an invisible side effect.
If the electrolyzer is meaningful, its thermal behavior is meaningful.

### Placement implication

Thermal interface routing should not force absurd maintenance access penalties or
unsafe proximity to hydrogen-handling equipment.

---

## 7) Production Supervisory Logic Submodule

### Function

Coordinate start, stop, hold, inhibit, and fault handling behavior for the
entire Hydrogen Generation Module.

### Locked philosophy

Hydrogen generation must be permissive-driven, not switch-driven.

### Minimum required permissives for start

All of the following shall be true before electrolysis begins:

- berth electrical input healthy
- no emergency stop active
- hydrogen-space ventilation proven
- no active hydrogen gas trip
- process-water quality valid
- clean-water reserve sufficient
- downstream gas path healthy
- maintenance mode not active
- required valves and process states confirmed
- no unresolved critical sensor fault in the module

### Minimum required stop triggers

The module shall command safe stop if any of the following occur:

- loss of required ventilation
- severe hydrogen leak trip in affected space
- emergency stop
- severe water-quality fault
- critical downstream gas-path fault
- severe thermal fault
- critical internal controller fault
- berth power loss outside acceptable ride-through handling

### Restart philosophy

Restart after critical trip must not be automatic by default.

The repo should assume that restart requires at least:

- fault condition cleared
- permissives restored
- alarm acknowledged
- operator or supervisory re-enable permitted

### Logging

The supervisory layer shall log at minimum:

- start events
- stop events
- lockout reasons
- trip reasons
- energy consumed
- production estimate
- inhibited time
- cumulative run hours

---

## Reference performance basis

The module is conceptually sized to support the reference vessel's hydrogen
inventory replenishment target in a berth window rather than as a continuous
underway generator.

### Operating interpretation

This means the module is expected to support:

- nightly or extended-layover replenishment
- recovery of daily hydrogen use within a realistic berth period
- alignment with the vessel's harbor-duty rhythm

### What this does not mean

It does not mean:

- the vessel is independent of berth power
- hydrogen production is trivial
- the module can run casually under any port condition
- ship-motion harvesters make berth power unnecessary

---

## Footprint and service allowances

The Hydrogen Generation Module shall be given concept-stage layout allowances
that reflect actual service needs.

### Locked envelope allowance

Allow approximately:

- **20 ft × 10 ft** main process-room envelope for electrolyzer and immediate
  process interfaces
- **3 ft** preferred front service aisle
- **2 ft** minimum side access where routine service is expected
- clear isolation-valve access
- overhead removal path or practical service extraction route

### Placement philosophy

The module should be placed:

- near the water-treatment output path
- near electrical distribution support
- away from accommodation spaces
- in a location compatible with gas-safe or gas-managed enclosure philosophy
- where maintenance access can be preserved

### Arrangement warning

A compact-looking process room that cannot be serviced is a bad design even if
the floorplan looks efficient.

---

## Energy-accounting expectations

This module is one of the largest electrical loads in the entire architecture.

The repo must later expose at minimum:

- instantaneous input power
- cumulative energy consumed per replenishment session
- estimated hydrogen produced
- energy-per-unit-hydrogen trend
- time spent inhibited versus producing

The point is to make performance and parasitic cost visible.

## Failure modes this module must expect

This module must already assume the following failure or degradation cases are
real:

- loss of berth power
- poor input power quality
- bad process-water feed
- insufficient clean-water reserve
- ventilation failure
- hydrogen leak in associated space
- unresolved purge or valve-state conflict
- internal controller fault
- gas-path unavailability
- thermal excursion
- faulty sensor input
- maintenance-state mismatch
- emergency stop activation

Detailed hazard treatment is handled in later files, but this module must be
written as if those failures will happen.

## Degraded operation behavior

The Hydrogen Generation Module is allowed to be unavailable while the rest of
the vessel concept still retains partial function.

If this module is unavailable:

- berth-side battery charging may still proceed if safely arranged
- stored hydrogen may still support future operation if inventory exists
- vessel dispatch may be reduced, delayed, or blocked depending on inventory
- operator must see the reason clearly

The architecture is not allowed to pretend that no electrolysis means no system
value at all. It is also not allowed to hide the operational penalty.

## Maintainability requirements

The module should support access to at minimum:

- electrical isolation points
- process-water isolation points
- service filters or equivalent balance-of-plant consumables
- stack-related service envelope
- drainage or purge access points
- sensors that require inspection or replacement
- emergency stop and local shutdown interfaces

Routine maintenance hostility is treated as a design flaw.

## Monitoring and controls interface

This module shall provide the Monitoring & Controls Module with at minimum:

- module ready / inhibited / running / stopping / tripped
- berth power available / unavailable
- water-quality valid / invalid
- clean-water reserve healthy / low
- ventilation proven / failed
- gas trip clear / active
- thermal state healthy / faulted
- downstream gas path ready / unavailable
- cumulative operating hours
- cumulative energy consumed
- estimated hydrogen production
- trip reason code
- maintenance due indicators if available

## Proof-of-concept expectations

Later proof-of-concept artifacts for this module should make it possible to
inspect:

- whether startup permissives are coherent
- whether berth-oriented generation logic is believable
- whether water-quality lockout is hard enough
- whether downstream coupling is visible
- whether the module exposes its real dependencies
- whether stop and inhibit logic are not hand-waved

## Explicit non-claims

This module does **not** claim:

- raw seawater direct-feed PEM operation as the baseline path
- universal cost competitiveness
- universal vessel applicability
- carefree operation without port dependency
- automatic safe restart after major fault
- final vendor packaging or procurement certainty
- class-approved installation for a real hull

## Summary

The Hydrogen Generation Module is the berth-oriented hydrogen-production core of
IX-Marine-H2-Retrofit.

Its job is to accept external electrical power and treated process water,
produce hydrogen under controlled permissives, expose its true operating burden,
and stop safely when water quality, ventilation, gas safety, power quality, or
downstream readiness no longer support credible operation.
